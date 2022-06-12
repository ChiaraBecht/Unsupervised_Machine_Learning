# Cluster analysis of Gene expression in lung cancer types

The gene expression was measured using microarray technique. The microarray is a well with several moles, which are coated with known sequences. If a known gene is expressed, it will bind to one of the coatings in the well. The coating has a fluorescent tag and intensity values can be measured for each mole/chamber. However, very high intensities can radiate and overlay the actual lower intensity of neighboring moles/chambers. This may introduce noise and can increase the contribution of the individual variance of genes with low expression. Moreover a bias towards high intensities is likely to occur [references] Handling the data collection characteristics requires appropriate data preparation. The gene expression set has the typical high dimensionality (about 60600 genes).

The major issue with gene expression data is (no matter whether obtained from microarrays or sequencing), that the number of genes (features) exceeds the number of observations massively. [https://www.sciencedirect.com/science/article/pii/S0025556401001067] This is the exact opposite case of what we like to have in machine learning. The more observation for a small subset of features the more likely to find a good predictor, which does not overfit and not learn noise or the few samples provided by heart. Dimensionality reduction is the main challenge when dealing with gene expression data. Especially conducting the dimensionality reduction in such a way, that it still covers the most of the information. Oftentimes it is desired to find the most influential genes as well. 

## Chosen methods
Standard preprocessing (often seen [references]) is conducting a PCA as preparation to reduce the dimensionality and then conduct clustering (often k-means or hierarchical clustering) on the first 2 or 3 prinicple components. As in the reader [reference] pointed out, directions of variance are not necessarily overlapping with the directions/embedding of best cluster separation. Therefore, the idea was to use spectral graph embedding as preprocessing, which conducts an eigendecomposition on the graph laplacian. In contrast to PCA (eigendecomposition of covariance or correlation matrix) the eigendecomposition is conducted on the spectrum of adjacency, which provides more insight into separation or dense clusters based on the connectivity. Unfortunately, spectral graph clustering requires building a adjacency matrix, digagonal matrix and graph laplacian, which have the size variables x variables, which is for this huge dataset not feasible.

PCA as implemented in scikit learn package does allow to process this big dataset, however due to the previously mentioned reasons other methods were preferred. Multidimensional scaling was assumed to be a good alternative, since it is based on dissimilarity matrix rather than on covariance/correlation. Distance/similiarity are as well the criteria, on which clustering is based, which seemed to be a better match than the covariance/correlation. 

As cluster methods, ...

preprocessing ideas:
normalisation -> enrichment analysis (what i mean: finding the genes most different -> will lead to most cluster separation)


## Future steps
### Reducing dimensionality in a meaningful way
With consecutive advances in annotation of genes related to diseases, gene panels are available, which focus on sets of genes relevant for the target tissue, for cancer and the already known linkage between tissue type and cancer. This might be a step which can help to reduce dimensionality in the first place, then followed by an unsupervised technique of dimensionality reduction. [https://news.mayocliniclabs.com/2020/06/26/lung-cancer-targeted-gene-panel-a-test-in-focus/]