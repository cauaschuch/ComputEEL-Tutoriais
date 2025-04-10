---
title: "Arquivo de entrada"
layout: default
permalink: /tutoriais/tutorial1/
---

# 1. Como estruturar as coordenadas atômicas e a célula do seu composto  
OBS: Existem 230 grupos espaciais: point group + translational simmetry


# A: Célula cúbica  
Ac2CdGe (225)  
4a	Ge	0	0	0  
4b	Cd	1/2	0	0  
8c	Ac	1/4	3/4	3/4  

Indo ao site Bilbao Crystallographic Server / WYCKPOS / num (225) para conseguir as posicoes equivalentes:  
```txt
(0,0,0) + (0,1/2,1/2) + (1/2,0,1/2) + (1/2,1/2,0) 
4	a	m-3m  (0,0,0)  
4	b	m-3m  (1/2,1/2,1/2)  # aplicar a translação (1/2,1/2,1/2) + (0,1/2,1/2) == 1/2	0	0 que é as coordenadas que batem com os dados  
8	c	-43m   (1/4,1/4,1/4)	(1/4,1/4,3/4) #aplicar a translação  (0,1/2,1/2)+(1/4,1/4,1/4) == 1/4	3/4	3/4  
```

Em alat:  
0.0 0.0 0.0  
0.5 0.0 0.0  
0.25 0.75 0.75  
0.25 0.75 0.25  


os vetores pelo pw.x pra ibrav =  2  cubic F (fcc)  
v1 = (a/2)(-1,0,1),  v2 = (a/2)(0,1,1), v3 = (a/2)(-1,1,0) ou      
b = .5 * np.array([[-1, 0, 1], [0, 1, 1], [-1, 1, 0]])  # ibrav 2  


em alat: (a-lattice) The lattice parameter "alat" is set to alat = celldm(1)  
as posicoes em crystal, então (código no final da página para fazer a transformação):  

 0.00000000  0.00000000  0.00000000  
 0.50000000  0.50000000  0.50000000  
 0.75000000  0.75000000  0.75000000  
 0.25000000  0.25000000  0.25000000  

 como é cubico, celldm(1) = X Bohr  
 no Materialsp project a unidade é Angstrom  
 entao a=b=c=celldm(1) = 7.95 * 1.8897259886 = 15.023321609 Bohr  


 Célula primitiva do composto Ac2CdGe 

 
<img src="{{ '/assets/cubic.jpeg' | relative_url }}" alt="cubic" width="300">  


# B: Célula tetragonal


AcBrO (129)  
2a	O	0	0	0  
2c	Ac	0	1/2	0.83497  
2c	Br	1/2	0	0.634694  
Symbol P4/nmm  


nesse caso, temos mais de uma forma pra escrever as coordenadas:  
ITA number	Setting	P	P-1  
129	P 4/n m m [origin 2]	a,b,c	a,b,c  
129	C 4/e m m [origin 2]	a-b,a+b,c	1/2a+1/2b,-1/2a+1/2b,c  
129	C 4/e m m [origin 2]	a+b,-a+b,c	1/2a-1/2b,1/2a+1/2b,c  
129	P 4/n m m [origin 1]	a-1/4,b+1/4,c	a+1/4,b-1/4,c  # vamos ficar com esse aqui pois bate com o Symbol P4/nmm e coord do Materials project  
129	C 4/e m m [origin 1]	a-b-1/4,a+b+1/4,c	1/2a+1/2b+1/4,-1/2a+1/2b-1/4,c  
129	C 4/e m m [origin 1]	a+b-1/4,-a+b+1/4,c	1/2a-1/2b+1/4,1/2a+1/2b-1/4,c  


Então temos:  
```txt
2	a	-4m2	(0,0,0)	(1/2,1/2,0)  
2	c	4mm	    (1/2,0,z)	(0,1/2,-z)  
```


posicoes que ja estao em crystal:  
0.0 0.0 0.0  
0.5 0.5 0.0  
0.0 0.5 0.83497  
0.5 0.0 -0.83497  
0.5 0.0 0.634694  
0.0 0.5 -0.634694  


existem 2 ibravs para células tetragonais, mas como o nosso é P4/nmm ou primitive, vamos ficar com ibrav = 6  
  6          Tetragonal P (st)               celldm(3)=c/a  
      v1 = a(1,0,0),  v2 = a(0,1,0),  v3 = a(0,0,c/a)  

  7          Tetragonal I (bct)              celldm(3)=c/a  
      v1=(a/2)(1,-1,c/a),  v2=(a/2)(1,1,c/a),  v3=(a/2)(-1,-1,c/a)  


