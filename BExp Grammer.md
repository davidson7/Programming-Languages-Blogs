# BExp: Grammar
For the extra credit, we added boolean features to LambdaNat. In the grammar, we added a boolean expression BExp. In addition, included *and*, *or*, *not* as well as ==, <=, <, >, >= operations. <br>
   
   * LambdaNat6.cf
     <pre>
     Prog.      Program ::= Exp ;
     EAbs.      Exp1 ::= "\\" Id "." Exp ; 
    
     --and, or, not operations
     BAnd.      BExp2 ::= BExp "and" BExp ;
     BNot.      BExp2 ::= "not" BExp ;
     BOr.       BExp2 ::= BExp "or" BExp ;
    
     -- Modified if statement using BExp
     EIf.       Exp2 ::= "if" BExp "then" Exp "else" Exp ; 
     ELet.      Exp3 ::= "let" Id "=" Exp "in" Exp ;  
     ERec.      Exp4 ::= "let rec" Id "=" Exp "in" Exp ;
     EHd.       Exp6 ::= "hd" Exp ;
     ETl.       Exp6 ::= "tl" Exp ;
     EMinusOne. Exp7 ::= "minus_one" Exp ;
    
     -- ==, <=, <, >, >= operations
     BEquals.   BExp7 ::= Exp "=" Exp ;
     BGe.       BExp7 ::= Exp ">=" Exp ;
     BLe.       BExp7 ::= Exp "<=" Exp ;
     BG.        BExp7 ::= Exp ">" Exp ;
     BL.        BExp7 ::= Exp "<" Exp ;
    
     EApp.      Exp8 ::= Exp8 Exp9 ;  
     ENil.      Exp9 ::= "#" ; -- EndOfList, aka empty list
     ECons.     Exp9 ::= Exp10 ":" Exp9 ;
     ENat0.     Exp10 ::= "0" ; 
     ENatS.     Exp10 ::= "S" Exp10 ; 
     BTrue.	   BExp10 ::= "true";
     BFalse.	   BExp10 ::= "false";
     EVar.      Exp11 ::= Id ;
    
     internal   EFix.      Exp5 ::= "fix" Exp ;  -- only for abstract syntax
    
     coercions BExp 10;
     coercions Exp 11 ;
    
     token Id (letter (letter | digit | '_')*) ;
    
     comment "//" ;
     comment "/*" "*/" ;
     </pre>
  
 * **Things we learned by implementing the grammar for BExp** <br>
      * When we started implementing ==, <=, <, >, >= operations in the grammar, we did not know if we could combine Exp and BExp types together. With research, we discovered and learned that Exp and BExp can be utilize together and after built the 
==, <=, <, >, >= operations code. Here are the two example of changes that we made before and after our research. The first example is the BL "less than" function and the second example is the EIf "if statement" function: <br>
         * BL function <br>
           <pre>
           Before: *BExp7 ::= BExp "<" BExp*
           After: *BExp7 ::= Exp "<" Exp*
           </pre>
            * In the before BL function, we implemented it by taking in two BExps, however, this grammar is incorrect because booleans (which are defined as true or false) can not be compared using <=, <, >, >= operations <br>
            * In the after BL function, we implemented it by taking in two Exps, this grammar is correct because Exp can hold different numerical values which can be compared using operations like ==, <=, <, >, >= to produce a boolean outcome. <br>
         * EIf function <br>
           <pre>
           Before: *Exp2 ::= "if" Exp "=" Exp "then" Exp "else" Exp*, 
           After: *Exp2 ::= "if" BExp "then" Exp "else" Exp* 
           </pre>
            * In the before EIf function, it was only allowed to compare if the Exps were equal to eachother. 
            * In the after EIf function, by modifying the code to BExp it improves the functionality of the if statement. It makes it versatile and flexible by allowing it to use other operations such as =, <=, <, >, >=.
         
         

         
         
         
