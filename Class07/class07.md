# Class07
Dhruv

KMEANS() is used for PCA analysis. To learn about this, we can create a
test dataset for ourselves. Before anything, we should start with the
`rnorm()` function.

``` r
hist(rnorm(1500))
```

![](class07_files/figure-commonmark/unnamed-chunk-1-1.png)

``` r
hist( rnorm(1500, mean = 3))
```

![](class07_files/figure-commonmark/unnamed-chunk-1-2.png)

``` r
hist( rnorm(1500, mean = -3))
```

![](class07_files/figure-commonmark/unnamed-chunk-1-3.png)

``` r
hist( rnorm(1500, mean = c(-3,3)))
```

![](class07_files/figure-commonmark/unnamed-chunk-1-4.png)

``` r
n=30
hist(c(rnorm(n, mean =3), rnorm(n, mean = -3)))
```

![](class07_files/figure-commonmark/unnamed-chunk-2-1.png)

``` r
x <- c(rnorm(n, mean =3), rnorm(n, mean = -3))
#how to reverse x from y?
y <- rev(x)
y
```

     [1] -2.5390928 -4.1326441 -3.1233244 -3.1328694 -3.4971664 -2.6407358
     [7] -2.0952863 -3.4904587 -5.4233492 -4.7392030 -1.9821322 -3.8752035
    [13] -3.4279517 -1.5140169 -3.8072442 -3.6200996 -4.6634003 -1.9758160
    [19] -1.7055162 -2.1582605 -2.9279507 -3.3222924 -3.8268253 -4.3435314
    [25] -3.1771034 -0.7093496 -2.5532574 -3.2934361 -4.2566945 -3.7046155
    [31]  4.7673888  2.8128161  0.4275863  2.6062708  2.1566756  3.1229065
    [37]  3.4496600  3.0936285  3.1645858  2.5461853  2.1658701  3.7536225
    [43]  2.7664329  3.9695633  3.0237789  3.0348825  2.5419268  2.7863225
    [49]  1.0189556  4.0046724  3.1745307  2.0362817  2.7995932  2.8241696
    [55]  1.1268243  5.1277450  3.3714305  1.5200625  2.3363195  4.0038556

``` r
z <- cbind(x,y)
plot(z)
```

![](class07_files/figure-commonmark/unnamed-chunk-2-2.png)

\##K-means clustering

The function for k-means clustering is called `kmeans()`. Run `kmeans()`
and assign two centers.

``` r
km <- kmeans(z, 2)
```

Q1. Print out the club membership vector (our main answer)

``` r
km$centers
```

              x         y
    1 -3.188628  2.851151
    2  2.851151 -3.188628

``` r
km$cluster
```

     [1] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 1 1 1 1 1 1 1 1
    [39] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1

``` r
plot(z, col = "red")
```

![](class07_files/figure-commonmark/unnamed-chunk-4-1.png)

``` r
plot(z, col = c("red", "blue")) #Think about R as vectors. One vector is two colors against our input of n = 30. 
```

![](class07_files/figure-commonmark/unnamed-chunk-4-2.png)

``` r
plot(z, col = km$cluster)
```

![](class07_files/figure-commonmark/unnamed-chunk-5-1.png)

# plot with clustering result and add centers.

``` r
plot(z, col = km$cluster)
points(km$centers, col = "blue", pch = 15, cex = 2)
```

![](class07_files/figure-commonmark/unnamed-chunk-6-1.png)

> Q. Can you cluster our data in `z` into four clusters

``` r
km_four <- kmeans(z, 4)
```

``` r
plot(z, col = km_four$cluster)
points(km_four$centers, col = "blue", pch = 15, cex = 2)
```

![](class07_files/figure-commonmark/unnamed-chunk-8-1.png)

``` r
kmeans(z,4)
```

    K-means clustering with 4 clusters of sizes 10, 30, 16, 4

    Cluster means:
              x         y
    1  2.936968 -2.016068
    2 -3.188628  2.851151
    3  3.254465 -3.910341
    4  1.023357 -3.233175

    Clustering vector:
     [1] 1 3 4 3 3 4 1 3 3 3 1 4 3 1 3 3 3 1 1 1 1 3 3 3 3 1 1 4 3 3 2 2 2 2 2 2 2 2
    [39] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2

    Within cluster sum of squares by cluster:
    [1]  8.087484 63.189664 15.580540  1.391267
     (between_SS / total_SS =  92.8 %)

    Available components:

    [1] "cluster"      "centers"      "totss"        "withinss"     "tot.withinss"
    [6] "betweenss"    "size"         "iter"         "ifault"      

