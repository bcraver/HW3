# Homework 3
## Download _Drosophila melanogaster_ genome
Go to homework 3 directory  

	$ cd myrepos/HW3 
   	$ cd data/raw/  
   	$ wget ftp://ftp.flybase.net/genomes/Drosophila_
        melanogaster/current/fasta/dmel-all-chromosome-
        r6.24.fasta.gz

### Check file integrity
    $ md5sum dmel-all-chromosome-r6.23.fasta.gz  

71a25289ae2e630d5247856dc2a67ab1  dmel-all-chromosome- 
	r6.24.fasta.gz

### Unzip the file
	$ gunzip dmel-all-chromosome-r6.24.fasta.gz 

#### 1. Calculate total number of nucleotides
	$ module load jje/kent
	$ faSize dmel-all-chromosome-r6.24.fasta 
143726002 bases (1152978 N's 142573024 real 142573024 upper 0 lower) in 1870 sequences in 1 files  
Total size: mean 76858.8 sd 1382100.2 min 544 (211000022279089) max 32079331 (3R) median 1577  
N count: mean 616.6 sd 6960.7  
U count: mean 76242.3 sd 1379508.4  
L count: mean 0.0 sd 0.0  
%0.00 masked total, %0.00 masked real  

**Answer= 143726002 nucleotides**

#### 2. Calculate total number of N's
**Answer = 1152978 N's**

#### 3. Calculate total number of sequences 
**Answer = 1870 sequences**  

	$ grep -c "^>" dmel-all-chromosome-r6.24.fasta 
1870

### Summarize an annotation file  

# Download gtf file for _D. melanogaster_

	$ wget ftp://ftp.flybase.net/genomes/Drosophila_
	melanogaster/current/gtf/dmel-all-r6.24.gtf.gz

### Verify file integrity  

	$ md5sum dmel-all-r6.24.gtf.gz 
5cd5dcfbfff952ea7ce89e26cba89bbd  dmel-all-r6.24.gtf.gz

### Unzip the gtf file
	$ gunzip dmel-all-r6.24.gtf.gz  

The GTF format consists of one line per feature, each containing 9 columns of data. Column 3 contains features.  

# Print a summary report with the following information:  
1. Total number of features of each type, sorted from the most common to the least common  

		grep -v "^#" dmel-all-r6.24.gtf | \
		cut -f3 | \
		sort | \
		uniq -c | \
		sort -rn
	 
 187315 exon  
 161014 CDS  
  46339 5UTR  
  33358 3UTR  
  30591 start_codon  
  30533 stop_codon  
  30507 mRNA  
  17772 gene  
   2961 ncRNA  
    485 miRNA  
    334 pseudogene  
    312 tRNA  
    299 snoRNA  
    262 pre_miRNA  
    115 rRNA  
     32 snRNA  


2. Total number of genes per chromosome arm (X, Y, 2L, 2R, 3L, 3R, 4) #Chromosome name in field #1, genes are features in field #3.

		$ grep -v "^[#]" dmel-all-r6.24.gtf \
		| cut -f1 \
		| sort \
		| uniq -c \
		| sort -rn \
		| head -7  

 126710 3R  
 110522 2R  
 101180 3L  
  97543 X  
  97461 2L  
   7839 4  
    639 Y  

