## Sharing productivity tools and tricks

## July 12, 2018


### University of Zurich
### URPP Evolution in Action
![URPP logo](Logo_URPP_kl2.png)

Stefan Wyder  
stefan.wyder@uzh.ch  

  
  
## bioawk

Bioawk is an extension to awk, adding the support of several common biological data formats, including optionally gzip'ed BED, GFF, SAM, VCF, FASTA/Q and TAB-delimited formats with column names.
It also adds a few handy functions.

### Installation

- Using Anaconda:
  ```{bash}
  conda install -c bioconda bioawk
  ```
- From source:
  ```{bash}
  git clone https://github.com/lh3/bioawk
  cd bioawk
  make
  ```

### Features

- It can automatically recognize and parse some popular bioinformatics formats.
  The format option is passed to bioawk using `-c filetype` flag. The format option is passed to bioawk using -carg flag. Here arg can be bed, sam, vcf, gff or fastx (for both fastq and FASTA).
- After parsing, values are parsed in these variables , e.g. for a FASTA file in $name and $sequence
```
bioawk -c help
bed:
	1:chrom 2:start 3:end 4:name 5:score 6:strand 7:thickstart 8:thickend 9:rgb 10:blockcount 11:blocksizes 12:blockstarts 
sam:
	1:qname 2:flag 3:rname 4:pos 5:mapq 6:cigar 7:rnext 8:pnext 9:tlen 10:seq 11:qual 
vcf:
	1:chrom 2:pos 3:id 4:ref 5:alt 6:qual 7:filter 8:info 
gff:
	1:seqname 2:source 3:feature 4:start 5:end 6:score 7:filter 8:strand 9:group 10:attribute 
fastx:
	1:name 2:seq 3:qual 4:comment
```
- several new functions specific for biological formats: `length`, `reverse`, `revcomp`, `trimq`, `gc`, `and`, `or`, `xor`
- it can automatically read gzipped/compressed files

### Options

- -t to set input and output filed separator as tab
- -c `filetype` to read and parse the file in desired format
- -H retain header in the output file (for files like SAM)
- and all standard awk flags will work with bioawk


### Examples

#### FASTA files

- List the supported formats:
  ```{bash}
  bioawk -c help
  ```

- Get length for FASTA sequences
  ```{bash}
  bioawk -c fastx '{print $name, length($seq)}' input.fasta
  ```  

- Print FASTA sequences longer than 10kb
  ```{bash}
  bioawk -c fastx '{if(length($seq) > 10000) {print ">"$name; print $seq}}' assembly.fasta
  ```

- Print FASTA sequences containing PREFIX
  ```{bash}
  bioawk -c fastx '$name ~/PREFIX/ {print ">"$name; print $seq)}' input.fasta
  ```
  
- Reverse complement FASTA
  ```{bash}
  bioawk -c fastx '{print ">"$name;print revcomp($seq)}' seq.fa.gz
  ```

- Extract all sequences STA file based on IDs supplied in a file
  ```{bash}
  bioawk -c fastx 'BEGIN {while((getline k <"IDs.txt")>0) i[k]=1} {if (i[$name]) print ">"$name"\n"$seq}' input.fasta
  ```

#### FASTQ files

- Trim fastq files based on quality
  ```{bash}
  # trims fastq bases 0 to 5 (beginning to end), scores less than 30.
  bioawk -c fastx ' trimq(30, 0, 5){print $0}' input.fastq
  ```

- Filter reads shorter than 10 bp
  ```{bash}
  bioawk -cfastx 'length($seq) > 10 {print "@"$name"\n"$seq"\n+\n"$qual}' input.fastq
  ```  

- Count all the reads in all FASTQ files
  ```{bash}
  for i in *.fastq.gz; do echo $i; bioawk -c fastx 'END {print NR}' $i; done
  ```

- Get the mean Phred quality score from a FASTQ file
  ```{bash}
  bioawk -c fastx '{print ">"$name; print meanqual($qual)}' input.fastq 
  ```

#### BED files

- Print the feature length
  ```{bash}
  bioawk -c bed '{ print $end - $start }' test.bed
  ```

#### SAM files

- Extract unmapped reads
  ```{bash}  
  bioawk -c sam 'and($flag,4)' input.sam
  ```

- Extract mapped reads
  ```{bash}
  bioawk -c sam -H '!and($flag,4)' input.sam
  ```

#### For other types of file

- When `-c header` is specified, the field names will used for variable names

  -----|-------|------|----
  name | phone |email |age
  -----|-------|------|----
  Jim  |6407   |a@g.com	| 24
  Tina |4506   |b@g.com	| 26

  ```{bash}
  bioawk -t -c header '$age < "25" {print $0}' input.txt
  ```

## Source

- https://gif.biotech.iastate.edu/bioawk-basics
