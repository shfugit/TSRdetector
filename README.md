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
**2. Download data for test** </br>
```
wget "https://regmedsrv1.wustl.edu/Public_SPACE/shuhua/Public_html/TSRdetector/testdata.tar.gz"
```
**3. Run TSRdetector with the image** </br>
> [!IMPORTANT]</br>
> Modify the path in the command to your working folder. Put the data for test under the working folder.</br></br>


With hg38 reference:</br>
```
singularity run -B ./:/process  -B /home:/[wd_path] TSRdetector_hgmm.simg -g hg38 -c cluster_cell_test -d test_condition_dat -b hg38_v36_exon_merged_filtered.bed -x 3 -p comparison1 -n TEST_hg38 -v 0.1 -r 20 -s
```
With chm13 (v2) reference:</br>
```
singularity run -B ./:/process  -B /home:/[wd_path] TSRdetector_hgmm.simg -g chm13v2 -c cluster_cell_test -d test_condition_dat -b chm13v2.0_exon_merged_filtered_sorted.bed -x 3 -p comparison1 -n TEST_t2t -v 0.1 -r 20 -s
```
</br>

## Start with bash scripts</br>
**Requirements**</br>
+ STAR (v2.5.4b, if you use STAR of other versions, please use corresponding index files) </br>
+ RSEM (v1.3.0) </br>
+ R (v4.2.0 or above) </br>
+ R libraries: ggplot2, doParallel, foreach, cowplot, matrixStats, RColorBrewer, RUVSeq, rtracklayer, jsonlite</br>
+ samtools (v1.3.1 or above)</br>
+ bedtools (v2.25.0 or above)</br>
+ bedGraphToBigWig (v2.9)</br>
+ Python (3.6.3 or above)</br>
</br>

**1. Download [TSRdetector](https://regmedsrv1.wustl.edu/Public_SPACE/shuhua/Public_html/Docker_image/TSRdetector/TSRdetector.tar.gz)**</br>
```
wget "https://regmedsrv1.wustl.edu/Public_SPACE/shuhua/Public_html/Docker_image/TSRdetector/TSRdetector.tar.gz"
```
</br>
**2. Uncompress it** </br>
```
tar xvzf TSRdetector.tar.gz
```
</br>
**3. Modify the file <process_source.sh>**</br>
Make sure the paths to the folders or exectuables are correct</br>


**Sources:**<br/>
(1) Gencode annotation (hg38, GTF file) : [GENCODE](https://www.gencodegenes.org/human/releases.html)<br />
(2) assembly from 30 human tissue samples by Nanopore RNA-seq reads (GTF file): [GSE192955]( https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE192955)<br />
(3) ENCODE 24 human tissues by long read RNA-seq [ENCODE](https://www.encodeproject.org/matrix/?type=Experiment&control_type!=*&status=released&perturbed=false&assay_title=long+read+RNA-seq&biosample_ontology.classification=tissue&biosample_ontology.classification=tissue&assay_title=total+RNA-seq&assay_title=polyA+plus+RNA-seq)</br>
The mappable long reads are downloaded and corrected by TranscriptClean (v2.0.2) and the unmapped ones are corrected by LoRDEC (v0.9) with corresponding short reads. The long read aligneer used is minimap2 (v2.28). IsoQuant (v.3.3.1) is used to assemble and quantify transcripts on corrected long reads. Only transcripts with TPM>1 is either of the 24 human tissues are included in the assembly. <br />

The prepared GTF file can be downloaded in [reference](https://regmedsrv1.wustl.edu/Public_SPACE/shuhua/Public_html/TSRdetector/merged_assembly_wGene_wCageInfo.gtf)<br />

