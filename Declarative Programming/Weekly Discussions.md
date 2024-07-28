
>[!example] Question 1
>```prolog
>?- enrolled(Student, comp90048) , X \= alex.
>```


>[!example] Question 2
>```prolog
>siblings(Sib1, Sib2) :- parent(_P, Sib1) , parent(_P, Sib2) , Sib1 \= Sib2.
>```


>[!example] Question 3
>```prolog
>?- enrolled(Student, comp90048) , student /= kai.
>```