\##Hierarchical Clustering

Function = `hclust()` For `hclust()` we first need a distance matrix
from data.

``` r
d <- dist(z)
hc <- hclust(d)
plot(hc) #gives a plot where data is divided on two main arms (1-30 and 31-60)
abline(h=10, col = "red")
```

![](class07_files/figure-commonmark/unnamed-chunk-10-1.png)

To get main clustering results, can “cut” the tree and give height. to
do this, use `cutree`.

``` r
grps <- cutree(hc, h=10)
```

``` r
plot(z, col = grps)
```

![](class07_files/figure-commonmark/unnamed-chunk-12-1.png)

\##Principle component analysis (PCA)

Take original data, and choose path with most variance and assign it
PC1. Then draw PC2 to capture more variance.

``` r
url <- "https://tinyurl.com/UK-foods"
x <- read.csv(url)
nrow(x) #Q.1 answer
```

    [1] 17

``` r
ncol(x)# Q.1 answer
```

    [1] 5

``` r
head(x) # Q.2 answer 
```

                   X England Wales Scotland N.Ireland
    1         Cheese     105   103      103        66
    2  Carcass_meat      245   227      242       267
    3    Other_meat      685   803      750       586
    4           Fish     147   160      122        93
    5 Fats_and_oils      193   235      184       209
    6         Sugars     156   175      147       139

``` r
rownames(x) <- x[,1]
x <- x[,-1]
head(x)
```

                   England Wales Scotland N.Ireland
    Cheese             105   103      103        66
    Carcass_meat       245   227      242       267
    Other_meat         685   803      750       586
    Fish               147   160      122        93
    Fats_and_oils      193   235      184       209
    Sugars             156   175      147       139

``` r
url <- "https://tinyurl.com/UK-foods"
x <- read.csv(url,row.names = 1)
nrow(x) #Q.1 answer
```

    [1] 17

``` r
ncol(x)# Q.1 answer
```

    [1] 4

``` r
dim(x)
```

    [1] 17  4

``` r
barplot(as.matrix(x), col=rainbow(nrow(x)))
```

![](class07_files/figure-commonmark/unnamed-chunk-14-1.png)

``` r
pairs(x, col=rainbow(10), pch=16)
```

![](class07_files/figure-commonmark/unnamed-chunk-14-2.png)

## 17 variables is not close to how many dimensions we would normally look at. Using PCA

Function for PCA in base R is `prcomp()`

``` r
x
```

                        England Wales Scotland N.Ireland
    Cheese                  105   103      103        66
    Carcass_meat            245   227      242       267
    Other_meat              685   803      750       586
    Fish                    147   160      122        93
    Fats_and_oils           193   235      184       209
    Sugars                  156   175      147       139
    Fresh_potatoes          720   874      566      1033
    Fresh_Veg               253   265      171       143
    Other_Veg               488   570      418       355
    Processed_potatoes      198   203      220       187
    Processed_Veg           360   365      337       334
    Fresh_fruit            1102  1137      957       674
    Cereals                1472  1582     1462      1494
    Beverages                57    73       53        47
    Soft_drinks            1374  1256     1572      1506
    Alcoholic_drinks        375   475      458       135
    Confectionery            54    64       62        41

``` r
t(x)
```

              Cheese Carcass_meat  Other_meat  Fish Fats_and_oils  Sugars
    England      105           245         685  147            193    156
    Wales        103           227         803  160            235    175
    Scotland     103           242         750  122            184    147
    N.Ireland     66           267         586   93            209    139
              Fresh_potatoes  Fresh_Veg  Other_Veg  Processed_potatoes 
    England               720        253        488                 198
    Wales                 874        265        570                 203
    Scotland              566        171        418                 220
    N.Ireland            1033        143        355                 187
              Processed_Veg  Fresh_fruit  Cereals  Beverages Soft_drinks 
    England              360         1102     1472        57         1374
    Wales                365         1137     1582        73         1256
    Scotland             337          957     1462        53         1572
    N.Ireland            334          674     1494        47         1506
              Alcoholic_drinks  Confectionery 
    England                 375             54
    Wales                   475             64
    Scotland                458             62
    N.Ireland               135             41

``` r
pca <- prcomp(t(x))
summary (pca)
```

    Importance of components:
                                PC1      PC2      PC3       PC4
    Standard deviation     324.1502 212.7478 73.87622 2.921e-14
    Proportion of Variance   0.6744   0.2905  0.03503 0.000e+00
    Cumulative Proportion    0.6744   0.9650  1.00000 1.000e+00

