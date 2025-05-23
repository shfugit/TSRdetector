
**Sources:**<br/>
(1) Gencode annotation (hg38, GTF-format file) : [GENCODE](https://www.gencodegenes.org/human/releases.html)<br /><br />
(2) assembly from 30 human tissue samples by Nanopore RNA-seq reads (GTF-format file): [GSE192955]( https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE192955)<br /> </br >
(3) ENCODE 24 human tissues by long read RNA-seq [ENCODE](https://www.encodeproject.org/matrix/?type=Experiment&control_type!=*&status=released&perturbed=false&assay_title=long+read+RNA-seq&biosample_ontology.classification=tissue&biosample_ontology.classification=tissue&assay_title=total+RNA-seq&assay_title=polyA+plus+RNA-seq)</br> </br>
The mappable long reads are downloaded and corrected by TranscriptClean (v2.0.2) and the unmapped ones are corrected by LoRDEC (v0.9) with corresponding short reads. </br> The long read aligner used is minimap2 (v2.28). IsoQuant (v.3.3.1) is used to assemble and quantify transcripts on corrected long reads. </br> Only transcripts with TPM>1 is either of the 24 human tissues are included in the assembly. <br /><br />

The prepared GTF file can be downloaded in [reference](https://regmedsrv1.wustl.edu/Public_SPACE/shuhua/Public_html/TSRdetector/merged_assembly_wGene_wCageInfo.gtf)<br />
