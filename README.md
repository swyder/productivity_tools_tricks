## Sharing productivity tools and tricks

## July 12, 2018


### University of Zurich
### URPP Evolution in Action
![URPP logo](Logo_URPP_kl2.png)

Stefan Wyder  
stefan.wyder@uzh.ch  
Carla Bello  
carla.bello@ieu.uzh.ch  
  
  
## bioawk

[Bioawk](bioawk.md) is an extension to awk, adding the support of several common biological data formats, including optionally gzip'ed BED, GFF, SAM, VCF, FASTA/Q and TAB-delimited formats with column names.
It also adds a few handy functions.

## Some command line tricks

[command line tricks](commandline_tricks.md) is a personal collection of useful (hopefully) less known command line tricks.

## GNU datamash

Carla shows us GNU datamash, a command-line program to perform table modifications, calculations and basic stats using text files as an input.  
[Presentation](https://github.com/carlalbc/URPP_tutorials/blob/master/Productivity%20tools%20II_%20Datamash.pdf)  [Exercises](https://github.com/carlalbc/URPP_tutorials/blob/master/Productivity_tools_GNUdatamash.md)

## Contributions from participants

### Docker

Glauco gave a short intro to [Docker](https://www.docker.com/) which is useful for creating and archiving computing environments. He recommended [this article](https://www.molecularecologist.com/2016/05/docker-making-our-bioinformatics-easier-and-more-reproducible/).   
[Biocontainers](https://biocontainers.pro/) is writing up dockerfiles of software commonly used in bioinformatics (see examples [here](https://cyverse-container-camp-workshop-2018.readthedocs-hosted.com/en/latest/biocontainer/biocontainers.html))

### Data.table

Michele presents the R package `data.table` with its main functions `fread` and `fwrite`:  super fast multi-threaded reading and writing of delimited text files.

### cowplot

Michele presents the R package `cowplot`, an add-on to `ggplot2` which provides a publication-ready theme and a function to arrange multiple plots together. 

### alias

Carla shows us some aliases she has in her ~/.bashrc :    
alias h='head'  
alias ..='cd ..'  
alias awktab="awk -v ''OFS=backslash tab"  

### column

Carla shows us the column command  
cat file.tsv | column -ts  
aligns tab-separated columns on the screen  


