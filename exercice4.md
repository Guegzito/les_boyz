##                                                    TOP SECRET : Projet pedicularis

### Introduction 

```bash
#Les exercices ont été réalisés sur des fichiers .loci et .vcf obtenu via ipyrad sur des séquences d'Orobranches avec les paramètres ci dessous
------- ipyrad params file (v.0.9.85)-------------------------------------------
pedicularis                    ## [0] [assembly_name]: Assembly name. Used to name output directories for assembly steps
/home/2022LBISM2/e21803739/ipyrad/rawdata/filtered/analysis ## [1] [project_dir]: Project dir (made in curdir if not present)
                               ## [2] [raw_fastq_path]: Location of raw non-demultiplexed fastq files
                               ## [3] [barcodes_path]: Location of barcodes file
/home/2022LBISM2/e21803739/Documents/Downloads/tranche/x*.fastq  ## [4] [sorted_fastq_path]: Location of demultiplexed/sorted fastq files
denovo                         ## [5] [assembly_method]: Assembly method (denovo, reference)
                               ## [6] [reference_sequence]: Location of reference sequence file
rad                            ## [7] [datatype]: Datatype (see docs): rad, gbs, ddrad, etc.
TGCAG,                         ## [8] [restriction_overhang]: Restriction overhang (cut1,) or (cut1, cut2)
5                              ## [9] [max_low_qual_bases]: Max low quality base calls (Q<20) in a read
33                             ## [10] [phred_Qscore_offset]: phred Q score offset (33 is default and very standard)
*6*                              ## [11] [mindepth_statistical]: Min depth for statistical base calling
*6*                              ## [12] [mindepth_majrule]: Min depth for majority-rule base calling
10000                          ## [13] [maxdepth]: Max cluster depth within samples
*0.99*                           ## [14] [clust_threshold]: Clustering threshold for de novo assembly
0                              ## [15] [max_barcode_mismatch]: Max number of allowable mismatches in barcodes
2                              ## [16] [filter_adapters]: Filter for adapters/primers (1 or 2=stricter)
35                             ## [17] [filter_min_trim_len]: Min length of reads after adapter trim
2                              ## [18] [max_alleles_consens]: Max alleles per site in consensus sequences
0.05                           ## [19] [max_Ns_consens]: Max N's (uncalled bases) in consensus
0.05                           ## [20] [max_Hs_consens]: Max Hs (heterozygotes) in consensus
3                              ## [21] [min_samples_locus]: Min # samples per locus for output
0.2                            ## [22] [max_SNPs_locus]: Max # SNPs per locus
8                              ## [23] [max_Indels_locus]: Max # of indels per locus
0.5                            ## [24] [max_shared_Hs_locus]: Max # heterozygous sites per locus
0, 0, 0, 0                     ## [25] [trim_reads]: Trim raw read edges (R1>, <R1, R2>, <R2) (see docs)
0, 0, 0, 0                     ## [26] [trim_loci]: Trim locus edges (see docs) (R1>, <R1, R2>, <R2)
p, s, l, v                       ## [27] [output_formats]: Output formats (see docs)
                               ## [28] [pop_assign_file]: Path to population assignment file
                               ## [29] [reference_as_filter]: Reads mapped to this reference are removed in this step
```
			       
### Exercice 4 

Tout d'abord jetons un coup d'oeil au fichier pedicularis.vcf

```bash
head pedicularis.vcf

##fileformat=VCFv4.0
##fileDate=2022/11/18
##source=ipyrad_v.0.9.85
##reference=pseudo-reference (most common base at site)
##phasing=unphased
##INFO=<ID=NS,Number=1,Type=Integer,Description="Number of Samples With Data">
##INFO=<ID=DP,Number=1,Type=Integer,Description="Total Depth">
##FORMAT=<ID=GT,Number=1,Type=String,Description="Genotype">
##FORMAT=<ID=DP,Number=1,Type=Integer,Description="Read Depth">
##FORMAT=<ID=CATG,Number=1,Type=String,Description="Base Counts (CATG)">
#CHROM	POS	ID	REF	ALT	QUAL	FILTER	INFO	FORMAT	xaa	xab	xac
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
```

