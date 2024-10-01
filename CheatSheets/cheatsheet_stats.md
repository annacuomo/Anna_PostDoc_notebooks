# Stats functions that may be useful

In some cases, self-implemented

## Cohen's kappa

[wiki](https://en.wikipedia.org/wiki/Cohen%27s_kappa)

```R
cohens_kappa <- function(a,b,c,d){
    n = a+b+c+d
    po = (a+d)/n
    pe = ((a+b)/n)*((a+c)/n) + ((c+d)/n)*((b+d)/n)
    k = (po-pe)/(1-pe)
    k
}
```

## Lambda GC

Also called genomic control / genomic inflation / just lambda.

https://genometoolbox.blogspot.com/2014/08/how-to-calculate-genomic-inflation.html
