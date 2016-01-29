#Using R to build Latex Table: Descriptive Statistics and Correlation Analysis

- The intent is to build out the latex with the data, so final tweaking for publication can be accomplished.
- This builds a standalone latex file with minimal package libraries to create a nicely formated table with Descriptive Statistics (M, SD) and Correlations.
- This generates the raw latex code directly without relying on other packages such as xtable
- This uses standard r@{}l to align decimal points and does NOT use dcolumn or siunitx


##Fundamental usage
```
source("R-latex-corr.txt");
corr.latex(x, file="sample.tex");
```

##Basic Example with Optional parameter (rotate me)
```
data(iris);
x = iris[,1:4];
colnames(x) = c("Sepal (Length)","Sepal (Width)","Petal (Length)","Petal (Width)");
 
source("R-latex-corr.txt");
corr.latex(x, file="iris.tex", rotateMe = F, decimal=4);
```

##Option List
* **x**: data frame (x) with colnames(x) containing only the variables to compute pairwise correlations
* **file**: filename relative to working directory, default is ```"correlations.tex"```
* **rotateMe**: using sidewaystable instead of table to rotate the correlation table, default is ```T(rue)```
* **decimal**: number of decimals to use throughout the table with trailing zeroes if necessary.  Current formatting is no leading zeroes before the decimal point, default is ```2```
* **showSummary**: should the summary statistics be included, or only the pairwise correlations, default is ```T(rue)```
* **showNumbers**: should the labels on the left include an auto-incremented number that is then displayed on the top columns (if false, the top columns will have the labels again), default is ```T(rue)```
* **lastColumn**: should the last diagonal entry be include (the trailing 1) or will the top columns have (N-1) entries, default is ```F(alse)```
* **type**: which correlation type should be computed from the Hmisc packing using R, c("pearson","spearman"), default is ```"pearson"``` [See http://www.inside-r.org/packages/cran/hmisc/docs/rcorr]
* **diagonal**: what value does the diagonal entry contain, default ```'1'```
* **whichTriangle**: which part of correlation matrix is displayed, c("lower","upper","both"), default is ```"lower"```
* **probs**: vector of probabilites to include significance and starts, default is ```c(.001,.01,.05,.10)```
* **sym**: symbols matching the probs, in the correct order[Note: latex symbols that have an escape \dagger, using R, in string syntax need to be escaped to \\dagger], default is ```c("***","**","*","\\dagger")``` 


TODO
- [x] Working example with most parameters
- [X] Code showSummary
- [X] Code lastColumn
- [ ] Consider default spacing elements as parameters ? Empty columns as | exist between:  labels | stats | correlations ... final tweaking can just occur with Find/Replace in latex when you place it in a bigger file
- [ ] Try-catch-exception to a dataframe x without colnames(x)
- [X] Code decimal form of diagonal=1.00 with the alignment using r@{}l
- [X] Code whichTriangle
- [ ] Possibly update probs, sym so it is a matched list
- [ ] Possibly allow other summary statistics, e.g., pass a vector of items (with display names):  stats=c("mean","sd") with names(stats)=c("M","SD") or stats=c("Q1","median","Q3") with names(stats) unnecessary
- [ ] Consider adding parameter bold=0.05 to bold values that are less than or equal to this threshold