celldm(1) = a=b =4.31*1.8897259886 = 8.1447190108 bohr  
celldm(3) = c/a = 4.31/7.54 = 0.571618037# celldm(3) nao tem unidade, é uma proporção  


 Célula primitiva do composto AcBrO 

 
<img src="{{ '/assets/tetragonal.jpeg' | relative_url }}" alt="tetragonal" width="300">


# C: Célula hexagonal


AcBr3 (176)  
2c	Ac	2/3	1/3	3/4  
6h	Br	0.614413	0.699821	3/4  


```txt
2	c	-6..	(1/3,2/3,1/4)	(2/3,1/3,3/4)  
6	h	m..	(x,y,1/4)	(-y,x-y,1/4)	(-x+y,-x,1/4)	(-x,-y,3/4) (y,-x+y,3/4)	(x-y,x,3/4)
```


posicoes aqui já vao estar em termos dos vetores do cristal (crystal):  
obs: vamos usar x = -0.614413 e y = -0.699821 para encaixar em (-x,-y,3/4)!  


0.66666667 0.33333333 0.75  
0.33333333 0.66666667 0.25  
-0.614413  -0.699821   0.250000  
0.699821   0.085408   0.250000  
-0.085408   0.614413   0.250000  
0.614413   0.699821   0.750000  
-0.699821  -0.085408   0.750000  
0.085408  -0.614413   0.750000  


 4          Hexagonal and Trigonal P        celldm(3)=c/a  

a = b =  celldm(1) = 8.17 Å*1.8897259886 = 15.439061327   
c  = 4.72 Å*1.8897259886 = 8.9195066661 bohr  
celldm(3) = c/a = 0.577723378  


 Célula primitiva do composto AcBr3  
<img src="{{ '/assets/hexagonal.jpeg' | relative_url }}" alt="hexagonal" width="300">


# D: Célula triclínica  


AgPbF6 (2) - triclinico  
1a	Ag	0	0	0  
1g	Pb	0	1/2	1/2  
2i	F	0.857469	0.102946	0.261334  
2i	F	0.828452	0.244639	0.751039  
2i	F	0.542902	0.433166	0.271319  


```txt
1	a	-1	(0,0,0)  
1	g	-1	(0,1/2,1/2)  
2	i	1	(x,y,z)	(-x,-y,-z)
```


Assim temos, coordenadas (em crystal):
0.0 0.0 0.0  
0.0 0.5 0.5  
0.857469 0.102946 0.261334  
-0.857469 -0.102946 -0.261334  
0.828452 0.244639 0.751039  
-0.828452 -0.244639 -0.751039  
0.542902 0.433166 0.271319  
-0.542902 -0.433166 -0.271319  


temos 3 angulos diferentes e 3 comprimentos diferentes:  
a 5.17 Å  
b 5.21 Å  
c 5.77 Å  
α 89.12 º  
β 114.02 º  
ɣ 118.54 º  


entao:  
celldm(1) = 5.17*1.8897259886 = 9.769883361 bohr  
celldm(2) = 1.0077  
celldm(3) = 1.1160  
celldm(4) = -0.4190  
celldm(5) = -0.4750  
celldm(6) = 0.0150  
14          Triclinic                       celldm(2)= b/a,  
                                             celldm(3)= c/a,  
                                             celldm(4)= cos(bc),  
                                             celldm(5)= cos(ac),  
                                             celldm(6)= cos(ab)  
      v1 = (a, 0, 0),  
      v2 = (b*cos(gamma), b*sin(gamma), 0)  
      v3 = (c*cos(beta),  c*(cos(alpha)-cos(beta)cos(gamma))/sin(gamma),  
           c*sqrt( 1 + 2*cos(alpha)cos(beta)cos(gamma)  
                     - cos(alpha)^2-cos(beta)^2-cos(gamma)^2 )/sin(gamma) )  
      where alpha is the angle between axis b and c  
             beta is the angle between axis a and c  
            gamma is the angle between axis a and b  


  Célula primitiva do composto  AgPbF6            
 <img src="{{ '/assets/triclinic.jpeg' | relative_url }}" alt="triclinic" width="300">


# Apêndice: códigos e arquivos .in  
OBS: os arquivos .in estão incompletos e não vão rodar - é apenas para facilitar a visualização das células e coordenadas.


