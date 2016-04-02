Intégrateur du premier ordre

# -*- coding: cp1252 -*-
import re
import math
from scipy import *
from pylab import *
import numpy
import numpy as np
from matplotlib.pyplot import *
import time
'''Tracés de la tension aux bornes d'un condensateur soumis à une tension rectangulaire
symétrique pour différentes valeurs de la constante de temps tau=RC'''
tab = []
tab1 = []
tab2 = []
tab3 = []
tab4 = []
tab5 = []
tab6 = []
tau = 0.05
tau2 = 0.25
tau3 = 0.5
tau4 = 2.5
d = 0.5
n = 10
global t, signal, U0, U1

N = 500
t = np.linspace(0,5, N)
dt = 5.0/500.0
for k in range(N):
    
    signal = math.sin(2*math.pi*k*dt)
    
    tab6.append(t)
    tab.append(signal)
       
for i in range(len(tab)):
    t[i]=i*dt
    if (tab[i]<0.0):
        z = -2
    if (tab[i]==0):
        z = 0
    if (tab[i]>0):
        z = +2
    tab1.append(z)

    if (t[i]<=0.5):
        s= 2*(1-exp(-i*dt/tau))
        tab2.append(s)
    if (t[i]<=0.5):
        s2= 2*(1-exp(-i*dt/tau2))
        tab3.append(s2)
    if (t[i]<=0.5):
        s3= 2*(1-exp(-i*dt/tau3))
        tab4.append(s3)
    if (t[i]<=0.5):
        s4= 2*(1-exp(-i*dt/tau4))
        tab5.append(s4) 
        
U0 = tab2[49]
U1 = tab3[49]
U2 = tab4[49]
U3 = tab5[49]

for j in range(n):
    
    for i in range(len(tab)):
        
        if (t[i]>0.5+0.5*j and t[i]<=1.0+0.5*j):
            
            U0 = tab2[49+50*j]
            print U0
            if (U0>0.0):
                s= -2*(1-exp(-(i*dt-(j+1)*d)/tau))+U0*exp(-(i*dt-(j+1)*d)/tau)
            if (U0<0.0):
                s= 2*(1-exp(-(i*dt-(j+1)*d)/tau))+U0*exp(-(i*dt-(j+1)*d)/tau)
            
            tab2.append(s)

for j in range(n):
    
    for i in range(len(tab)):
        
        if (t[i]>0.5+0.5*j and t[i]<=1.0+0.5*j):
            
            U1 = tab3[49+50*j]
            if (U1>0.0):
                s2= -2*(1-exp(-(i*dt-(j+1)*d)/tau2))+U1*exp(-(i*dt-(j+1)*d)/tau2)
            if (U1<0.0):
                s2= 2*(1-exp(-(i*dt-(j+1)*d)/tau2))+U1*exp(-(i*dt-(j+1)*d)/tau2)
            
            tab3.append(s2)


for j in range(n):
    
    for i in range(len(tab)):
        
        if (t[i]>0.5+0.5*j and t[i]<=1.0+0.5*j):
            
            U2 = tab4[49+50*j]
            if (U2>0.0):
                s3= -2*(1-exp(-(i*dt-(j+1)*d)/tau3))+U2*exp(-(i*dt-(j+1)*d)/tau3)
            if (U2<0.0):
                s3= 2*(1-exp(-(i*dt-(j+1)*d)/tau3))+U2*exp(-(i*dt-(j+1)*d)/tau3)
            
            tab4.append(s3)

for j in range(n):
    
    for i in range(len(tab)):
        
        if (t[i]>0.5+0.5*j and t[i]<=1.0+0.5*j):
            
            U3 = tab5[49+50*j]
            if (U3>0.0):
                s4= -2*(1-exp(-(i*dt-(j+1)*d)/tau4))+U3*exp(-(i*dt-(j+1)*d)/tau4)
            if (U3<0.0):
                s4= 2*(1-exp(-(i*dt-(j+1)*d)/tau4))+U3*exp(-(i*dt-(j+1)*d)/tau4)
            
            tab5.append(s4)

e = tab1
u1 = tab2
u2 = tab3
u3 = tab4
u4 = tab5

plot(t,e,'r', linewidth=1)
plot(t,u1, 'b-',label=ur"$\tau = T/20$", linewidth=1)
plot(t,u2, 'g--',label=ur"$\tau = T/4$", linewidth=2)
plot(t,u3, 'y--',label=ur"$\tau = T/2$", linewidth=2)
plot(t,u4, 'm--',label=ur"$\tau = 2.5\ T$", linewidth=2)
xlabel('t')
ylabel(ur"$u\ (avec\ E= \pm 2)$")
axis([0,3,-3,5])
grid()

legend()
show()
