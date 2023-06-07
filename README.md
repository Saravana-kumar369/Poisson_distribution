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

L = list(map(int, input().split()))
M = max(L)
X = list(range(M + 1))
f = [L.count(i) for i in X]
sf = sum(f)
p = [count / sf for count in f]
mean = np.inner(X, p)

p = [math.exp(-mean) * mean**x / math.factorial(x) for x in X]
E = [px * sf for px in p]
xi = [(fx - ex)**2 / ex for fx, ex in zip(f, E)]

print("X P(X=x) Obs.Fr Exp.Fr xi")
print("--------------------------")
for x, px, fx, ex, xi_value in zip(X, p, f, E, xi):
    print("%2d %.3f %4d %.2f %.2f" % (x, px, fx, ex, xi_value))
print("--------------------------")

cal_chi2_sq = sum(xi)
table_chi2 = scipy.stats.chi2.ppf(1 - 0.01, df=M)

print("Calculated value of Chi square is %.2f" % cal_chi2_sq)
print("Table value of chi square at 1 level is %.2f" % table_chi2)

if cal_chi2_sq < table_chi2:
    print("The given data can be fitted in the Poisson Distribution at 1% LOS")
else:
    print("The given data cannot be fitted in the Poisson Distribution at 1% LOS")
```
# Output : 
![Screenshot 2023-06-07 103625](https://github.com/Saravana-kumar369/Poisson_distribution/assets/117925254/08df66b9-ca08-44f4-8eb7-13fcdd2de66b)


# Results

The Poisson distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 
 