Código de mudança de base (cartesiana -> vetores do cristal)
```python
import numpy as np  
import numpy.linalg as la  

alat = np.genfromtxt('Ac2CdGe_alat')  

out = open('Ac2CdGe_crystal', 'w')  
b = .5 * np.array([[-1, 0, 1], [0, 1, 1], [-1, 1, 0]])  # ibrav 2  
M = b.T  
print(M)  
Minv = la.inv(M)  

crystal = np.zeros([len(alat), 3])  

for i in range(len(alat)):  
    crystal[i] = (Minv @ alat[i]) % 1  
    out.write(f'{crystal[i, 0]:11.8f} {crystal[i, 1]:11.8f} {crystal[i, 2]:11.8f}\n')  

out.close()  
```


Ac2CdGe.in
```txt
&CONTROL  
   calculation     = 'scf'  
/  
&SYSTEM  
   ibrav           = 2  
   celldm(1)       = 15.023321609  
   nat             = 4  
   ntyp            = 3  
/  
&ELECTRONS  
/  

ATOMIC_SPECIES  
Cd  157.25  Gd.pseudo  
Ge  140.12  Ce.pseudo  
Ac  227.03  Ac.pseudo  

ATOMIC_POSITIONS crystal  
Ge 0.00000000  0.00000000  0.00000000  
Cd 0.50000000  0.50000000  0.50000000  
Ac 0.75000000  0.75000000  0.75000000  
Ac 0.25000000  0.25000000  0.25000000  
  
K_POINTS automatic  
4 4 4 0 0 0  
```


AcBrO.in
```txt
&CONTROL  
   calculation     = 'scf'  
/  
&SYSTEM  
   ibrav           = 6  
   celldm(1)       = 8.1447190108  
   celldm(3)       = 1.749419953  
   nat             = 6  
   ntyp            = 3  
/  
&ELECTRONS  
/  

ATOMIC_SPECIES  
O    15.999    O.pseudo  
Br   79.904    Br.pseudo  
Ac   227.03    Ac.pseudo  

ATOMIC_POSITIONS crystal  
O   0.0 0.0 0.0  
O  0.5 0.5 0.0  
Ac  0.0 0.5 0.83497  
Ac  0.5 0.0 -0.83497  
Br  0.5 0.0 0.634694  
Br  0.0 0.5 -0.634694  

K_POINTS automatic  
4 4 4 0 0 0  
```



AcBr3.in
```txt
&CONTROL  
   calculation     = 'scf'  
/  
&SYSTEM  
   ibrav           = 4  
   celldm(1)       = 15.439061327  
   celldm(3) =       0.577723378  
   nat             = 8  
   ntyp            = 2  
/  
&ELECTRONS  
/  

ATOMIC_SPECIES  
Br  79.904 Br.pseudo  
Ac  227.03  Ac.pseudo  

ATOMIC_POSITIONS crystal  
Ac   0.66666667 0.33333333 0.75  
Ac   0.33333333 0.66666667 0.25  
Br   -0.614413  -0.699821   0.250000  
Br   0.699821   0.085408   0.250000  
Br   -0.085408   0.614413   0.250000  
Br   0.614413   0.699821   0.750000  
Br   -0.699821  -0.085408   0.750000  
Br   0.085408  -0.614413   0.750000  

K_POINTS automatic  
4 4 4 0 0 0  
```


AgPbF6.in
```txt
&CONTROL  
   calculation     = 'scf'  
/  
&SYSTEM  
   ibrav           = 14  
    celldm(1) = 9.769883361   
    celldm(2) = 1.0077  
    celldm(3) = 1.1160  
    celldm(4) = -0.4190  
    celldm(5) = -0.4750  
    celldm(6) = 0.0150  
   nat             = 8  
   ntyp            = 3  
/  
&ELECTRONS  
/  

ATOMIC_SPECIES  
Ag   107.8682   Ag.pseudo  
Pb   207.2      Pb.pseudo  
F    18.998403  F.pseudo  

ATOMIC_POSITIONS crystal  
Ag 0.0 0.0 0.0  
Pb 0.0 0.5 0.5  
F 0.857469 0.102946 0.261334  
F -0.857469 -0.102946 -0.261334  
F 0.828452 0.244639 0.751039  
F -0.828452 -0.244639 -0.751039  
F 0.542902 0.433166 0.271319  
F -0.542902 -0.433166 -0.271319  

K_POINTS automatic  
4 4 4 0 0 0  
```


# 2. Relaxando a estrutura: exemplo com célula triclínica CsHg



