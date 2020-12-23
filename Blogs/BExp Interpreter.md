# BExp: Interpreter
* In the interpreter, we implemented boolean evaluate functions evalBool for *and*, *or*, *not* as well as ==, <=, <, >, >= operations. <br>

  * Interpreter.hs
    <pre>
    1   -- Interpreter for LambdaNat6
    2   -- numbers, conditionals, recursion, lists
    3   {-# LANGUAGE StandaloneDeriving, DeriveDataTypeable, TypeApplications,
    4   ExplicitForAll, ScopedTypeVariables #-}
    5
    6     module Interpreter where
    7 
    8     import AbsLambdaNat
    9     import ErrM
    10    import PrintLambdaNat
    11
    12    import Data.Map ( Map )
    13    import qualified Data.Map as M
    14
    22    execCBN :: Program -> Exp
    23    execCBN (Prog e) = evalCBN e
    24    
    25    evalCBN :: Exp -> Exp
    26    evalCBN (EApp e1 e2) = case (evalCBN e1) of
    27      (EAbs i e1') -> evalCBN (subst i e2 e1')
    28      e1' -> EApp e1' e2
    29
    31    -- evalCBN
    32    evalCBN (BIf f1 e3 e4) = if (bExp2Bool(evalBool f1)) then evalCBN e3 else evalCBN e4
    33    evalCBN (ELet i e1 e2) = evalCBN (EApp (EAbs i e2) e1)
    34    evalCBN (ERec i e1 e2) = evalCBN (EApp (EAbs i e2) (EFix (EAbs i e1)))
    35    evalCBN (EFix e) = evalCBN (EApp e (EFix e))
    36    evalCBN (EMinusOne e) = case (evalCBN e) of
    37    ENat0 -> ENat0
    38     (ENatS e) -> e
    39
    40    evalCBN (ENatS e') = ENatS (evalCBN e')
    41
    42    evalCBN (ECons e1 e2) = ECons (evalCBN e1) (evalCBN e2)
    43
    44    evalCBN(EHd e) =case (evalCBN e) of
    45      ENil -> ENil
    46      ECons e1 e2 -> e1
    47
    48    evalCBN(ETl e) = case (evalCBN e) of
    49      ENil -> ENil
    50      ECons e1 e2 -> e2
    51
    52    evalCBN x = x
    53 
    54    -- bExp2Bool
    55    bExp2Bool :: BExp -> Bool
    56    bExp2Bool BTrue = True
    57    bExp2Bool	BFalse = False
    58
    59    -- evalBool
    60    -- and, or, not operations
    61    evalBool :: BExp -> BExp
    62    evalBool (BAnd f1 f2) = case (evalBool f1) of
    63      BFalse -> BFalse
    64      BTrue -> case (evalBool f2) of
    65        BTrue -> BTrue
    66        BFalse -> BFalse
    67
    68    evalBool (BOr f1 f2) = case (evalBool f1) of
    69      BTrue -> BTrue
    70      BFalse -> case (evalBool f2) of
    71        BTrue -> BTrue
    72        BFalse -> BFalse
    73
    74    evalBool (BNot f1) = case (evalBool f1) of
    75      BFalse -> BTrue
    76      BTrue -> BFalse
    77
    78    -- ==, <=, <, >, >= operations
    79    evalBool (BG f1 f2) = case (evalCBN f1) of
    80      ENat0 -> BFalse
    81      _-> case (evalCBN f2) of
    82        ENat0 -> BTrue
    83        _->BG (EMinusOne f1) (EMinusOne f2)
    84
    85    evalBool (BL f1 f2) = case (evalCBN f1) of
    86      ENat0 -> BTrue
    87      _-> case (evalCBN f2) of
    88        ENat0 -> BFalse
    89        _->BL (EMinusOne f1) (EMinusOne f2)
    90
    91    evalBool (BGe f1 f2) = case (evalCBN f1) of
    92      ENat0 -> BTrue
    93      _-> case (evalCBN f2) of
    94        ENat0 -> BFalse
    95        _->BGe (EMinusOne f1) (EMinusOne f2)
    96
    97    evalBool (BLe f1 f2) = case (evalCBN f2) of
    98      ENat0 -> BTrue
    99      _-> case (evalCBN f1) of
    100       ENat0 -> BFalse
    101       _->BLe (EMinusOne f1) (EMinusOne f2)
    102
    103   evalBool (BEquals f1 f2) = case (evalCBN f1) of
    104     ENat0 -> case (evalCBN f2) of
    105       ENat0 -> BTrue
    106       _-> BEquals (EMinusOne f1) (EMinusOne f2)
    107     _-> BEquals (EMinusOne f1) (EMinusOne f2)
    108 
    109   -- The following code should need no modification
    110   -- Read at your own peril
    111   -- The use of "traverse" allows us to not write
    112   --   code for trivial case, see also subst below
    113
    114   fresh_ :: Exp -> String
    115   fresh_ (EVar (Id i)) = i ++ "0"
    116   fresh_ (EApp e1 e2) = fresh_ e1 ++ fresh_ e2
    117   fresh_ (EAbs (Id i) e) = i ++ fresh_ e
    118   fresh_ _ = "0"
    119
    120   fresh = Id . fresh_
    121
    122   subst :: Id -> Exp -> Exp -> Exp			  
    123   subst id s (EVar id') | id == id' = s
    124                         | otherwise = EVar id'
    125   subst id s (EApp e1 e2) = EApp (subst id s e1) (subst id s e2)
    126   subst id s e@(EAbs id' e') = 
    127   -- to avoid variable capture, we first substitute id' with a fresh name inside the body
    128   -- of the λ-abstraction, obtaining e''. 
    129   -- Only then do we proceed to apply substitution of the original s for id in the 
    130   -- body e''.
    131   let f = fresh e 
    132       e'' = subst id' (EVar f) e' in 
    133       EAbs f $ subst id s e''
    134   subst id s (ENatS e) = ENatS (subst id s e) 
    135   subst id s ENat0 = ENat0
    137   subst id s (EIf f1 e3 e4) = EIf (bsubst id s f1) (subst id s e3) (subst id s e4) 
    138   subst id s (ELet i e1 e2) = subst id s (EApp (EAbs i e1) e2)
    139   subst id s (ERec i e1 e2) = subst id s (EApp (EAbs i e2) (EFix (EAbs i e1)))
    140   subst id s (EFix e) = EFix (subst id s e)
    141   subst id s (EMinusOne e) = EMinusOne (subst id s e)
    142   subst id s (EHd e) = EHd (subst id s e)
    143   subst id s (ETl e) = ETl (subst id s e)
    144   subst id s ENil = ENil
    145   subst id s (ECons e l) = ECons (subst id s e) (subst id s l)
    146
    147   bsubst :: Id -> Exp -> BExp -> BExp
    148   bsubst id t (BAnd f1 f2) = BAnd (bsubst id t f1) (bsubst id t f2)
    149   bsubst id t (BOr f1 f2) = BOr (bsubst id t f1) (bsubst id t f2)
    150   bsubst id t (BNot f1) = BNot (bsubst id t f1)
    151   bsubst id t (BG f1 f2) = BG (subst id t f1) (subst id t f2)
    152   bsubst id t (BL f1 f2) = BL (subst id t f1) (subst id t f2)
    153   bsubst id t (BGe f1 f2) = BGe (subst id t f1) (subst id t f2)
    154   bsubst id t (BLe f1 f2) = BLe (subst id t f1) (subst id t f2)
    155   bsubst id t (BEquals f1 f2) = BEquals (subst id t f1) (subst id t f2)
    </pre>
    
 - **Things we learned from by implementing our interpreter for BExp**
     * We discovered and learned that we needed to implement the bExp2Bool function (line 55-57) because we needed to typecast the bool type we created to Haskell bool type
     * After we were finished implementing our evalBool functions, we found out that we needed to separate evalCBN functions from evalBool functions. If evalCBN functions are not separated from evalBool functions then it would generate *multiple declaration of evalCBN...* or *multiple declaration of evalBool...* causing compiling errors
     * In addition, we had to go back to the first version of the interpreter provided by Assignment 2 Part 1. When we went back to the first verison of the interpreter, we created and implemented another substitution for BExp, bsubst. This would handle substitutions for BExp type within our evalCBN and evalBool funtions. As we were testing the bsubst, we did encounter this compiling error message *"Couldn't match expected type 'BExp' with the actual type 'Exp'"*. and that helped when we were modifying the EIf. Here is an example of changes we made before and after for the and EIf function andbsubst :: Id. <br>
          * EIf
            <pre>
            Before: subst id s (EIf f1 e3 e4) = EIf (subst id s f1) (subst id s e3) (subst id s e4) 
            After: subst id s (EIf f1 e3 e4) = EIf (bsubst id s f1) (subst id s e3) (subst id s e4) 
            </pre>
            * We had to change *subst id s f1* to *bsubst id s f1* because we modified the parameter of the EIf function with the purpose to take in BExp to improve the functionality. The substitution for BExp is denoted as bsubst.
          * bsubst :: Id
            <pre>
            Before: bsubst :: Id -> BExp -> BExp -> BExp 
            After: bsubst :: Id -> Exp -> BExp -> BExp -> BExp
            </pre>
            * We had to change *Id -> BExp -> BExp -> BExp* to *Id Exp-> BExp -> BExp* because in the EIf function, BExp breaks down to two Exps being compared to by one of these ==, <=, <, >, >= operations and the boolean result of that is what BExp is. Therefore, we need to match the expected type to Exp -> BExp -> BExp.
 
     
           
