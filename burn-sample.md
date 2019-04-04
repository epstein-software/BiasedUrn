## Example

Here we present an example of using the BiasedUrn package to perform permutation sampling of case-control data that adjusts for covariates. The set of case-control data used in this example can be downloaded [here](test.dat).  

We begin by loading the BiasedUrn package, setting the permutation counts, then reading the data file containing disease and covariate data. For this example, there are 600 subjects and we wish to perform 1000 permutations.  

<div class="chunk">

<div class="rcode">

<div class="source">

<pre class="knitr"><span class="functioncall">library</span>(<span class="string">"BiasedUrn"</span>)

n.subjects <- 600
n.permutations <- 1000

# the file <span class="string">'test.dat'</span> contains the case-control subject data:
datamat <- <span class="functioncall">matrix</span>(<span class="functioncall">scan</span>(<span class="string">"test.dat"</span>), nrow = n.subjects, byrow = T)
</pre>

</div>

</div>

</div>

For the subject data in this example, the first column is the case-control status while the remaining columns denote the covariate data. We assign these subarrays below.  

<div class="chunk">

<div class="rcode">

<div class="source">

<pre class="knitr">dis <- datamat[, 1]
n.cases <- <span class="functioncall">sum</span>(dis)  # number of case subjects
cov <- datamat[, -<span class="functioncall">c</span>(1)]
</pre>

</div>

</div>

</div>

The first step to permutation sampling is to fit a logistic-regression model; using the notation in [Epstein, et al., 2012](http://dx.doi.org/10.1016/j.ajhg.2012.06.004), this is  

![eqn-1](http://genetics.emory.edu/labs/epstein/software/BiasedUrn/eqn-1.png)  

<div class="chunk">

<div class="rcode">

<div class="source">

<pre class="knitr">model <- <span class="functioncall">glm</span>(dis ~ cov, family = <span class="functioncall">binomial</span>())
</pre>

</div>

</div>

</div>

The maximum-likelihood estimates of these parameters are then used to construct the estimated disease odds for the j-th subject, i.e.,  

![eqn-2](http://genetics.emory.edu/labs/epstein/software/BiasedUrn/eqn-2.png)  

<div class="chunk">

<div class="rcode">

<div class="source">

<pre class="knitr">disease.odds <- <span class="functioncall">exp</span>(model$linear.predictors)
</pre>

</div>

</div>

</div>

Finally, we generate an `n.subjects X n.permutations` matrix of permuted datasets. Note that each column (rather than each row) of the resulting matrix corresponds to a permuted dataset that can then be used to establish significance of a case-control test.  

<div class="chunk">

<div class="rcode">

<div class="source">

<pre class="knitr">m1 <- <span class="functioncall">c</span>(<span class="functioncall">rep</span>(1, <span class="functioncall">length</span>(dis)))
perm.hg <- <span class="functioncall">rMFNCHypergeo</span>(n.permutations, m1, n.cases, disease.odds)
</pre>

</div>

</div>

</div>


[Epstein software](http://genetics.emory.edu/labs/epstein/software/index.html) | [Human Genetics](http://genetics.emory.edu/) | [School of Medicine](http://www.med.emory.edu/) | [Emory University](http://www.emory.edu/)
