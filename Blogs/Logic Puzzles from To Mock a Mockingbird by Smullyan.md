# Logic Puzzles from To Mock a Mockingbird by Raymond M. Smullyan
## How Do You Win Your Prize

**To Mock a Mockingbird** by Raymond M. Smullyan is one of his many books of logic puzzles. I am very interested in brainteasers and riddles like this, so I decided to try some of his puzzles.

### __The Prize and other Puzzles__
 
                  4 • The Three Prizes
       Suppose I offer to give you one of three prizes — Prize A, Prize
    B, or Prize C. Prize A is the best of the three, Prize B is
    middling, and Prize C is the *booby prize*. You are to make a
    statement; if the statement is true, then I promise to award
    you either Prize A or Prize B, but if your statement is false,
    then you get Prize C — the booby prize.
       Of course it is easy for you to be sure to win either Prize
    A or Prize B; all you need say is: "Two plus two is four." But
    suppose you have your heart set on Prize A — what statement
    could you make which would force me to give you Prize A?

The easiest statement to start with is one that tries to predict the future, "I will get prize ...", which can be either true or false.
Let's make a truth table.



If we say "I will get prize A" or "I will get prize B", there is no garuntee we will get a particular prize, there is both the chance the statement is true and the state ment is false. 
However, if we say "I will get prize C", the statement can be neither true or false. If the statement is true, we should get prize A or B, which makes the statement false. If the statement is false, we should get prize C, which makes the statement true. 

This circular reasoning is interesting to us, because with more constraints it could isolate Prize A for us. So let's add another prize to the statement, like "I will get prize C AND/OR ..." 



AND statements will always be false because you can only receive one prize, but with OR statements, we can box in Prize A and garuntee the best prize.


                 5 • A Fourth Prize Is Added
       I now add a fourth prize-Prize D. This prize is also a booby
    prize. The conditions now are that if you make a true statement,
    I promise to give you either Prize A or Prize B, but if
    you make a false statement, you get one of the two booby
    prizes-Prize C or Prize D.
       Suppose you happen to know in advance what the four
    prizes are, and for some reason or other, you like Prize C better
    than any of the other prizes.
       Incidentally, this situation is not necessarily unrealistic. I
    recall that as a child I was at a birthday party where I won a
    prize, but became very envious of the kid who won the booby
    prize, because I liked his prize much more than mine! In fact,
    the booby prize seemed to be a general favorite, since we all
    spent most of the day playing with it.
       Getting back to the present puzzle, what statement could
    you make that would force me to give you Prize C?

Another simple truth table makes this clear. 


Saying "I will get prize A/B" can easily be false if you're given C or D. However if you say "I will get prize C", the statement can never be true, because a true statement gives you prizes A or B, making the statement false again. Since the statement can never be true, you can only recieve prize D. The same goes for "I will get prize D", and you will end up with prize C.


                       6 • You Wish to Confound Me!
          Again, we have the four prizes of the last problem and the
        same conditions. Now, suppose you don't give a hoot for any'
        of the prizes; you merely wish to confound me by making a
        statement that will force me to break my promise.
          What statement would do this?
        Note: This problem is essentially the same as the one known
        as the Sancho Panza paradox, a discussion of which is included
        in the solution.

The truth table from the last question gives us a starting point, but where do we go from there? Like the first question, we need to add more constriants. Specifically, we are looking to create a statment that becomes false when given A or B, and becomes true when given C or D. So let's combine some prizes and look for a pattern.

Starting with A and combining it with every other prize, one row stands out. "A OR B" can get you any of the four prizes. We're looking for the opposite of that, so let's try the opposite letters.



"C OR D" cannot be true or false. If it is true, then you get prize A or B, making the statement false. If the statement is false, you get prize C or D, making the statement true. You cannot get any prize without breaking the rules.

