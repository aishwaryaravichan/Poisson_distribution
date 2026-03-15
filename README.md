# Fitting Poisson  distribution
# Aim : 

To fit poisson distribution for the arrival of objects per minute from the feeder

# Software required :  

Python and Visual component tool

# Theory:

The Poisson distribution is the discrete probability distribution of the number of events occurring in a given time period, given the average number of times the event occurs over that time period.

![image](https://user-images.githubusercontent.com/104613195/166248326-fd042076-8b0b-40c4-8b11-1d8e8fcb74db.png)

 Conditions for Poisson Distribution:

1. An event can occur any number of times during a time period.
2. Events occur independently. I
3. The rate of occurrence is constant.
4. The probability of an event occurring is proportional to the length of the time period. 
 
# Procedure :

![image](https://user-images.githubusercontent.com/104613195/166251988-d0c53205-6080-4f7b-ae4c-398178586637.png)

# Experiment :

![image](https://user-images.githubusercontent.com/103921593/230282876-f4a5afbf-cac1-4648-a1b0-c78840638a8e.png)

# Program :
```
import numpy as np

import math

import scipy.stats


L = [int(i) for i in input().split()]

N = len(L)

M = max(L)

X = []

f = []


for i in range(M + 1):

    c = 0
    
    for j in range(N):
    
        if L[j] == i:
        
            c = c + 1
    
    f.append(c)
    
    X.append(i)


sf = np.sum(f)

p_observed = []


for i in range(M + 1):

    p_observed.append(f[i] / sf)


mean = np.inner(X, p_observed)


p = []

E = []

xi = []


print("X   P(X=x)   Obs.Fr   Exp.Fr   xi")

print("--------------------------")


for x in range(M + 1):

    p.append(math.exp(-mean) * mean**x / math.factorial(x))
    
    E.append(p[x] * sf)
    
    xi.append((f[x] - E[x])**2 / E[x])
    
    print("%2.2f %2.3f %4.2f %3.2f %3.2f" % (x, p[x], f[x], E[x], xi[x]))


print("-------------------")


cal_chi2_sq = np.sum(xi)

print("Calculated value of chi square is %4.2f" % cal_chi2_sq)


table_chi2 = scipy.stats.chi2.ppf(1 - .01, df=M)

print("Table value of chi square at 1 level is %4.2f" % table_chi2)


if cal_chi2_sq < table_chi2:
    
    print("The given data can be fitted in poisson distribution at 1% LOS")

else:
    
    print("The given data cannot be fitted in poisson distribution at 1% LOS")
``` 

# Output : 
```
https://private-user-images.githubusercontent.com/227108188/557398715-8e65d9f8-74a0-49cd-8c45-530d6a5490cc.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NzM1ODIzNjUsIm5iZiI6MTc3MzU4MjA2NSwicGF0aCI6Ii8yMjcxMDgxODgvNTU3Mzk4NzE1LThlNjVkOWY4LTc0YTAtNDljZC04YzQ1LTUzMGQ2YTU0OTBjYy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYwMzE1JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MDMxNVQxMzQxMDVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT01Y2MxYWFlYjFhNDlkZjk4MTBjY2MxYTY1MDQxMDRiYTY1YWFkZGYzOTQxNGZmODUzOTZmMzI1NGNlNDFmMjVkJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.WR6lgd0C-Tz14WkDBDviDHvBHGQoAZsDcywy4XDf7ds
```

# Results

The Poisson distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 
 
