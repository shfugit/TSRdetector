# TSRdetector
TSRdetector manuscript code


## Usage </br>
### Options </br>
|Option|Description|
| -- | -- |
|-g|Reference genome (hg38, chm13v2, mm10)|
|-c|Cell barcodes for each cell type (single-cell data only)| 
|-b|Input file of reference TSR information|
|-x|Only data from x most abundant cell types will be considered|
|-p|File including the information of comparison between cell types|
|-v|Cutoff of p-value in wilcox test|
|-r|Cutoff of absolute difference of between two cell types or condtions|
|-n|User defined output folder name|
|-s|Use if single-cell data are applied|


## Quick Start with singularity image</br>
**Requirements**</br>
+ Singularity (3.10.3 or above) </br></br>

**1. Download singularity image** </br>
```
wget https://regmedsrv1.wustl.edu/Public_SPACE/shuhua/Public_html/TSRdetector/docker/TSRdetector_hgmm.simg
```
**2. Download and uncompress human single-cell data for test** </br>
```
wget "https://regmedsrv1.wustl.edu/Public_SPACE/shuhua/Public_html/TSRdetector/testdata.tar.gz"
```
Uncompress the folder </br>
```
tar -xvzf testdata.tar.gz
```
**3. Run TSRdetector with the image** </br>
> [!IMPORTANT]</br>
> Modify the path in the command to your working folder. Put the files from folder "testdata" under the working folder.</br></br>


With hg38 reference:</br>
```
singularity run -B ./:/process  -B /home:/[wd_path] TSRdetector_hgmm.simg -g hg38 -c cluster_cell_test -d test_condition_dat -b hg38_v36_exon_merged_filtered.bed -x 3 -p comparison1 -n TEST_hg38 -v 0.1 -r 20 -s
```
With chm13 (v2) reference:</br>
```
singularity run -B ./:/process  -B /home:/[wd_path] TSRdetector_hgmm.simg -g chm13v2 -c cluster_cell_test -d test_condition_dat -b chm13v2.0_TSR.bed -x 3 -p comparison1 -n TEST_t2t -v 0.1 -r 20 -s
```
</br>

## Start with bash scripts</br>
**Requirements**</br>
+ STAR (v2.5.4b, if you use STAR of other versions, please use corresponding index files) </br>
+ RSEM (v1.3.0) </br>
+ R (v4.2.0 or above) </br>
+ R libraries: ggplot2, doParallel, foreach, cowplot, matrixStats, RColorBrewer, RUVSeq, rtracklayer, jsonlite, data.table</br>
+ samtools (v1.3.1 or above)</br>
+ bedtools (v2.25.0 or above)</br>
+ bedGraphToBigWig (v2.9)</br>
+ Python (3.6.3 or above)</br>

**1. Download [TSRdetector](https://regmedsrv1.wustl.edu/Public_SPACE/shuhua/Public_html/Docker_image/TSRdetector/TSRdetector.tar.gz)**</br>
```
wget "https://regmedsrv1.wustl.edu/Public_SPACE/shuhua/Public_html/Docker_image/TSRdetector/TSRdetector.tar.gz"
```
**2. Uncompress it** </br>
```
tar xvzf TSRdetector.tar.gz
```
**3. Modify the file <process_source.sh>**</br>
Make sure the paths to the folders or exectuables are correct</br>
You can apply TSRdetector to your favorite genome by providing relevant files here</br>
</br>
**4. Use test data or your own data to run TSRdetector**</br>
bash TSRdetector.sh [your options] </br>


## Output files</br>
+ TXT-format files for TSR usage comparison that pass ("sig_TSR_xxx") or not pass the cutoff (all comparison results in "all_TSR_xxx"): under folder "summary_files"
+ sashimi plots for each comparison between conditions: under folder "sashimi_plots"
+ percent stacked barplots for each comparison between conditions: under folder "stacked_barplots"
+ bigWig files after merged replicates for same conditions for visualization on [genome browser](https://epigenomegateway.readthedocs.io/en/latest/) under folder "merged_bam_files/bw_files"