Nous allons enlever les premières lignes de la première colonne afin de n'avoir que les informations utiles à l'analyse des SNP

```bash
cat pedicularis.vcf | tail -n +12 $1 >> pedicularislevrai.vcf

cat pedicularis.vcf | tail -n +12 $1 >> pedicularislevrai.vcf
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
```

Maintenant commençons par stocker la colonne LOCUS dans une variable $LOC

```bash
LOC=$(cut -f 1 ./pedicularislevrai.vcf)
RAD_7
RAD_8
RAD_8
RAD_8
RAD_14
RAD_14
RAD_16
RAD_17
RAD_24
RAD_24
RAD_24
RAD_26
RAD_26
RAD_30
RAD_30
RAD_32
RAD_35
RAD_42
RAD_43
RAD_43
RAD_44

```
Stockons ensuite la colonne position dans une autre variable appelée $POS

```bash
POS=$(cut -f 2 ./pedicularislevrai.vcf)
```
Nous voulons ensuite connaitre le nombre d'allèle que chaque individu a par loci
- Pour cela nous allons subset la colonne correspondant à l'individu 
- Puis nous allons subset la troisième colonne en spécifiant que le séparateur est ':'; plutot habile car notre colonne est structurée comme ceci ```1/0:15:11,0,4,0```
- La stratégie est de soustraire à 4 le nombre de zéro et donc le nombre d'allèles inéxistantes pour ce SNP, pour cela nous allons remplacer tous les 10, 20, 30, 40, 50 par des 1, puis les 1-9 et les , par des ' ' avant de remplacer les ' ' par des ''.  

```bash
ind1=$(cut -f 10 ./pedicularislevrai.vcf | cut -d ':' -f 3 | sed "s/10/1/g" |sed "s/20/1/g" | sed "s/30/1/g" | sed "s/40/1/g" | sed "s/1/ /g" | sed "s/2/ /g" | sed "s/3/ /g" | sed "s/4/ /g" | sed "s/5/ /g" | sed "s/6/ /g" | sed "s/7/ /g" | sed "s/8/ /g" | sed "s/9/ /g" | sed "s/,/ /g" | sed "s/ //g" | awk '{ print length-4 }' | sed "s/-/ /g" | sed "s/ //g" )

2
2
2
2
1
3
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
1
2
2
2
2
2
2
2
2
2
2
2


```

```bash
ind2=$(cut -f 11 ./pedicularislevrai.vcf | cut -d ':' -f 3 | sed "s/10/1/g" |sed "s/20/1/g" | sed "s/30/1/g" | sed "s/40/1/g" | sed "s/1/ /g" | sed "s/2/ /g" | sed "s/3/ /g" | sed "s/4/ /g" | sed "s/5/ /g" | sed "s/6/ /g" | sed "s/7/ /g" | sed "s/8/ /g" | sed "s/9/ /g" | sed "s/,/ /g" | sed "s/ //g" | awk '{ print length-4 }' | sed "s/-/ /g" | sed "s/ //g" )
```

```bash
ind3=$(cut -f 12 ./pedicularislevrai.vcf | cut -d ':' -f 3 | sed "s/10/1/g" |sed "s/20/1/g" | sed "s/30/1/g" | sed "s/40/1/g" | sed "s/1/ /g" | sed "s/2/ /g" | sed "s/3/ /g" | sed "s/4/ /g" | sed "s/5/ /g" | sed "s/6/ /g" | sed "s/7/ /g" | sed "s/8/ /g" | sed "s/9/ /g" | sed "s/,/ /g" | sed "s/ //g" | awk '{ print length-4 }' | sed "s/-/ /g" | sed "s/ //g" )
```
Nous avons donc le nombre d'allèles intraspécifiques 
Place aux nombre d'allèles interspécifiques 

