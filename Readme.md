Citation: Andrew Dopheide, Leah K. Tooman, Stefanie Grosser, Barbara Agabiti, Birgit Rhode, Dong Xie, Mark I. Stevens, Nicola Nelson, Alexei J. Drummond, Thomas R. Buckley, and Richard D. Newcomb, 2018. **Estimating the biodiversity of terrestrial invertebrates on a temperate forested island using DNA barcodes and metabarcoding data.**

The invertebrate barcode sequences are available from Genbank under accessions KP420745 - KP422464 (COI barcodes) and KT439401 - KT440856 (28S barcodes). The sequences used in this analysis are included in this repository ("COI_1611_barcode_sequences.fasta" and "28S_1282_barcode_sequences.fasta" in "Invert_DNA_barcode_data/"). 

The soil DNA metabarcoding data is a subset of the multigene metabarcoding dataset generated by Drummond et al., 2015. Evaluating a multigene environmental DNA approach for biodiversity assessment. GigaScience, 4(1), 46. http://doi.org/10.1186/s13742-015-0086-1. 

**Analysis steps:**
+ The COI and 28S barcode sequences were processed into OTUs using the UCLUST algorithm in USEARCH v7 (Edgar, 2010) (usearch_pipeline.py). Alternatively, using VSEARCH (Rognes et al,. 2016) gave the same outcomes.
+ Analysis of DNA barcoding outcomes, and invertebrate biodiversity analyses based on the COI and 28S DNA barcode OTUs, were carried out using R (Invert_barcode_OTUs_analysis.R)
+ Invertebrate biodiversity on the island was estimated based on the COI and 28S DNA barcodes, and based on the soil DNA metabarcoding data, using SPECRICH2 (Rexstad & Burnham, 1991).
  + Occurrences of OTUs among samples for different taxonomic groups were determined using R (Invert_barcode_OTUs_analysis.R)
  + The occurrence data was entered into the estimator at http://www.mbr-pwrc.usgs.gov/software/specrich2.shtml.
+ Invertebrate biodiversity on the island was estimated by mark-recapture analysis of invertebrate COI barcode OTUs against soil DNA metabarcoding COI OTUs.
  + The invertebrate COI DNA barcode OTU sequences were split into taxonomic groups (split_fasta_by_taxa.py).
  + The 454 soil DNA metabarcoding COI OTU sequences were split into the same taxonomic groups (split_fasta_by_taxa.py)
  + The invertebrate COI barcode OTUs were matched against the soil DNA metabarcoding COI OTUs, for each taxonomic group, using the usearch_global algorithm in USEARCH (or VSEARCH) (usearch_match_seqs.py).
  + Biodiversity estimates for different taxonomic groups were calculated based on overlap of OTUs between the two datasets:

    N = (((K+1)\*(n+1))/(k+1))-1 (Chapman, 1951)

    Where K is the number of 454 soil DNA metabarcoding COI OTUs, n is the number of invertebrate COI DNA barcode OTUs, k is the number of matching OTUs between the two datasets.

+ New Zealand-wide invertebrate biodiversity was estimated by mark-recapture analysis of invertebrate COI barcode OTUs against BOLD database COI barcodes from New Zealand. 
  + COI barcode sequences derived from NZ invertebrate groups were extracted from the Barcoding of Life Database Public Data Portal, by entering as search terms "New Zealand" plus each of:
    - Arthropoda -Malacostraca -Trombidiformes -Sarcoptiformes -Mesostigmata -Ixodida -Trichoptera -Ephemeroptera -Plecoptera; (i.e. terrestrial arthropods excluding mites; resulting in 20,227 sequences)
    - Araneae Opiliones Pseudoscorpiones; (i.e. arachnids excluding mites; 718 sequences)
    - Chilopoda Diplopoda Pauropoda Symphyla; (i.e. myriapods; 14 sequences)
    - Insecta -Trichoptera -Ephemeroptera -Plecoptera; (i.e. terrestrial insects; 18,193 sequences)
    - Coleoptera; (1,304 sequences)
    - Diptera; (9,819 sequences)
    - Lepidotera; (1,162 sequences)
    - Hymenoptera; (4,137 sequences)
    - Hemiptera; (1,540 sequences)
    - Orthoptera; (17 sequences)
  + Any dashes were stripped out of the downloaded sequences using regex (e.g. using Notepad++).
  + Many of the barcode sequences have been imported into BOLD from Genbank since their submission to Genbank. Therefore, to repeat the analysis, any of these Hauturu invertebrate barcode sequences should be removed from the downloaded BOLD sequences (remove_Hauturu_barcodes_from_BOLD.py). 
  + Each set of BOLD database-derived sequences was clustered into OTUs (usearch_pipeline.py)
  + The invertebrate COI barcode OTUs were matched against the the BOLD database-derived OTUs, for each taxonomic group, using the usearch_global algorithm in USEARCH (or VSEARCH) (usearch_match_seqs.py).
  + Biodiversity estimates for different taxonomic groups were calculated based on overlap of OTUs between the two datasets, as above. 

