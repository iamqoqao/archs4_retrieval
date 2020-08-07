# archs4_retrieval

Processing scripts for annotated RNA-seq metadata from the ARCHS4 database. See report.pdf for details and comments in jupyter notebooks.

Download the files necessary for main_input and auxiliary_input to the ./data folder:

`cd ./data`

`wget "https://s3.amazonaws.com/mssm-seq-matrix/human_matrix.h5"`

`wget --timestamping 'ftp://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz' -O hg38.fa.gz`

`gunzip hg38.fa.gz`

File descriptions:

> DE_analysis.r contains the differential expression anasysis r script with the procedure described in report.pdf.

> DE_save_fasta.ipynb imports the output of the previous script (the list of differentially expressed transcripts) and saves teir sequences in .fasta format in ./data/DE_AML_transcripts.

> auxiliary_input.ipynb imports the DE transcript names and sequences and constructs a table of levels of differentially expressed transcripts of interest across AML/random samples and stores the result in csv format in ./data/aux_AML_rand_49DE.csv (**the table is uploaded and doesn't need to be regenerated**)

> main_input.ipynb imports count files (transcript files across samples) from ./data/counts_AML.tsv and ./data/counts_RAN.tsv and calculates exon inclusion levels for labels, and stores gene sequences along with their names, acceptor and donor labels in a separate file for each sample. The files will be saved in ./data/AML_library/AMLi.txt or ./data/rand_library/RANi.txt. Each file will contain a number of genes for the region of interest specified in the "region" parameter of the notebook (for ex., chr22), for each gene there will be 4 lines: -> @header with the name of the gene -> sequence with 1000nt flanks (specified in the parameters section) -> acceptor labels: tuples separated by a comma, the first value is an index, the second value is the label value, all the other nonspecified cells contain zeros -> donor labels, same as acceptor. (**the input files need to be generated**)
