#CNCI
## About CNCI
It is a challenge to classify protein-coding or non-coding transcripts, especially those re-constructed from high-throughput sequencing data of poorly annotated species. We developed and evaluated a powerful signature tool, Coding-Non-Coding Index (CNCI), by profiling adjoining nucleotide triplets to effectively distinguish protein-coding and non-coding sequences independent of known annotations. CNCI is effective for classifying incomplete transcripts and sense-antisense pairs. The implementation of CNCI offered highly accurate classification of transcripts assembled from whole-transcriptome sequencing data in a cross-species manner, that demonstrated gene evolutionary divergence between vertebrates, and invertebrates, or between plants, and provided a long non-coding RNA catalog of orangutan.

![CNCI](http://nar.oxfordjournals.org/content/early/2013/08/06/nar.gkt646/F1.medium.gif)

## Current Version
Release : CNCI version 2 Feb 28, 2014

## Documentation
CNCI has update to version 2,in this version some bugs have be fixed,and more friendly for users. CNCI can run in 32-bit Linux, 64-bit Linux. Please note that: CNCI's input file must not be empty.

## Install CNCI
At the first time to running CNCI, we suggest you to install "libsvm-3.0" that stored in our package.

```
git clone git@github.com:www-bioinfo-org/CNCI.git
cd CNCI
unzip libsvm-3.0.zip
cd libsvm-3.0
make
cd ..
```

## HELP for CNCI subroutines

**compare.py: compare the merged/assembled transcripts with known gene annotation!**

Usage: compare.py [-h] -c coding_ref -n noncoding_ref -i input_gtf -o out_dir

Parameters:

-h, --help show this help message and exit.

-c CODING_REF, --coding_ref=CODING_REF

(Required.) The path of coding reference gtf file. Two mandatory attributes (gene_id "value"; transcript_id "value") should be provided in the file. Some files which has been prepared could be download at http://www.bioinfo.org/np/

-n NONCODING_REF, --noncoding_ref=NONCODING_REF.

(Required.) The path of lincRNA reference gtf file. Two mandatory attributes (gene_id "value"; transcript_id "value") should be provided in the file. Some files which has been prepared could be download at http://www.bioinfo.org/np/

-i INPUT_GTF, --input_gtf=INPUT_GTF

(Required.) The path of user input assemble gtf file. This file usually be generated by cufflinks/cuffcompare/cuffmerge. Also, two mandatory attributes (gene_id "value"; transcript_id "value") should be provided in the file.

-o OUT_DIR, --out_dir=OUT_DIR

(Required.) Output dirctory of the results. 

**CNCI: A classification tool for identify coding or non-coding transcripts (fasta files and gtf files)**

Parameters: 

-f or --file : input files

-o or --out : assign your output file in current directory (this parameter will produce a Temp sub-folder in current directory, and will remove it automatically at the end of programming), and the result is stored in xxx.index

-p or --parallel : assign the running CUP numbers

-m or --model : assign the classification models ("ve" for vertebrate species, "pl" for plat species)

-g or --gtf : if you input files is gtf format please use this parameter

-d or --directory : if you use the -g or --gtf this parameter must be 
assigned, within this parameter please assign the path of your reference genome.

**filter_novel_lincRNA.py: A tool that can convert the index file which produced by python CNCI_package/CNCI.py to four gene classes (novel_lincRNA,novel_coding, ambiguous_genes and filter_out_noncoding)**

Usage: filter_novel_lincRNA.py [-h] [-s 0] [-l 200] [-e 2] -i cnci_index -g unannotated_gtf -o out_dir

Parameters: 

-h, --help
show this help message and exit

-i INDEX, --index=INDEX

(Required.) The path of coding/noncoding index file. This file is the output file of CNCI.py.

-g GTF, --gtf=GTF

(Required.) The path of potentially_novel gtf file. This
file could be generated by compare.py.

-s SCORE, --score=SCORE

(Optional.) Threoshold of CNCI score. RNAs with score less than SCORE will be classified as noncoding. The Default is 0 .

-l LENGTH, --length=LENGTH

(Optional.) Minimal length of lincRNA. lincRNA with length >= LENGTH will be kept. The Default is 200.

-e EXON_NUM, --exon_num=EXON_NUM

(Optional.) Minimal exon number of lincRNA. lincRNA with exon number >= EXON_NUM will be kept. The Default is 2.

-o OUT_DIR, --out_dir=OUT_DIR

(Requried.) Output directory of the results.

## EXAMPLE

you can use CNCI subroutines like our example:

```
python CNCI_package/CNCI.py -f unannotation.gtf -g -o test -m ve -p 8 -d hg19.2bit

python filter_novel_lincRNA.py -i test.index -g unannotation.gtf -s 0 -l 200 -e exon_num -o out_dir 

python extract.py -i novel-noncoding.gtf,nov.gtf -n known-non-coding.gtf -c known-coding.gtf
```
*Please note that : "libsvm-3.0 must be installed accordance with our instruction in SETUP section"*

## Citation
+ [Liang Sun, Haitao Luo, Dechao Bu, Guoguang Zhao, Kuntao Yu, Changhai Zhang, Yuanning Liu, RunSheng Chen and Yi Zhao* Utilizing sequence intrinsic composition to classify protein-coding and long non-coding transcripts. Nucleic Acids Research (2013), doi: 10.1093/nar/gkt646](http://nar.oxfordjournals.org/content/early/2013/08/06/nar.gkt646.long)

## Contact
+ Yi Zhao : biozy@ict.ac.cn
