Custom Scripts for Ho et al. Genome Research 2017 include annotation and analyses programs written in bash, Ruby, R, and Python
Dependencies include Ruby 2.0, and bedtools v2.25.0 (Quinlan and Hall 2010), R (version 3.1), Python 2.7, and optionally, MEME Suite for motif analysis and pyBedTools for permutation analysis (Dale et al. 2011)
ce10 genome data was downloaded from UCSC genome browser and WS241 gene models from Wormbase

*************** Annotation of DHSs ***************
The annotation program/ subfolder contains annotation program scripts
The 13576to14140_annotation_v4/ subfolder contains embryo and L1 annotation analyses and scripts
The text file WormbaseMotifs2013+PromoterMotifsv3.txt lists PWM motifs for C. elegans TF motifs curated by Wormbase and authors in MEME format.
IDR peaks/ subfolder contains peaks in BED format output resulting from running raw HOTSPOT peak data through the IDR framework from ENCODE Project. These are the original DHS peaks that are input into our annotation program.

(1) In the embryo and L1 annotation folders, the shell scripts embryoannotation_NCscores.sh and L1annotation_NCscores.sh are used to identify noncoding DHS from comparison of DHS peak data to Wormbase gene models and annotate these DHSs to the nearest gene. These scripts generate data in the Step1,2,3 folders to create the annotation files.

(2) Then, shell scripts L1noncodinganalysis_trimJuly2014.sh and noncodinganalysis_trimJuly2014_WormbaseMotifsv3_scores.sh take the annotation files and use them to further annotate noncoding DHSs into  categories of promoter(<=300bp to nearest gene), intron, and intergenic (>300bp to nearest gene) DHSs. In the case of the embryo script, additional DNA motif analysis is performed using DREME and motifs are compared to known motifs (using Wormbase curated PWM data in MEME format) using TOMTOM. DREME AND TOMTOM are both in the MEME analysis suite (available at http://meme-suite.org/).

(3) The footprintanalysis/ folders contain TF footprint data that we generated using DNase2TF and further analyzed with MEME using the footprintanalysis.sh scripts for each of L1 and embryo datasets.

(4) Preparation to analyse GO data from embryo noncoding DHS motifs is performed in GOanalysisofNoncodingMotifsv2.sh and AmiGO (http://amigo.geneontology.org/amigo). Analysis is parsed with GOsignificant.rb run on every AmiGO result for the motif using GOsignificant.sh. Further analysis of GO terms is performed with ReviGO (using website (http://revigo.irb.hr/)

*************** Comparison with modENCODE and other data ***************
Statistics and analysis scripts comparing overlap embryo noncoding DHSs with modENCODE data are in STATISTICS/ folder

intersections.sh is used to measure overlap between DHSs and modENCODE data (Gerstein et al. 2010; HOT regions, CBP-1, H3K4me3, RNAPII ChIP binding data) and TSS data (Chen et al 2013)

intersection_shuffle_MH.py is used to perform permutation analyses using pyBedTools and Python

intersections.R is used to perform statistical analysis using R

intersections_EmbryononcodingDHS.R is used to compare observed intersection/overlap between embryo noncoding DHS with known TSS and modENCODE features (i.e. CBP-1, H3K4me3, HOT regions, RNAPII) compared to 10,000 randomly shuffled permutations of embryo noncoding DHSs

Conservation analysis scripts are in the conservation/ subfolder:
embryo_NONCODINGONLY_TRIM.phyloP_stats.R is used to calculate observed phyloP conservation scores and to perform statistical tests as compared to 10,000 randomly shuffled permutations of embryo noncoding DHSs

Expression/ subfolder contains scripts and analysis for embryo expression of genes associated with embryo noncoding DHSs using modENCODE embryo expression data from Gerstein et al. 2010:
Embryo expression analysis of genes associated with embryo noncoding DHSs with differing numbers of marks is analyzed in ExpressionAnalysis_howmanymarks.sh
Embryo expression analysis of genes associated with varying number of embryo noncoding DHSs per gene is analyzed in ExpressionAnalysis_NumberNoncodingPeaks.sh
Statistics and graphs were generated with R script ExpressionAnalysis.R

*************** Comparative Analysis between L1 and Embryo noncoding DHSs ***************

The L1vsEmbryoNCDHS/ subfolder includes analyses of L1 Arrest Associated DHSs (that are observed in L1 arrest but not embryo):
These are identifed and analyzed using L1enhancersnotinEmbryo.sh script with BedTools and MEME
The compare_L1noncodingonly_Zhong2010_PHA-4_L1Starved.rb script is used to match L1 arrest footprints in these L1 Arrest Associated DHSs

The script compare_L1noncodingonly_Zhong2010_PHA-4_L1Starved is used to study the overlap/intersections between L1 Arrest Associated DHSs and PHA-4 ChIP binding sites (Zhong et al. 2010). Statistics are computed using R scripts in PHA4intersections/

The script VennDiagram_L1intersections_five.rb script is  used to identify overlap/intersections betwen L1 Arrest Associated DHSs and other L1 arrest relevant genes (i.e. genes regulated by DAF-16, PHA-4 upregulated in response to starvation, those more highly expressed in L1 vs embryo)
Statistics are computed using VennDiagram_L1intersections_L1noncoding.R

Comparison of genes associated with L1 arrest vs embryo noncoding DHSs using L1 arrest and embryo expression datasets from Baugh et al. 2009 is analyzed using compare_L1noncodingonly_vs_L1noncodingall_noncodingDHS_expression_revised.rb and graphed using compare_L1noncodingonly_vs_L1noncodingall_noncodingDHS_expression_revised.R
