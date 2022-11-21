
```bash
cat pedicularis.vcf | tail -n +12 $1 >> pedicularislevrai.vcf
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
