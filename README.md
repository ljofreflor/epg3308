epg3308 <img src="http://www.labmat.puc.cl/themes/labmat/imagenes/facultad_logo.png" align="right" />
====================


Biblioteca de estadistica descriptiva en R

## Instalación
```s
# install.packages("devtools")
devtools::install_github("ljofre/epg3308")
```

## Uso de la libreria

Datos de prueba

```s
>library(describeNsimulate)

>data("albahaca")

>head(albahaca)


  produccion  temp alt n.riegos hum sexo marca cuidado
1      46.44 14.93 590        9   2    0     3       1
2      27.77 13.05 586        5   2    0     2       1
3      47.02 18.86 939       12   1    1     1       1
4      32.38 14.32 833        8   3    1     2       2
5      30.40 13.34 819        7   1    0     1       1
6      27.24 12.95 604        4   3    1     3       1
```

funciones básicas de estadistica descriptiva

```s
# Coeficiente de Asimetria de Fisher 

> asimetria.fisher(albahaca$produccion,'SI')
[1] "Asimetria Negativa"
[1] -0.1934995

#Curtosis
> curtosis(albahaca$produccion,'SI')
[1] "Distribucion Platicurtica"
[1] 2.251493

#Cuartiles            *******
> cuartiles(albahaca$produccion)
   Cuartiles
Q1     29.26
Q2     38.97
Q3     46.45

#Correlacion de Pearson   *********
> corr.pearson(albahaca,"n.riegos","produccion")
[1] 0.7930546
[1] "Asosiacion Lineal Positiva"


#Matriz Correlaciones Pearson
> corr.matrix.pearson(albahaca)
           produccion      temp        alt  n.riegos
produccion  1.0000000 0.3567275 -0.3984812 0.7930546
temp        0.3567275 1.0000000  0.1889965 0.2377609
alt        -0.3984812 0.1889965  1.0000000 0.1408494
n.riegos    0.7930546 0.2377609  0.1408494 1.0000000

#Matriz Correlaciones Spearman
> corr.matrix.spearman(albahaca)
           produccion      temp       alt  n.riegos
produccion  1.0000000 0.8631957 0.8190119 0.8575672
temp        0.8631957 1.0000000 0.8468730 0.7956535
alt         0.8190119 0.8468730 1.0000000 0.7920263
n.riegos    0.8575672 0.7956535 0.7920263 1.0000000

#Covarianza
> covarianza(albahaca$produccion,albahaca$temp)
[1] 10.11587

#Coeficiente Variacion
> coeficiente.variacion(albahaca$produccion)
[1] 0.2882387

#Promedio
> promedio(albahaca$produccion)
[1] 37.5985

#Suma
> suma(albahaca$produccion)
[1] 1503.94
```

## Resumenes Descriptivos

### Categoricas

```s
descriptive.categorical(albahaca)
[1] "hum"
  hum  n proporcion   odds error std
1   1  7      0.175 0.2121    0.0601
2   2 15      0.375 0.6000    0.0765
3   3 18      0.450 0.8182    0.0787
[1] "sexo"
  sexo  n proporcion   odds error std
1    0 19      0.475 0.9048     0.079
2    1 21      0.525 1.1053     0.079
[1] "marca"
  marca  n proporcion   odds error std
1     1 12        0.3 0.4286    0.0725
2     2 16        0.4 0.6667    0.0775
3     3 12        0.3 0.4286    0.0725
[1] "cuidado"
  cuidado  n proporcion odds error std
1       1 20        0.5    1    0.0791
2       2 20        0.5    1    0.0791
```

### Numéricas

```s
> descriptive.continue(albahaca)
            n promedio     suma     std    CV asimetria curtosis minimo maximo     Q1     Q2
produccion 40   37.598  1503.94  10.837 0.288    -0.193    2.251  12.94  60.31  35.67  39.31
temp       40   16.466   658.64   2.617 0.159    -0.018    1.727  12.07  20.92  18.65  18.20
alt        40  790.375 31615.00 158.639 0.201    -0.185    1.426 502.00 988.00 779.00 974.00
n.riegos   40    7.500   300.00   2.253 0.300     0.131    1.948   4.00  12.00   6.50   9.00
               Q3
produccion  35.67
temp        18.65
alt        779.00
n.riegos     6.50
```

### Generación de variables aleatorias

