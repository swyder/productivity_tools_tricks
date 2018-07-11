## Sharing productivity tools and tricks

## July 12, 2018


### University of Zurich
### URPP Evolution in Action
![URPP logo](Logo_URPP_kl2.png)

Stefan Wyder  
stefan.wyder@uzh.ch  

  
  
## command line tricks

A collection of useful (hopefully) less known tricks in the command line.


## find file

- Find script Calc_Phylosignal in home directory and all subfolders  
  find ~ -name 'Calc_Phylosignal.R'

- Find all R script starting with "Calc_"  
  find ~ -name 'Calc_*.R'

- ignore case  
  find ~ -iname 'Calc_*.R'

- Find all directories (type d: directories, type f: files) on the system  
  find / -type d -name FASTQ

- Find Last 50 Days Modified Files (see also ctime)  
  find / -mtime 50

- Find all files larger than 100MB in the file system and list them in long format  
  find / -size +100M -exec ls -lh {} \; 2>/dev/null

## xargs

find ~ -name 'Readme*.txt' | xargs -i grep blat {}  
or shorter:  
find ~ -name 'Readme*.txt' | xargs -i grep blat  

use max 6 threads:  
cat sample_names.txt | xargs -P 6 -n 1 bash script.sh  
  
A very good alternative is GNU parallel:  
find . -name "pattern" | parallel --dry-run command option {} {}.out

## Handy for fall cleaning

`alias space='du -h --max-depth=1 . | sort -h'`

## Multi-threaded sorting

GNU sort can be run multi-threaded: `sort --parallel`

## Speed up grep for large files

1. Prefix your grep command with `LC_ALL=C` to use the C locale instead of UTF-8.    
2. Use fgrep if you're searching for a fixed string, not a regular expression   
  
from http://crazyhottommy.blogspot.com/2014/10/speed-up-grep.html  
  
## No folder structure with wget download

```-nd --no-directories```  
Do not create a hierarchy of directories when retrieving recursively. With this option turned on, all files will get saved to the current directory, without clobbering (if a name shows up more than once, the filenames will get extensions .n).

## ggplot2 Plotting from the command line

See this [ggplot2](https://www.datascienceatthecommandline.com/chapter-7-exploring-data.html#introducing-ggplot2) chapter from the book [Data science at the command line](https://github.com/jeroenjanssens/data-science-at-the-command-line) https://www.datascienceatthecommandline.com/chapter-7-exploring-data.html#introducing-ggplot2


- installation  
  wget https://raw.githubusercontent.com/jeroenjanssens/data-science-at-the-command-line/master/tools/Rio  
  chmod +x Rio  

- get data  
  curl -s 'https://raw.githubusercontent.com/pydata/pandas/master/pandas/tests/data/iris.csv' > iris.csv

- some examples:
  ```{bash}  
  seq 100 | ./Rio -ne 'sum(df)'  
  cat iris.csv | ./Rio -f summary  
  cat iris.csv | ./Rio -ge 'g+geom_point(aes(x=SepalLength,y=SepalWidth,colour=Name))' | display  
  cat iris.csv | ./Rio -ge 'g+geom_point(aes(x=SepalLength,y=SepalWidth,colour=Name))' > iris.png  
  ```  

### csvkit
[csvkit](https://csvkit.readthedocs.io) csvkit is a suite of command-line tools for converting to and working with CSV, the king of tabular file formats. 

- installation csvkit  
  Using Anaconda: conda install csvkit  
  or using pip: sudo pip install csvkit  


## Create an empty file in terminal
I am working mostly in the terminal and I don't like to change back and forth between keyboard and mouse

```{bash}
touch manuscript.docx  
# on Ubuntu  
libreoffice manuscript.docx  
# on Mac  
open manuscript.docx  
```

## Define a function in bash

```{bash}
# The () are only for decoration, we cannot pass arguments in parentheses
function_name () {
command...
} 
```
