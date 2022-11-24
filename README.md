# Deep Generative Modeling and Probabilistic Dimension Reduction

RNA-seq is a way to measure our body's gene expression. In recent years, RNA-seq has driven medical innovation and discovery. The approach is often applied to tissues containing tens of thousands to millions of cells. However, this has prevented direct assessment of the cells within the tissue. As a result, the sequencing process was applied to individual cells, called single-cell RNA-eq, instead of tissues. The opportunities arising from single-cell RNA-eq are enormous, but its data pose unique and new challenges. 


## Challenges in analyzing Single-cell RNA-eq data 

- **Sparsity and dropout:** The scRNA-seq data are sparse and typically have a high percentage of observed zeros. The zeros in the scRNA-seq are typically from two sources. One is biological, where a gene is not expressed (the count is zero), and the other is technical, where a gene is expressed but not detected in the experiment, called "dropout."
- **Batch effect:** Operational limitations cause the data to be generated separately (at different times or in various laboratories) for large-scale studies. Consequently, there will be differences between distinctive groups. These differences are not due to biological reasons and are technical errors that happen when cells from one group are processed separately from cells in a second group.
- **Unlabeled samples:** Cell types are undetermined and have to be labeled during the analyses.
- **Curse of dimensionality:** In a typical single-cell experiment, each cell (sample) could have more than 20,000 genes (features).
- **Count data:** The count nature of the data has to be considered in the analyses; i.e., the measurements are integers and not floating point numbers.
- **Scalability:** Analyzing the ever-growing number of cells (samples), ranging from thousands to millions in large projects like the Human Cell Atlas, is a major challenge in scRNA-seq data analysis. Many statistical and machine learning methods developed for scRNA-seq fail to scale to more than 30,000 samples.

Applying the appropriate computational and statistical techniques is essential to ensuring that scRNA-seq data are used efficiently and interpreted correctly. Consequently, many statistical and machine learning models have been developed to analyze scRNA-seq data. 

Here, I have re-engineered the implementation of the [scVI](https://www.nature.com/articles/s41592-018-0229-2) tool, developed at the University of Berkeley, using [Pyro](https://pyro.ai/), [PyTorch Lightning](https://www.pytorchlightning.ai/), and Pytorch resulted in fewer lines of code, more efficiency, and reliability. scVI is a general dimension reduction and data imputation tool which can be trained efficiently for large datasets.

## scVI
scVI is a variational autoencoder with latent variables specified by normal distributions and generates estimations of the Zero-Inflated Negative Binomial (ZINB) distribution parameters through a nonlinear transformation of data. Lopez *et al.* showed that scVI captures meaningful biological information through nonlinear transformation and is scalable from tens of thousands of cells to a million. 

In the scVI, $Y_{ij}$, the expression count of gene $j$ in sample $i$ of matrix $Y$, is modeled as a random variable following the ZINB distribution. The ZINB distribution is as follows: 

$$f_{\mathrm{ZINB}}(y;\mu ,\theta ,\pi ) = \pi \delta _0(y) + (1 - \pi )f_{\mathrm{NB}}(y;\mu ,\theta ),\quad \forall y \in {\mathbb N}$$

where $f_{\mathrm{NB}}$ is: 

$$f_{\mathrm{NB}}(y;\mu ,\theta ) = \frac{{{{\Gamma }}(y + \theta )}}{{{{\Gamma }}(y + 1){{\Gamma }}(\theta )}}\left( {\frac{\theta }{{\theta + \mu }}} \right)^\theta \left( {\frac{\mu }{{\mu + \theta }}} \right)^y,\quad \forall y \in {\mathbb N}$$

scVI uses a Bayesian approach in which the probability of observing $Y_{ij}$ is $p(Y_{ij}{\mathrm{|}}z_i,s_i,\ell_i)$, where $s_i$ is the batch annotation of each cell, and $\ell_i$ and $z_i$ are the latent variables. The $\ell_i$ is a variable following a Gaussian distribution with a dimension of one which captures technical variations. On the other hand, $z_i$ is a multi-dimensional variable following a Gaussian distribution that captures biological variations. The overall structure of the scVI has two parts: the Variational posterior and Generative model. The Variational posterior consists of multiple fully-connected Neural Networks (NNs) to transform the gene expression count into two latent variables ( $\ell_i$ and $z_i$ ). The Generative model part contains several fully-connected NNs which generate $\pi_i$, $\mu_i$, and $\theta_i$, the parameters of ZINB distribution, from the latent variables ( $\ell_i$ and $z_i$ ) and batch annotations ( $s_i$ ).

The Colab notebook contains a short report of my implementation, interpretations, and results.
