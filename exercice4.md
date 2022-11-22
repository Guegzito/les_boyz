![Ceci est un exemple d'image](https://example.com/bild.jpg)

###                                                      Un document d'exemple

<ol>
    <li>item</li>
    <li>item</li>
    <li>item</li>
</ol>

> okay trop fun

```bash
RAD_7	56	loc7_pos55	C	T	13	PASS	NS=2;DP=32	GT:DP:CATG	0/0:10:9,0,1,0	./.:7:6,0,1,0	1/0:15:11,0,4,0
RAD_8	16	loc8_pos15	C	A	13	PASS	NS=2;DP=26	GT:DP:CATG	0/1:6:2,4,0,0	./.:11:9,2,0,0	0/0:9:9,0,0,0
RAD_8	25	loc8_pos24	G	A	13	PASS	NS=2;DP=26	GT:DP:CATG	0/1:6:0,4,0,2	./.:11:0,2,0,9	0/0:9:0,0,0,9
RAD_8	55	loc8_pos54	G	T	13	PASS	NS=2;DP=26	GT:DP:CATG	0/1:6:0,0,4,2	./.:11:0,0,2,9	0/0:9:0,0,0,9
RAD_14	65	loc14_pos64	A	C	13	PASS	NS=3;DP=24	GT:DP:CATG	0/0:8:0,8,0,0	1/0:6:2,4,0,0	0/0:10:1,9,0,0
RAD_14	68	loc14_pos67	A	C	13	PASS	NS=1;DP=24	GT:DP:CATG	./.:8:1,6,0,1	1/0:6:2,4,0,0	./.:10:2,8,0,0
RAD_16	3	loc16_pos2	G	T	13	PASS	NS=1;DP=31	GT:DP:CATG	./.:9:0,0,7,2	0/1:14:0,0,11,3	./.:8:0,0,7,1
RAD_17	13	loc17_pos12	A	C	13	PASS	NS=1;DP=25	GT:DP:CATG	./.:9:7,2,0,0	1/0:6:3,3,0,0	./.:10:8,2,0,0
RAD_24	12	loc24_pos11	C	T	13	PASS	NS=1;DP=75	GT:DP:CATG	1/0:30:8,0,22,0	./.:23:3,0,20,0	./.:22:3,0,19,0
RAD_24	15	loc24_pos14	G	C	13	PASS	NS=3;DP=75	GT:DP:CATG	0/0:30:1,0,0,29	0/1:23:4,0,0,19	0/0:22:0,0,0,22
RAD_24	22	loc24_pos21	A	T	13	PASS	NS=1;DP=75	GT:DP:CATG	1/0:30:0,8,22,0	./.:23:0,3,20,0	./.:22:0,3,19,0
RAD_26	9	loc26_pos8	T	G	13	PASS	NS=3;DP=23	GT:DP:CATG	0/0:10:0,0,9,1	1/0:7:0,0,5,2	0/0:6:0,0,6,0
RAD_26	56	loc26_pos55	T	C	13	PASS	NS=3;DP=23	GT:DP:CATG	0/0:10:1,0,9,0	0/1:7:2,0,5,0	0/0:6:0,0,6,0
RAD_30	24	loc30_pos23	A	G	13	PASS	NS=2;DP=35	GT:DP:CATG	./.:12:0,10,0,2	0/0:6:0,6,0,0	1/0:17:0,9,1,7
RAD_30	55	loc30_pos54	T	C	13	PASS	NS=2;DP=35	GT:DP:CATG	./.:12:2,0,10,0	0/0:6:0,0,6,0	0/1:17:7,0,9,1
RAD_32	17	loc32_pos16	T	G	13	PASS	NS=2;DP=87	GT:DP:CATG	./.:29:0,0,25,4	1/0:36:0,0,28,8	0/0:22:0,0,20,2
RAD_35	26	loc35_pos25	A	G
```

```bash
head pedicularis.vcf
```

```bash
cat pedicularis.vcf | tail -n +12 $1 >> pedicularislevrai.vcf
```

```bash
head pedicularislevrai.vcf
```

```bash
LOC=$(cut -f 1 ./pedicularislevrai.vcf)
```

```bash
POS=$(cut -f 2 ./pedicularislevrai.vcf)
```

```bash
ind1=$(cut -f 10 ./pedicularislevrai.vcf | cut -d ':' -f 3 | sed "s/10/1/g" |sed "s/20/1/g" | sed "s/30/1/g" | sed "s/40/1/g" | sed "s/1/ /g" | sed "s/2/ /g" | sed "s/3/ /g" | sed "s/4/ /g" | sed "s/5/ /g" | sed "s/6/ /g" | sed "s/7/ /g" | sed "s/8/ /g" | sed "s/9/ /g" | sed "s/,/ /g" | sed "s/ //g" | awk '{ print length-4 }' | sed "s/-/ /g" | sed "s/ //g" )
```

```bash
ind2=$(cut -f 11 ./pedicularislevrai.vcf | cut -d ':' -f 3 | sed "s/10/1/g" |sed "s/20/1/g" | sed "s/30/1/g" | sed "s/40/1/g" | sed "s/1/ /g" | sed "s/2/ /g" | sed "s/3/ /g" | sed "s/4/ /g" | sed "s/5/ /g" | sed "s/6/ /g" | sed "s/7/ /g" | sed "s/8/ /g" | sed "s/9/ /g" | sed "s/,/ /g" | sed "s/ //g" | awk '{ print length-4 }' | sed "s/-/ /g" | sed "s/ //g" )
```

```bash
ind3=$(cut -f 12 ./pedicularislevrai.vcf | cut -d ':' -f 3 | sed "s/10/1/g" |sed "s/20/1/g" | sed "s/30/1/g" | sed "s/40/1/g" | sed "s/1/ /g" | sed "s/2/ /g" | sed "s/3/ /g" | sed "s/4/ /g" | sed "s/5/ /g" | sed "s/6/ /g" | sed "s/7/ /g" | sed "s/8/ /g" | sed "s/9/ /g" | sed "s/,/ /g" | sed "s/ //g" | awk '{ print length-4 }' | sed "s/-/ /g" | sed "s/ //g" )
```

```bash
inter=$(cut -f 5 ./pedicularislevrai.vcf | sed "s/,/ /g" | sed "s/ //g" | awk '{ print length+1 }' )
```

```bash
paste <(echo "${LOC}") <(echo "${POS}") <(echo "${ind1}") <(echo "${ind2}") <(echo "${ind3}") <(echo "${inter}") >>final.txt
```

```bash
(echo -e "LOC    POS   trancheaa  trancheab  trancheac  INTER" ; cat final.txt) >final2.txt
```

```bash
cat final2.txt
```

```bash
grep 0 final.txt
```


#*exercice 5*

```{r}
#' iPyrad alleles.loci file to fasta alignments conversion
#' @description Converts iPyrad alleles.loci file to fasta alignmets.
#'              The alleles.loci is a specific iPyrad format that contains the phased alleles for all loci.
#'              To get this file use the * option in the output_formats parameter of iPyrad.
#' @param alleles.loci The name of the alleles.loci file as a character string. The alleles.loci file must be in the working directory.
#' @param output.dir The path to the output directory to write the fasta alignments.
#' @return Writes one fasta alignment per locus in the output.dir
#' @author Marcelo Gehara (Thanks Gustavo Cabanne for the help)
#' @export
iPyrad.alleles.loci2fasta <- function(alleles.loci, output.dir){
  
  x <- readLines(alleles.loci)
  setwd("~/ipyrad/rawdata/filtered/analysis/pedicularis_outfiles/exercice5")
  breaks <- grep("//",x)
  z <- 1
  for(i in 1:length(breaks)){
    fas <- x[z:(breaks[i]-1)]
    fas <-sapply(fas,strsplit," ")
    fas2 <- NULL
    for(j in 1:length(fas)){
      y <- paste(">",fas[[j]][1],sep="")
      y <- c(y, fas[[j]][length(fas[[j]])])
      fas2 <- c(fas2,y)
    }
    nam <- strsplit(x[breaks[i]],"|")[[1]]
    nam <- nam[grep("|",nam, fixed=T)[1]:grep("|",nam, fixed=T)[2]]
    nam <- gsub("|","",nam, fixed=T)
    nam <- paste(nam, collapse="")
    write(paste(fas2, sep="\n"), paste("locus_",nam,".fasta",sep=""))
    z <- 1+breaks[i]
    print(paste("locus_",nam,".fasta",sep=""))
  }
  
}
iPyrad.alleles.loci2fasta( alleles.loci = "pedicularis.loci", output.dir = "exercice5")
```

#*appelez le script dans le terminale*

```bash
Rscript scriptexo5.R
