---
layout: default
katex: yes
---
## AFLP (Average Fragment Length Prediction)

Say you develop a new method of doing metagenomics called reduced metagenome sequencing (RMS), in this method you first digest your sample with two
different restriction enzymes and then only sequence those fragments cut by both enzymes. You want to reduce the amount of data about 10-fold so you
pick one 4-base cutter (MseI: TTAA) that will cut frequently and one 6-base cutter (EcoRI: GAATTC) that cuts more infrequently.

In a DNA sequence where each base A, T, C and G are picked at random with equal probabilities EcoRI will cut on average every 4^4 = 4096 bp and 
MseI every 4^4 = 256 bp.

The question I had was this, what is the average length of the fragments cut by both enzymes? Or stated differently, what will be your insert size?

The easiest solution to this problem is to simulate it. First step is to write a function that generates a random DNA sequence, digests it and then
returns the avarage size of the fragments cut by both enzymes. My implementation in R is as follows: 

```R
library(Digestion)
library(dplyr)
data(allRestrictionEnzymes)

avgFragLength <- function(G){
  GC <- 0.5
  genome <- paste(sample(x=c("A","C","G","T"),                 
                         size=G,                               
                         replace=T,                            
                         prob=c((1-GC)/2,GC/2,GC/2,(1-GC)/2)),
                  collapse="")
  fragments <- getDigestionFragments(Restriction=c("EcoRI:MseI"), DNASequence=genome)
  fragments_1 <- filter(fragments, (fragments$EnzymeStart == "MseI" & fragments$EnzymeEnd == "EcoRI") | (fragments$EnzymeStart == "EcoRI" & fragments$EnzymeEnd == "MseI"))
  return(mean(fragments_1$Length))
}
```

This code requires the [Digestion package available here](https://github.com/th-of/Digestion/blob/master/Digestion_1.0.tar.gz). 

This simulation will only provide an estimate of the real value (a numerical solution, not analytical), this estimate should converge towards the real
value with larger and larger genomes. Just to get an idea of what value it should converge towards I will run the function on 100 genomes of increasing size
and plot the result.

```R
test <- unlist(lapply(seq(1000000, 10900000, 100000), avgFragLength))
plot(seq(1000000, 10900000, 100000), test, ylab = "Average fragment length", xlab = "Genome size (bp)")
```
<center>
<img src="/code/AFLP_plot.jpeg">
</center>

```console
> mean(test)
[1] 242.3683
> median(test)
[1] 242.4948
```

It seems like the answer is something close to 242 bp, now that we have an approximate answer we can attempt an analytical solution. With some probability math and trial and error
this is the likely analytical solution:

\\[\frac{1}{  \left(\frac{1-0.5}{2} \right)^{4} + \left(\left(\frac{0.5}{2} \right)^{2} \cdot \left(\frac{1-0.5}{2} \right)^{4} \right)} = 240.\overline{9411764705882352}\\]

Close enough.