``` r
pca$rotation
```

                                 PC1          PC2         PC3          PC4
    Cheese              -0.056955380  0.016012850  0.02394295 -0.409382587
    Carcass_meat         0.047927628  0.013915823  0.06367111  0.729481922
    Other_meat          -0.258916658 -0.015331138 -0.55384854  0.331001134
    Fish                -0.084414983 -0.050754947  0.03906481  0.022375878
    Fats_and_oils       -0.005193623 -0.095388656 -0.12522257  0.034512161
    Sugars              -0.037620983 -0.043021699 -0.03605745  0.024943337
    Fresh_potatoes       0.401402060 -0.715017078 -0.20668248  0.021396007
    Fresh_Veg           -0.151849942 -0.144900268  0.21382237  0.001606882
    Other_Veg           -0.243593729 -0.225450923 -0.05332841  0.031153231
    Processed_potatoes  -0.026886233  0.042850761 -0.07364902 -0.017379680
    Processed_Veg       -0.036488269 -0.045451802  0.05289191  0.021250980
    Fresh_fruit         -0.632640898 -0.177740743  0.40012865  0.227657348
    Cereals             -0.047702858 -0.212599678 -0.35884921  0.100043319
    Beverages           -0.026187756 -0.030560542 -0.04135860 -0.018382072
    Soft_drinks          0.232244140  0.555124311 -0.16942648  0.222319484
    Alcoholic_drinks    -0.463968168  0.113536523 -0.49858320 -0.273126013
    Confectionery       -0.029650201  0.005949921 -0.05232164  0.001890737

What is inside our result from our object pca

``` r
attributes(pca)
```

    $names
    [1] "sdev"     "rotation" "center"   "scale"    "x"       

    $class
    [1] "prcomp"

``` r
pca$x
```

                     PC1         PC2        PC3           PC4
    England   -144.99315   -2.532999 105.768945 -9.152022e-15
    Wales     -240.52915 -224.646925 -56.475555  5.560040e-13
    Scotland   -91.86934  286.081786 -44.415495 -6.638419e-13
    N.Ireland  477.39164  -58.901862  -4.877895  1.329771e-13

To make our PC plot/Score plot/ordination plot/PC1/2 plot.

``` r
plot(pca$x[,1], pca$x[,2], col = x[,1])
```

![](class07_files/figure-commonmark/unnamed-chunk-18-1.png)

``` r
plot(pca$x[,1], pca$x[,2], col = c("black", "red", "blue", "darkgreen"), pch = 16, xlab = "PC1(67.4%)", ylab = "PC2 (29%)")
```

![](class07_files/figure-commonmark/unnamed-chunk-18-2.png)

## add loadings plot before submitting this.

``` r
## Lets focus on PC1 as it accounts for > 90% of variance 
par(mar=c(10, 3, 0.35, 0))
barplot( pca$rotation[,1], las=2 )
```

![](class07_files/figure-commonmark/unnamed-chunk-19-1.png)

``` r
barplot( pca$rotation[,4], las=2 )
```

![](class07_files/figure-commonmark/unnamed-chunk-19-2.png)

``` r
pca$rotation
```

                                 PC1          PC2         PC3          PC4
    Cheese              -0.056955380  0.016012850  0.02394295 -0.409382587
    Carcass_meat         0.047927628  0.013915823  0.06367111  0.729481922
    Other_meat          -0.258916658 -0.015331138 -0.55384854  0.331001134
    Fish                -0.084414983 -0.050754947  0.03906481  0.022375878
    Fats_and_oils       -0.005193623 -0.095388656 -0.12522257  0.034512161
    Sugars              -0.037620983 -0.043021699 -0.03605745  0.024943337
    Fresh_potatoes       0.401402060 -0.715017078 -0.20668248  0.021396007
    Fresh_Veg           -0.151849942 -0.144900268  0.21382237  0.001606882
    Other_Veg           -0.243593729 -0.225450923 -0.05332841  0.031153231
    Processed_potatoes  -0.026886233  0.042850761 -0.07364902 -0.017379680
    Processed_Veg       -0.036488269 -0.045451802  0.05289191  0.021250980
    Fresh_fruit         -0.632640898 -0.177740743  0.40012865  0.227657348
    Cereals             -0.047702858 -0.212599678 -0.35884921  0.100043319
    Beverages           -0.026187756 -0.030560542 -0.04135860 -0.018382072
    Soft_drinks          0.232244140  0.555124311 -0.16942648  0.222319484
    Alcoholic_drinks    -0.463968168  0.113536523 -0.49858320 -0.273126013
    Confectionery       -0.029650201  0.005949921 -0.05232164  0.001890737