```bash
inter=$(cut -f 5 ./pedicularislevrai.vcf | sed "s/,/ /g" | sed "s/ //g" | awk '{ print length+1 }' )
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
2
#tout va bien étant donné qu'on a que des SNP :)
```
Nous regroupons maintenant nos variables avant des les invoquer

```bash
paste <(echo "${LOC}") <(echo "${POS}") <(echo "${ind1}") <(echo "${ind2}") <(echo "${ind3}") <(echo "${inter}") >>final.txt
```

```bash
(echo -e "LOC    POS   trancheaa  trancheab  trancheac  INTER" ; cat final.txt) >final2.txt
```

```bash
barriere@barriere-ThinkPad-X220 ~/B/G/exo> ./youpi.sh ./pedicularis.vcf 
LOC    POS   trancheaa  trancheab  trancheac  INTER
RAD_7	56	2	2	2	2
RAD_8	16	2	2	1	2
RAD_8	25	2	2	1	2
RAD_8	55	2	2	1	2
RAD_14	65	1	2	2	2
RAD_14	68	3	2	2	2
RAD_16	3	2	2	2	2
RAD_17	13	2	2	2	2
RAD_24	12	2	2	2	2
RAD_24	15	2	2	1	2
RAD_24	22	2	2	2	2
RAD_26	9	2	2	1	2
RAD_26	56	2	2	1	2
RAD_30	24	2	1	3	2
RAD_30	55	2	1	3	2
RAD_32	17	2	2	2	2
RAD_35	26	2	2	2	2
RAD_42	65	2	2	2	2
RAD_43	4	2	2	2	2
RAD_43	38	2	2	2	2
RAD_44	53	2	2	2	2
RAD_99	63	1	2	2	2
```
Do you observe any loci with intra-individual genetic richness larger than two?

