# BExp: bMergeSort.lc

let rec makeLists = \ x . if x = # then # else (((hd x): #) : (makeLists (tl x))) in <br>
let rec merge = \ x . \ y . if x=# then y else if y=# then x else if ((hd x) <= (hd y)) then ((hd y) :(merge x (tl y))) else ((hd x) :(merge (tl x) y)) in <br>
let rec bMergeSort = \x. if x=# then # else (merge (hd (makeLists x)) (bMergeSort(tl(x)))) in <br>

-- Testing 
//bMergeSort (#) //Answer: # <br>
//bMergeSort (0: #) //Answer: 0 : #  <br>
//bMergeSort (S S 0: S 0: 0:#) //Answer: 0 : S 0 : S S 0 : #  <br>
//bMergeSort (S S S S 0:S S S S S S S 0: #) //Answer: S S S S 0 : S S S S S S S 0 : #  <br>
bMergeSort (S S S 0:0 :S 0:S S 0: #) //Answer: 0 : S 0 : S S 0 : S S S 0 : #  <br>
//bMergeSort (S S S S 0:S S S 0:S S 0:S 0: 0: #) //Answer: 0 : S 0 : S S 0 : S S S 0 : S S S S 0 : #  <br>