```s
#Simulacion Variable Aleatoria Bernulli
> sim.bernulli(100,0.4)
  [1] 0 0 0 1 0 1 0 1 0 1 0 0 0 1 0 0 0 0 0 0 1 0 1 0 0 0 1 1 1 1 1 0 1 1 1 0 1 1 0 1 0 0 1 1 1 0
 [47] 0 0 1 0 1 1 1 1 1 0 1 1 1 0 0 1 0 1 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 1 0 1 0 0 0 1 0 0 1 0 0 1
 [93] 1 0 0 1 1 1 1 0
[1] "Porcentaje de unos"
[1] 0.45
[1] "Porcentaje de ceros"
[1] 0.55


#Simulacion Variable Aleatoria Binomial

> sim.binomial(100,30,0.4)                               
  [1] 16 16 11 13 14 11  8 13 12 12 13 12 11 11 14 11 10 11 10  9 15 14 10 18 16 18 13  9 10 13 13
 [32] 12 14 11 11 13 13 13 10 10 12 16 14 10  9 18 11 11  6 16 13 11  8  7  8  8 16 14 14 11 13 16
 [63] 12 11 13  9 14 13 12 15 13 11 12 11 13 11  9 14 11  6 15  7  9  9 13 12 12 11 18 12 13 11 16
 [94] 18 15 15  9 10 13 11

#Simulacion Variable Aleatoria Exponencial                
> sim.exponencial(100,7)                              
[1] "Datos generados"
  [1] 15.4324292  1.2769402 15.4433196  2.1640642  3.8189583  1.5256075  9.1251705  6.6026517
  [9]  7.9725288  1.7822154  4.3544797  0.1876629  7.9384326  5.5563637 17.3626629  4.5010474
 [17]  0.8047338  1.9163189  2.0870716  4.8703891  5.3728843  0.9691185 13.2630116  2.2297282
 [25]  1.2678847 19.7409516  3.5037086 11.5733687  6.1511497 10.7581658  0.5721064  1.5974501
 [33]  4.3027675 18.6710193  3.1457651  1.1578702 11.1287757  0.6880114 52.2844298  0.3066399
 [41]  0.1721700  8.9232180  0.9650566  8.1402058  3.9502570  4.5482969  0.1992635  0.5191902
 [49]  2.2159593  8.3779794 13.8463694  2.7443387 10.5041474 13.0338497  0.5867305  4.8797644
 [57]  6.7521178  6.9591053  1.3149369  2.5724079  4.6739811  5.7231091  3.0620808 10.6264473
 [65]  2.7166708  7.9099602  0.9176003  3.5792940  3.6920771  0.9274179  4.5079135  3.5476202
 [73] 26.0471526  2.7161325  3.0995804  2.1983706 14.7653598  7.5426262 10.5156434  1.2381734
 [81] 15.5187006  7.1937368  1.3900071 15.1256305 18.6899617  3.6014590  4.0216523  6.2863216
 [89] 17.9072232  0.2829696  2.6308445  6.9573257  3.5342838  1.4393879  3.0780518 15.7667351
 [97] 13.7706194  0.3386954  3.5021862  9.6589314

#Simulacion Variable Aleatoria Geometrica                
> sim.geometrica(100,0.5)
  [1] 1 8 0 9 2 1 1 3 2 0 1 0 1 1 0 1 1 4 0 3 2 2 1 2 2 1 2 3 1 2 2 1 1 8 2 0 3 5 1 0 0 1 1 1 1 0
 [47] 1 0 0 0 3 0 2 0 3 2 2 1 4 2 3 0 2 1 3 0 0 0 0 3 2 2 2 3 0 2 0 0 0 2 1 0 1 0 1 2 0 1 4 1 1 1
 [93] 5 1 3 1 0 6 0 1

#Simulacion Variable Aleatoria Hipergeometrica         
> sim.hipergeometrica(200,100,40,20)
  [1] 10 11  7  8 10  8  7  8 11  8  9 10  8  7  8  3  7  5 10  8  9  9  9  7 10  9 11 10  7  8  9
 [32]  9  7  8  9  6  5  7  8 10  7  8 10  7  6  6  9  9 10  9  6  7  8  7 10  7  9  7  9  8  6  6
 [63]  6  6 10  9  9  7  8  5  7  8  9 10  6  9  8  8 14  7  8  3 10 10  5  8 10 10 11  9  8  7  9
 [94]  6  8  6 10 11  9  9  7  9 11 12 11  8  5 13  6  8  7  8 10 12  8  9  9  7  8 10  7  9  8  7
[125]  9  8  7  9  5  6 11  7  7  9  7  7  6  7  8 10  7  8  6  5 10  6  5  6 11  8  8  9  8  3 12
[156]  8  9  5 10  8  9  9 10  8  7  7  9  7  7 11 10  7  5  6  8 10  8  2  8  8  8 10  7  9 11 10
[187]  9  6 10  8 10  9  7 10  6  4  8  8  9 12

#Simulacion Variable Aleatoria Poisson                
> sim.poisson(100,5)
  [1]  6  7  6 10  8  5  5  3 11  4  3  1  2  6  5  1  5  6  4  6  4  7  6  3  9  5  5  5  8  7  5
 [32]  2  7  8  6  3  3  6  5  3  5  5  3  5  5  6  2  3  1  4  5  7  5  2  3  4  5  2  8  4  3  1
 [63]  4  6  7  2  5  4  3  4  3  7 12  8  4  6  9  7  3  6  2  5 10  4  9  4  3  6  4  8  6  4  6
 [94]  5  9  5  4  4  8  4

#Simulacion Variable Aleatoria Normal via Box Muller      
> snormalBM(100)
[1] "valores generados de X"
  [1] -0.836680742 -0.057401114 -0.573398843  0.754762023 -0.437261617 -0.332083749  1.108383459
  [8]  0.761701086  0.826051646 -0.078175210 -0.004688785 -0.991902188  0.082037217  0.860070269
 [15]  0.853915365  1.483900844 -0.954793213 -1.312202719  0.737118418 -0.022660825 -0.644149454
 [22]  0.058513309 -0.567826007 -1.005787672  1.181535114  0.965047970  0.636055737 -1.009742526
 [29]  0.232625429  0.024014519 -0.092416763 -0.943287560  1.107459240  2.389261797  0.585759384
 [36]  1.290600564 -1.775293517  1.188939781  0.930782380 -0.538232601  1.694010767 -0.256229014
 [43]  0.539710912 -1.135554615 -1.678045427  0.030367331 -1.213657927  0.495888380 -0.248574755
 [50]  0.045724561  1.345151416  2.369391584  0.200173414  0.693455138  0.938490863 -0.184914170
 [57]  0.785580907 -0.858951585 -0.013480310 -1.228316278 -1.312838998 -2.039302105 -1.002131898
 [64] -1.154906527 -0.276401421  1.130224441 -0.515162322 -0.553489687  0.328757876 -2.009848044
 [71]  0.281643788 -0.900026698  0.564469273  1.084654692 -0.381010853  1.922786193  0.146210714
 [78]  0.519156987 -0.646458512 -2.045164349 -0.238140910 -2.076021177  1.237339773  0.844925485
 [85] -0.336980523  0.226823193  1.769405570 -0.932427870 -0.316653085 -1.771556000 -1.228566173
 [92]  0.135906012  0.965531460 -0.663979508  1.826083452 -1.001738140 -0.900956689  1.629632064
 [99] -1.174615882  0.096175840
[1] "valores generados de Y"
  [1] -0.684181420  0.147229703 -0.741395388  0.432298263 -0.597438415 -0.213200849 -0.204589343
  [8]  0.094486457  0.230360746  1.430605941  1.857869827  0.004002011  2.250335311  1.321564671
 [15] -1.509705701 -1.391810500 -0.775684069  0.565501343 -0.049484857 -1.715369365  0.090989728
 [22]  0.438660643 -1.305793481  2.350202203  0.283278517 -1.089557438 -0.644937928  1.191640643
 [29] -0.514930868 -1.166183065  0.372592057 -0.372512301 -2.561631581  0.734849112  0.931334243
 [36] -0.803162855 -0.992289133  1.563152982  1.485643403 -1.187867032  0.051498137  0.550909476
 [43] -0.675419779  0.015924825 -1.760199776  0.727578348 -0.584647000 -1.181467653 -0.865116668
 [50]  2.043304827 -0.994207017 -1.398184680 -1.298812504  0.827355489  0.555169336  0.038656586
 [57]  2.094603381  0.100639918 -0.527041421 -1.878429249 -0.424218348 -1.884053392  2.185012587
 [64]  0.437357013  0.489122416 -0.027847923  0.434183779 -1.926523219 -0.050705939  0.277681132
 [71] -1.191116795  0.137938873  0.427321820  0.795417148  0.346833082  2.017914485 -0.688073429
 [78] -1.790153355  0.751542305  1.198578826 -0.437270254 -1.024026502  0.914007532  0.121125566
 [85]  1.307367713 -0.358811989 -1.629965345 -0.278873265 -0.443801248 -0.559606429  0.209004167
 [92] -0.951212553 -1.397645130 -0.164417876 -1.430280799 -0.635262638 -0.491931625 -1.872534374
 [99] -0.741437561  1.014920649


#Simulacion Variable Aleatoria Normal via Coordenadas Polares  
> snormalCP(100)
[1] "valores generados de X"
  [1] -1.42772745  1.48908537 -1.79767179 -0.35610168 -0.62741256  0.71544673  0.90265955
  [8] -0.23938884 -0.28017809 -1.56070046  1.28680721 -1.26686810  0.74903114 -0.80738161
 [15]  1.15218668  1.69231644  0.05639165 -0.57343673 -0.69412012  0.50155080  1.12770177
 [22] -0.47608132  0.27250207  1.41653828 -1.12170907 -0.70885888 -0.58677575  0.52870682
 [29] -0.72115323  1.49166229 -2.37221810 -0.27449933 -0.62082440 -1.85066055 -1.58060592
 [36] -0.30481972  0.56015185  0.47632508  1.48649276 -0.37082691 -0.49954040  0.81735501
 [43]  0.42878490 -1.09971084 -2.01224979  0.61624008  0.94615523 -0.09969550 -0.16090065
 [50]  0.20035323 -0.37553658  1.29156725  0.83667896  2.19127476 -0.63666543  0.45457235
 [57]  1.74345008 -1.13782822 -0.65264144 -1.72006628 -1.47404244  0.24198844 -0.24189256
 [64] -0.42060676  1.38467143  0.25089719 -0.09394457 -0.46665753 -1.84992812  0.33958232
 [71] -0.89938710 -0.80393199 -1.82044848 -1.18087195  1.13053855  0.45551755 -1.37179957
 [78] -0.46902107 -1.08142251  1.89717818  1.29049339 -0.67800570  0.95724414  1.26204968
 [85]  0.46286607 -0.71596384  0.71850168 -0.12525037  0.18443026 -1.61873804  0.43930073
 [92] -1.98640020  0.21291018  2.01944426  1.43737175 -0.72044139  0.39808719  0.09604342
 [99] -0.86227487 -0.58899200
[1] "valores generados de Y"
  [1] -0.40262267  0.17302153 -0.85653006  0.44881078  0.10450577 -0.06512757  0.15400633
  [8] -1.19307820 -1.85184740  0.69121591  0.13433273 -1.03541401  1.49995502 -0.87719119
 [15] -1.22608479 -1.04680677  2.32296434 -0.66015318  2.57615133  1.23946927  1.14960237
 [22] -0.28714177 -0.87278095 -0.14885293 -0.30134326 -1.90010766 -0.62253419  1.94309294
 [29] -0.32898525  0.42185549  0.29046902 -0.27828834  0.54431764 -0.01988942  0.02685056
 [36]  0.98045162 -0.44643650 -0.15878770 -0.63315742 -0.06788602 -0.52114597 -1.17261633
 [43]  1.92363908 -0.22384496 -0.48641828  1.05994397 -1.04524715  1.43630599  0.58223555
 [50] -0.07546200  0.31589475  0.70515550  0.05843099  1.10169321 -0.16154190  0.86513635
 [57]  0.34519389  1.31943656 -1.54056641 -0.86777884  0.31394951 -0.37388777 -1.00003315
 [64] -0.98030511 -1.08395038  0.06142717  1.11447805  0.15450985 -0.23843068  0.62013865
 [71]  1.83062770  0.84917672  0.71102659  0.86187035 -0.28336571  0.17436825  0.09043334
 [78] -1.31371110  0.23511116 -2.44798578 -0.11943985 -1.99362527 -0.06110943  1.55087167
 [85] -0.55017294 -0.82821069  1.69195040  0.50343408  0.23723136 -0.07316155 -1.46784185
 [92] -0.57299838  1.51780682  0.43787153 -0.33769026 -0.22066275  0.93748799  0.45979068
 [99]  1.03553346 -0.8775717
```

## Visualización y Reportería 

Ver estas funcionalidades en el [manual](https://github.com/ljofre/epg3308/tree/master/man)


## Autores

Seomara Palominos (skpalominos@uc.cl)

<img src="https://media.licdn.com/mpr/mpr/shrinknp_400_400/AAEAAQAAAAAAAAkKAAAAJGEwNjIxNDcxLWQ5OWUtNGMxMC1iZjNhLWU4NGUyNmYwZjA3Zg.jpg" width="200" height="200" />


Leonardo Jofré (lnjofre@uc.cl)

<img src="https://media.licdn.com/mpr/mpr/shrinknp_400_400/AAEAAQAAAAAAAAmpAAAAJDVhMWI1M2YzLWExYzMtNDZiZi1hMmViLTgzMmFhNzkyOTc3Yw.jpg" width="200" height="200" />