```bash
grep 0 final2.txt

RAD_14	68     *3*	2	2	2
RAD_16	3	2	2	2	2
RAD_17	13	2	2	2	2
RAD_30	24	2	1	3	2
RAD_30	55	2	1	3	2
RAD_32	17	2	2	2	2
RAD_35	26	2	2	2	2
RAD_43	4	2	2	2	2
RAD_43	38	2	2	2	2
RAD_44	53	2	2	2	2
RAD_99	63	1	2	2	2
RAD_112	34	2	2	2	2
RAD_128	31	2	2	2	2
RAD_129	13	2	2	2	2
RAD_129	35	2	2	2	2
RAD_131	59	2	2	1	2
RAD_138	55	2	2	2	2
RAD_143	23	2	2	2	2
RAD_143	26	2	2	2	2
RAD_146	63	2	2	2	2
RAD_153	30	2	2	2	2
RAD_153	50	2	2	2	2
RAD_155	13	2	2	2	2
RAD_161	33	2	2	2	2
RAD_168	35     *3*	2	3	2
RAD_168	53	3	3	3	2
RAD_171	53	2	2	2	2
RAD_180	63	2	2	2	2
RAD_181	53	2	2	2	2
RAD_192	33	2	2	2	2
RAD_196	34	2	2	2	2
RAD_207	36	1	2	2	2
RAD_218	63	2	2	2	2
RAD_236	46	2	1	2	2
RAD_293	1	2	2	2	2
RAD_301	41	2	2	2	2
RAD_306	44	2	2	2	2
RAD_308	60	2	2	2	2
RAD_308	62	2	2	2	2
RAD_309	66     *3*	3	3	2
RAD_312	21	2	2	2	2
RAD_312	40	2	2	2	2
RAD_315	18	2	2	2	2
RAD_315	57	2	2	2	2
RAD_315	59	2	2	2	2
RAD_317	39	2	2	2	2
RAD_330	27	1	2	2	2
RAD_339	10	1	2	2	2
RAD_339	29	1	2	2	2
RAD_339	39	1	2	2	2
RAD_339	57	1	2	2	2
RAD_340	11	2	2	2	2
RAD_340	39	2	2	2	2
RAD_340	43	2	2	2	2
RAD_342	40	2	2	2	2
RAD_348	2	2	2	2	2
RAD_350	67     *3*	2	2	2
RAD_371	34	2	2	2	2
RAD_372	50	2	2	2	2
RAD_372	69	2	2	2	2
RAD_376	26	2	2	2	2
RAD_376	53	2	2	2	2
RAD_379	68	2	2	1	2
RAD_381	42	2	2	2	2
RAD_382	18	2	2	2	2
RAD_382	26	2	2      *3*	2
RAD_386	2	2	2	2	2
RAD_386	59	2	2	2	2
RAD_386	66	2	2	2	2
RAD_388	51	2	2	2	2
RAD_389	45	2	2	2	2
RAD_390	10	2	2	2	2
RAD_405	35	1	2	1	2
RAD_409	30	1	2	1	2
RAD_463	19	2	1	1	2
RAD_463	35	2	1	1	2
RAD_481	3	2	2	2	2
RAD_14	68	3	2	2	2
RAD_16	3	2	2	2	2
RAD_17	13	2	2	2	2
RAD_30	24	2	1	3	2
RAD_30	55	2	1	3	2
RAD_32	17	2	2	2	2
RAD_35	26	2	2	2	2
RAD_43	4	2	2	2	2
RAD_43	38	2	2	2	2
RAD_44	53	2	2	2	2
RAD_99	63	1	2	2	2
RAD_112	34	2	2	2	2
RAD_128	31	2	2	2	2
RAD_129	13	2	2	2	2
RAD_129	35	2	2	2	2
RAD_131	59	2	2	1	2
RAD_138	55	2	2	2	2
RAD_143	23	2	2	2	2
RAD_143	26	2	2	2	2
RAD_146	63	2	2	2	2
RAD_153	30	2	2	2	2
RAD_153	50	2	2	2	2
RAD_155	13	2	2	2	2
RAD_161	33	2	2	2	2
RAD_168	35	*3*	2	*3*	2
RAD_168	53	*3*	*3*	*3*	2
RAD_171	53	2	2	2	2
RAD_180	63	2	2	2	2
RAD_181	53	2	2	2	2
RAD_192	33	2	2	2	2
RAD_196	34	2	2	2	2
RAD_207	36	1	2	2	2
RAD_218	63	2	2	2	2
RAD_236	46	2	1	2	2
RAD_293	1	2	2	2	2
RAD_301	41	2	2	2	2
RAD_306	44	2	2	2	2
RAD_308	60	2	2	2	2
RAD_308	62	2	2	2	2
RAD_309	66	3	3	3	2
RAD_312	21	2	2	2	2
RAD_312	40	2	2	2	2
RAD_315	18	2	2	2	2
RAD_315	57	2	2	2	2
RAD_315	59	2	2	2	2
RAD_317	39	2	2	2	2
RAD_330	27	1	2	2	2
RAD_339	10	1	2	2	2
RAD_339	29	1	2	2	2
RAD_339	39	1	2	2	2
RAD_339	57	1	2	2	2
RAD_340	11	2	2	2	2
RAD_340	39	2	2	2	2
RAD_340	43	2	2	2	2
RAD_342	40	2	2	2	2
RAD_348	2	2	2	2	2
RAD_350	67	*3*	2	2	2
RAD_371	34	2	2	2	2
RAD_372	50	2	2	2	2
RAD_372	69	2	2	2	2
RAD_376	26	2	2	2	2
RAD_376	53	2	2	2	2
RAD_379	68	2	2	1	2
RAD_381	42	2	2	2	2
RAD_382	18	2	2	2	2
RAD_382	26	2	2	3	2
RAD_386	2	2	2	2	2
RAD_386	59	2	2	2	2
RAD_386	66	2	2	2	2
RAD_388	51	2	2	2	2
RAD_389	45	2	2	2	2
RAD_390	10	2	2	2	2
RAD_405	35	1	2	1	2
RAD_409	30	1	2	1	2
RAD_463	19	2	1	1	2
RAD_463	35	2	1	1	2
RAD_481	3	2	2	2	2

```
The answer is 'YES'
Car nous n'avons pas bien réglé nos paramètres dans params_pedicularis.txt !!!!!


