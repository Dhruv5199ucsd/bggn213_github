# Class06
Dhruv

General format for R script: ADD \<- FUNCTION(x,y){x+y}

``` r
add <- function(x,y=1){x+y}
```

What would happen if we add x+y

``` r
add(1,1)
```

    [1] 2

``` r
add(c(100,1,100),1)
```

    [1] 101   2 101

``` r
add(c(100,1,100),c(100,1,100))
```

    [1] 200   2 200

``` r
add(10)
```

    [1] 11

``` r
add(1,1)
```

    [1] 2

Make a function that generates a random nucleotide sequence of any
length

``` r
Nucleotides <- c("A","T","G","C")
sequence <- sample(Nucleotides, 100, replace = TRUE)
sequence
```

      [1] "T" "T" "C" "C" "T" "A" "A" "T" "G" "T" "T" "A" "G" "G" "A" "T" "G" "A"
     [19] "A" "T" "A" "A" "A" "T" "G" "A" "G" "G" "T" "T" "A" "A" "T" "C" "G" "A"
     [37] "G" "A" "A" "A" "A" "G" "G" "A" "G" "G" "G" "A" "T" "C" "T" "G" "T" "T"
     [55] "G" "G" "T" "T" "T" "T" "G" "T" "A" "A" "C" "A" "A" "G" "T" "C" "C" "T"
     [73] "A" "G" "C" "G" "G" "G" "C" "A" "T" "C" "G" "G" "G" "T" "C" "T" "C" "C"
     [91] "T" "C" "C" "C" "A" "A" "C" "C" "A" "C"

``` r
Generate_DNA <- function(length){
  Nucleotides <- c("A","T","G","C")
  sequence <- sample(Nucleotides,size = length, replace=TRUE)
  return(sequence)
}
Generate_DNA(10)
```

     [1] "T" "A" "C" "T" "A" "A" "A" "T" "C" "G"

This working snippet ROCKS! Now i can make it into an angelic function

``` r
library(bio3d)
unique(bio3d::aa.table$aa1)[1:20]
```

     [1] "A" "R" "N" "D" "C" "Q" "E" "G" "H" "I" "L" "K" "M" "F" "P" "S" "T" "W" "Y"
    [20] "V"

``` r
amino_acids <- unique(bio3d::aa.table$aa1)[1:20]
sample(amino_acids, size = 30, replace = TRUE)
```

     [1] "P" "W" "F" "F" "F" "E" "P" "E" "D" "S" "K" "N" "T" "C" "F" "T" "K" "S" "H"
    [20] "S" "I" "A" "Q" "D" "Y" "I" "R" "F" "Y" "K"

``` r
Generate_AA <- function(length){
  amino_acids <- unique(bio3d::aa.table$aa1)[1:20]
  string <- sample(amino_acids, size = length, replace = TRUE)
  string <- paste(string, collapse = "")
  return(string)
}
Generate_AA(100)
```

    [1] "LRIIIVPIGSDIYYIQNPFMAHLHNDWKHVTTKMEHIAAVWLDFCGHRMVIDVAYHHDTNIRADVDHIGNVWSNVFRTNEMSELHARSEMSVSYTWTRGM"

I want to generate random sequences of length 6 - 12

``` r
formatted<-sapply(6:12,Generate_AA)
formatted
```

    [1] "RQHWMF"       "TNPHDLC"      "DVNWHRQK"     "KWFLDHFMP"    "KDLLHQKYTP"  
    [6] "FKITPRTSRKY"  "DSQTHFSCPQCH"

``` r
cat(paste(">id.",6:12,"\n", formatted, sep = ""),sep = "\n")
```

    >id.6
    RQHWMF
    >id.7
    TNPHDLC
    >id.8
    DVNWHRQK
    >id.9
    KWFLDHFMP
    >id.10
    KDLLHQKYTP
    >id.11
    FKITPRTSRKY
    >id.12
    DSQTHFSCPQCH
