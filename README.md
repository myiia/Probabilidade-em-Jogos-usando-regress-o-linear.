# Probabilidade-em-Jogos-usando-regress-o-linear.
Probability starting from a csv database where there are columns named from 2005 to 2023, the probability will be that of a time with and the score will be in a certain position.

import pandas as pd
import numpy as np


#df = pd.read_csv(".csv") dataset
df = to_csv

position = int(input("enter the desired position: "))
score= int(input("enter current score: "))


lista = []
for element in df.iloc[position]:
    lista.append(element)


x = np.array([i for i in range(1, 20)]) #x mean the years, a interval between 2005 and 2023


y = np.array(lista)


def regressao(X,Y): #X and Y are independent variables, x means the years and y the score
    n = len(X)
    sx = sum(X)
    sy = sum(Y)
    sx2 = sum(X**2)
    sxy = sum(X*Y)
    a0 = (sx2*sy - sxy*sx) / (n*sx2 - sx**2)
    a1 = (n*sxy - sx*sy) / (n*sx2 - sx**2)
    return a0, a1

a0, a1 = regressao(x, y)


def P(X, score, x, y, a0, a1):
    z = a0 + a1 * x
    D = y - z
    E = D**2
    V = sum(D**2) / len(x)
    DP = V**(0.5)
    zano = a0 + a1 * X
    P = (score - zano + 2 * DP) / (2 * DP)
    return P
result = P((len(x)+1), score, x, y, a0, a1)
print("The probability of the team with the score {} being in the desired position is: {}".format(score, result))
