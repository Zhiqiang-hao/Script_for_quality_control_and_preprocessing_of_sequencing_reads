# Script_for_quality_control_and_preprocessing_of_sequencing_reads
Here, we provide the sample data for the users to test the pipeline for quality control and preprocessing of sequencing reads, and the softwares used in pipeline were provided with their download links.
The complete smaple data can be accessed with the URL as follows:
http://ftp.sra.ebi.ac.uk/vol1/fastq/SRR206/007/SRR2061397/SRR2061397_1.fastq.gz
http://ftp.sra.ebi.ac.uk/vol1/fastq/SRR206/007/SRR2061397/SRR2061397_2.fastq.gz
http://ftp.sra.ebi.ac.uk/vol1/fastq/SRR206/008/SRR2061398/SRR2061398_1.fastq.gz
http://ftp.sra.ebi.ac.uk/vol1/fastq/SRR206/008/SRR2061398/SRR2061398_2.fastq.gz
The prequisite softwares can be obtained by visiting their released website. For example,
1. FastQC can be accessed by https://codeload.github.com/s-andrews/FastQC/zip/refs/heads/master, or  it can be installed in your computer by conda (conda install fastqc)
2. iTools can be accessed by https://github.com/BGI-shenzhen/Reseqtools/blob/master/iTools_Code20180520.tar.gz
3. Cutadapt can be accessed by https://codeload.github.com/jamescasbon/cutadapt/zip/refs/heads/master
4. Fastp can be accessed by https://codeload.github.com/OpenGene/fastp/zip/refs/heads/master, and the alternative way is conda (conda install -c bioconda fastp)
5. FASTX can be accessed by https://codeload.github.com/agordon/fastx_toolkit/zip/refs/heads/master
User can install and use those softwares with linux-like system.

By integrating those softwares, we could finish the quality control and preprocessing for high-throughput data in multiple way. In addition, we provide the simple usage of those software for the users.
FastQC can be either as an interactive  graphical application. Alternatively, you can run the program in non-interactive way. If you don't specific any files to process the program will try to open the interactive application. Click the file button and choose fastq files located in your computer. Click the confirm button, and wait your reports about several minutes. Run fastqc from the command line like this:
fastqc -t 8 -o outdir SRR2061397_1.fastq  SRR2061397_2.fastq  SRR2061398_1.fastq   SRR2061397_2.fastq
Parameter description: -t for CPU number, -o for output directory

iTools is a toolkit for analyzing next-generation sequencing data. One module of iTools is Fqtools, which processes the fastq sequence file. Here, we show one of its function as follows: summarizes the quality and amount of data as well as the GC content. Run iTools from the command line like this:
iTools Fqtools stat -InFq SRR2061397_1.fastq -InFq SRR2061397_1.fastq -InFq SRR2061398_1.fastq -InFq SRR2061397_2.fastq -OutStat read.info -CPU 8


cutadapt -a AGATCGGAAGAGC -A AGATCGGAAGAGC -q 30 -m 20 –trim-n -O 10 -o SRR2061397_1trimmed.fastq -p SRR2061397_2trimmed.fasq  SRR2061397_1.fastq SRR2061397_2.fastq
fastp -i SRR2061397_1.fastq -I SRR2061397_2.fastq -o SRR2061397_1clean.fastq -O SRR2061397_2clean.fastq
fastx_clipper -a AGATCGGAAGAGC -l 25 -d 0 -Q 33 -i SRR2061397_1.fastq -o\ SRR2061397_1trimmed.fastq