## Exercice 5

Pour commencer nous allons essayer de placer les identifiants des locis de manières à ce qu'ils apparaissent dans la sortie blastn

```bash
grep "//" pedicularis.loci | sed 's/-/ /g' | sed 's/*/ /g' | sed 's/\///g' | sed 's/\|/\n/' | tr -s " "  > ZEBIloci.txt
head ZEBIloci.txt 

 |0|

 |1|

 |2|

 |3|

 |4|
```

```bash
grep -E -i '(xaa|\/\/)' ./pedicularis.loci >> loci.txt
head loci.txt
xaa     GGGAATCTCCACTCACTGCTTCCCCTAATATCCTCCCTTTACCACATCATGGGGGTTTACAGGAGATCC
//                                                                           |0|
xaa     GTGGTGATTTCGATGGTTTTGATGGTGTCGTGGATTGGAATGATGTGCCTGGTGGTGATTTTGACGAGG
//                                                                           |1|
xaa     AAGCCTGCTTGTACAGGTTGCTCAACCCGGATCGAGCTGGCGGGGCGTCTTTGTCCGATTCATTGACTG
//                                                                           |2|
xaa     CAGCAGCTGGTGTTCGTGTTCGTGTTCGCGCCCTTTCGCCTTTGACGCAGCACAAGAAGAGTCAAAGTC
//                                                                           |3|
xaa     CCACCTTTNTTCCGGTGNTTTTTTTTTATCAATTTAAAAATATATTGGGAAATTTAGATTTGGTTTTATC
//                                                                            |4|
```

```bash
sed '1d' ./ZEBIloci.txt > ZEBIloci2.txt
head ZEBIloci2.txt 
 |0|

 |1|

 |2|

 |3|

 |4|
 ```
 
```bash
paste ZEBIloci2.txt loci.txt > ZERMA.loci
head ZERMA.loci
 |0|	xaa     GGGAATCTCCACTCACTGCTTCCCCTAATATCCTCCCTTTACCACATCATGGGGGTTTACAGGAGATCC
	//                                                                           |0|
 |1|	xaa     GTGGTGATTTCGATGGTTTTGATGGTGTCGTGGATTGGAATGATGTGCCTGGTGGTGATTTTGACGAGG
	//                                                                           |1|
 |2|	xaa     AAGCCTGCTTGTACAGGTTGCTCAACCCGGATCGAGCTGGCGGGGCGTCTTTGTCCGATTCATTGACTG
	//                                                                           |2|
 |3|	xaa     CAGCAGCTGGTGTTCGTGTTCGTGTTCGCGCCCTTTCGCCTTTGACGCAGCACAAGAAGAGTCAAAGTC
	//                                                                           |3|
 |4|	xaa     CCACCTTTNTTCCGGTGNTTTTTTTTTATCAATTTAAAAATATATTGGGAAATTTAGATTTGGTTTTATC
	//                                                                            |4|
```

On obtenait cette sortie 

```bash
|0|	xaa     GGGAATCTCCACTCACTGCTTCCCCTAATATCCTCCCTTTACCACATCATGGGGGTTTACAGGAGATCC
	//                                                                           |0|
 |1|	xaa     GTGGTGATTTCGATGGTTTTGATGGTGTCGTGGATTGGAATGATGTGCCTGGTGGTGATTTTGACGAGG
	//                                                                           |1|
 |2|	xaa     AAGCCTGCTTGTACAGGTTGCTCAACCCGGATCGAGCTGGCGGGGCGTCTTTGTCCGATTCATTGACTG
	//                                                                           |2|
 |3|	xaa     CAGCAGCTGGTGTTCGTGTTCGTGTTCGCGCCCTTTCGCCTTTGACGCAGCACAAGAAGAGTCAAAGTC
	//                                                                           |3|
 |4|	xaa     CCACCTTTNTTCCGGTGNTTTTTTTTTATCAATTTAAAAATATATTGGGAAATTTAGATTTGGTTTTATC
	//                                                                            |4|
 |5|	xaa     TTTTACTGCGCTTTTGAGGATATAAGACGCAAATTGAATCTCGTTCTTAGACCCACCAAATCCGTTGAT
	//                                                                           |5|
 ```
 
