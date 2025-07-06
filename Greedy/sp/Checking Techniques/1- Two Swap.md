How to know if it is correct ?

-> Try to prove it false -> if you fail to do so -> it means your original argument is correct 


If this is correct sum1 = a1*b1 + a2*b2 + a3*b3 + a4*b4 + a5*b5 
                                    = g + a2*b2 + a4*b4 

Attack argument :- It will be best only if you swap (a2,a4) 


Sum 2 = a1*b1 + a4*b2 + a3*b3 + a2*b4 + a5*b5  = g + a4*b2 + a2*b4


If sum1<=sum2 ; it means even doin 1 swap will destroy your minimum answer hence proved your original argument is correct 

=> d = sum2 - sum1 if it >=0 then your original argument is correct 

-> d = (a4-a2)*(b2-b4) >=0 
