# SATC
Sex assignment through coverage

Framework for joint determination of individual sex and sex-linked scaffolds for non-model organism based on genome coverage. Our method assign individual sex by projecting sequencing depth of the samples to a two dimensional Principal Component Analysis plot followed by Gaussian mixture clustering. Jointly sex-linked scaffolds are identified based on differences in male and female read depth by a two-sample t-test.

SATC works following these steps:

1. Normalizing the depth of each scaffold within each sample
2. Reducing the dimensionality of the normalized depths using PCA
3. Clustering the samples using Gaussian mixtures clustering on the top PCs, 
4. Identifying the sample sex and sex-linked scaffolds from the clustering and the DoC. 


## Get SATC
```bash
git clone https://github.com/popgenDK/SATC
cd SATC/
```

### Install dependencies
The required R package (mclust) can be easily installed, we have already included an automatic install code in our main function if needed.

## Usage

SATC is run by executing the main function file satc.R:
```bash
Rscript --vanilla satc.R <prefix> <idxstat folder path> <output folder path>
```

SATC will output a list and saved as a single R object in (.rds) format. To read files in R:
```R
data <-readRDS(file ="path to <prefix>.sexSample_sexScaffolds.rds") #reads SATC output
sexSamples <- data$sex #inferred sex for samples
X_Z_scaffolds <- data$SexScaffolds[data$SexScaffold$X_Z_Scaffolds,1] #get a vector of X_Z_scaffolds
Sex_linked_Scaffolds <- data$SexScaffolds[data$SexScaffold$Sex_linked_Scaffolds,1] #get a vector of Sex_linked_Scaffolds

#Plotting
source("satc.R")
#To get plot of normalized depth from all scaffolds and all samples
plotDepth(data)
#To get a PCA plot, different color suggest different sex
plotGroup(data)
#To get boxplots of X_Z Scaffolds grouped by sex
plotScafs(data)
#To get boxplots of Sex-linked Scaffolds grouped by sex
plotScafs(data,ab=T)
```
## Example Usage

Below is an example of performing SATC on our leopard data:
```bash
Rscript --vanilla satc.R leo examples/idx_leopard/ .
```

```R
data <-readRDS(file ="leo.sexSample_sexScaffolds.rds")

#Plotting
source("satc.R")
plotDepth(data)
plotGroup(data)
plotScafs(data)
```
By running SATC, it will automatically produced two plots (normalized depth plot, PCA and Sex-linked Scaffolds) in png format.

For example, here's a normalized depth plot of leopard dataset:
<p align="center" width="100%">
    <img width="50%" src="https://github.com/popgenDK/SATC/blob/6f919613ed9765ef108bcdb63a37d18c9f3e7ae7/examples/plots/leo_depth.png"> 
</p>

Also PCA plot and boxplot of X/Z Scaffolds:
![](https://github.com/popgenDK/SATC/blob/6f919613ed9765ef108bcdb63a37d18c9f3e7ae7/examples/plots/leo_PCA_and_boxplot.png)


## Citation
Please cite our papers:
......
