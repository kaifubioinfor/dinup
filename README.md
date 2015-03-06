# dinup
Home page for DiNuP (Differential Nucleosome Positioning)

dinup -t file A of nucleosome sequencing -c file B of nucleosome sequencing
dinup -- a systematic approach to identify regions of differential nucleosome positioning

Options:

--version                 show program's version number and exit.
-h, --help                show this help message and exit.
-t, --treatment=TFILE     input your treatment file. this version only supports BED format. (REQUIRED)
-c, --control=CFILE       input your control file. (REQUIRED)
-n, --name=NAME           experiment name, which will be used to generate output file names. DEFAULT: NA
-f, --feature             if specified, DiNuP will calculate physical features of identified regions.
-w, --windowsize=WINDOW   choose your sliding window size. DEFAULT:200 bp
--fdr=FDR                 use FDR as cutoff. DEFAULT:0.05
--pvalue=PVALUE           use input p-value as cutoff. DEFAULT:0.00001
--region=REGION           minimal length of identified region. DEFAULT:70 bp  
--format=FORMAT           this version only supports BED format.
--bias=BIAS               reduce experimental bias by given a coordinate disturbance.DEFAULT:3 bp
--time=TIMES              number of times to calculate K-S test and then take the average value. DEFAULT:3
--wig                     if speficied, DiNuP save significant p-values into wiggle file.
-a=asize                  set the average nucleosomal DNA length of sample A.DEFAULT:146bp
-b=bsize                  set the average nucleosomal DNA length of sample B.DEFAULT:146bp
--fold                    if specified, DiNuP will additionally use fold change method
--fcutoff=FCUTOFF         cutoff of fold change method. DEFAULT:2

Parameters

-t, --treatment FILENAME
This parameter provides one of the input file.  

-c, --control FILENAME
This parameter provides another input file. -t and -c are the only required parameters.  

-n, --name
The name string of the experiment. DiNuP will first create a directory named 
DiNuP_results under the directory of DiNuP package, then it will use this string
NAME to create output files like 'NAME_dinup.bed','NAME_dinup.xls','NAME_fold.bed'.
So please avoid any conflict between these filenames and your existing files.

-f, --feature
If specified, physical features will be provided to characterize the properties of
identified regions, including repositioned variation, occupancy change ratio between
–t file and –c file (for example, the ratio of 0.5 means nucleosome occupancy in
–t file is the half of that in –c file), and positioning degree change (for example,
the number of -0.3 means nucleosome positioning degree in –t file is smaller than
that in –c file). 

-w, --windowsize
The size of sliding window. Different window size may also have different results.
We recommend users to use 200 bp as window size since the average distance between
two nucleosomes is about 200 bp.

--fdr FDR
The false discovery rate cutoff. FDR is empirically estimated by DiNuP using a
simulation method. We recommend users to use FDR as cutoff when users have no idea
about how to set a p-value cutoff. 

--pvalue PVALUE
The p-value cutoff. Besides FDR cutoff, the user is able to set a p-value cutoff.
If p-value cutoff is preferred, please use --pvalue and disable --fdr.

--region REGION
Minimal length of identified differential nucleosome positioning regions. Regions
with at least given length will be identified as output results. Default:70 bp.

--format FORMAT
Format of input file. This version only supports BED format. The BED format is defined
in "http://genome.ucsc.edu/FAQ/FAQformat#format1"
            
--bias BIAS
Simulation of experimental bias. Experimental bias (bias of MNase, PCR or sequencing)
may result in false positive regions, we thus use coordinate disturbances to reduce
such bias.

--time TIMES
Number of times to calculate K-S test. Since we introduce coordinate disturbances,
DiNuP will calculate p-value significance at a given time and use the average p-value.
          
--wig
If specified, DiNuP will save significant p-values in wiggle files for each chromosome.
The WIG format is defined in "http://genome.ucsc.edu/goldenPath/help/wiggle.html"

-a,-b ASIZE,BSIZE
Set average nucleosomal DNA length. DEFAULT:146bp

--fold
If specified, DiNuP will additionally use fold change method to calculate occupancy
change (i.e., reads number change) regions. 

--fcutoff FCUTOFF
The cutoff of fold change method. DEFAULT: 2.

Output

1. BED file. This file contains genomic coordinates, effective width and p-value for 
each identified differential nucleosome positioning regions. 

2. BED file (fold change). This file contains genomic coordinates, effective width and
occupancy change for each identified nucleosome occupancy change regions based on fold
change method.

3. XLS file. This file contains genomic coordinates, effective width, p-value and
summits for each identified region. If -f is specified, this file will
additional contain occupancy change, repositioned variation and positioning
degree change.

4. WIG file. This file contains significant p-values. Values has been transformed
to -10*log10(p-value).

Note:
Because DiNuP recognizes chromosomal information automatically solely based on input
data, users do not need to specify the species. If input file size is too large, DiNuP
may require lots of EMS memory. An efficient way is to split your input files into
chromosomes, then use files of each chromosome to run DiNuP.






