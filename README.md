# Deep Generative Modeling and Probabilistic Dimension Reduction

RNA-seq is a way to measure our body's gene expression. In recent years, RNA-seq has driven medical innovation and discovery. The approach is often applied to tissues containing tens of thousands to millions of cells. However, this has prevented direct assessment of the cells within the tissue. As a result, the sequencing process was applied to individual cells, called single-cell RNA-eq, instead of tissues. The opportunities arising from single-cell RNA-eq are enormous, but its data pose unique and new challenges. 


## Challenges in analyzing Single-cell RNA-eq data 

- Sparsity and dropout: the scRNA-seq data are sparse and typically have a high percentage of observed zeros. The zeros in the scRNA-seq are typically from two sources. One is biological, where a gene is not expressed (the count is zero), and the other is technical, where a gene is expressed but not detected in the experiment, called "dropout."
- Batch effect: operational limitations cause the data to be generated separately (at different times or in various laboratories) for large-scale studies. Consequently, there will be differences between distinctive groups. These differences are not due to biological reasons and are technical errors that happen when cells from one group are processed separately from cells in a second group.
- Unlabeled samples: cell types are undetermined and have to be labeled during the analyses.
- Curse of dimensionality: in a typical single-cell experiment, each cell (sample) could have more than 20,000 genes (features).
- Count data: the count nature of the data has to be considered in the analyses; i.e., the measurements are integers and not floating point numbers.
- Scalability: analyzing the ever-growing number of cells (samples), ranging from thousands to millions in large projects like the Human Cell Atlas, is a major challenge in scRNA-seq data analysis. Many statistical and machine learning methods developed for scRNA-seq fail to scale to more than 30,000 samples.

Applying the appropriate computational and statistical techniques is essential to ensuring that scRNA-seq data are used efficiently and interpreted correctly. Consequently, many statistical and machine learning models have been developed to analyze scRNA-seq data. 

Here, I have re-engineered the implementation of the [scVI](https://www.nature.com/articles/s41592-018-0229-2) tool, developed at the University of Berkeley, using [Pyro](https://pyro.ai/), [PyTorch Lightning](https://www.pytorchlightning.ai/), and Pytorch resulted in fewer lines of code, more efficiency, and reliability. scVI is a general dimension reduction and data imputation tool which can be trained efficiently for large datasets.

The Colab notebook contains a short report of my implementation, interpretations, and results.