On a ensuite été confronté à un problème que l'ont a résolu en utilisant la bonne vieille touche effacer de notre clavier et on a obtenu cette sortie 

```bash
|0|	xaa     GGGAATCTCCACTCACTGCTTCCCCTAATATCCTCCCTTTACCACATCATGGGGGTTTACAGGAGATCC
//                                                                           |0|
|1|	xaa     GTGGTGATTTCGATGGTTTTGATGGTGTCGTGGATTGGAATGATGTGCCTGGTGGTGATTTTGACGAGG
//                                                                           |1|
|2|	xaa     AAGCCTGCTTGTACAGGTTGCTCAACCCGGATCGAGCTGGCGGGGCGTCTTTGTCCGATTCATTGACTG
//                                                                           |2|
|3|	xaa     CAGCAGCTGGTGTTCGTGTTCGTGTTCGCGCCCTTTCGCCTTTGACGCAGCACAAGAAGAGTCAAAGTC
//                                                                           |3|
|4|	xaa     CCACCTTTNTTCCGGTGNTTTTTTTTTATCAATTTAAAAATATATTGGGAAATTTAGATTTGGTTTTATC
//                                                                            |4|
|5|	xaa     TTTTACTGCGCTTTTGAGGATATAAGACGCAAATTGAATCTCGTTCTTAGACCCACCAAATCCGTTGAT
//                                                                           |5|
 ```

*Transformation du .loci en .fasta* 

#*appelez le script dans le terminal*

```bash
Rscript scriptexo5.R
```
#Le script en question

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
Création de la banque de données 

téléchargement de ITS_eukaryote_sequences.tar.gz LSU_eukaryote_rRNA.tar.gz SSU_eukaryote_rRNA.tar.gz

création de la banque de données regroupant toutes les séquences ribosomales d'eucaryotes 

```bash
blastdb_aliastool -dblist "SSU_eukaryote_rRNA LSU_eukaryote_rRNA ITS_eukaryote_sequences" -dbtype nucl -out ribosome_all -title "pedicularis ribosome"

cat ./ribosome_all.nal
#
# Alias file created 11/22/2022 13:20:53
#
TITLE pedicularis ribosome
DBLIST "SSU_eukaryote_rRNA" "LSU_eukaryote_rRNA" "ITS_eukaryote_sequences" 
NSEQ 90306
LENGTH 87778360
```
La commande blastn

```bash
blastn -db ribosome_all -query allfiles.fasta -max_target_seqs 1 -outfmt 6 > zebi2.txt
```
Le tableau qu'on obtient 

```bash
barriere@barriere-ThinkPad-X220 ~/B/G/b/ALL> cat zebi2.txt
|56|	KM213403.1	100.000	69	0	0	1	69	5728	5796	8.15e-30	128
|162|	AY189043.1	100.000	68	0	0	2	69	121	54	2.93e-29	126
|241|	U38314.1	100.000	69	0	0	1	69	82	14	8.15e-30	128
|331|	U38314.1	100.000	69	0	0	1	69	929	861	8.15e-30	128
|337|	AY727943.1	100.000	69	0	0	1	69	2646	2714	8.15e-30	128
|370|	MT796508.1	100.000	47	0	0	1	47	620	666	7.36e-18	87.9
|397|	U38314.1	100.000	69	0	0	1	69	1334	1266	8.15e-30	128
```
Les loci 56, 162,241,331,337,370,397 sont donc des locis ribosomaux 
Soit une proportion de 7/120 soit ``` 5.8% ```

```bash
grep 'RAD_162' ./pedicularis.vcf
'RAD_162	58	1	2	2	2'
```
Seul le loci  162 a passé les filtres pour le .vcf, on ne peut donc pas en conclure grand chose 
