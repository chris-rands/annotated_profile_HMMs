# annotated_profile_HMMs
Sets of protein familes represented as profile HMMs annotated for antibiotic resistance and virulence function.

## Description and methods

Each sub-directory contains a catalogue of HMMs and some corresonding `.txt`files that describe the profile HMMs. There is also a `.pdf` file that shows how the gathering (GA) thresholds were set for each HMM.

Profile HMMs were constructed by first clustering the initial sequence databases using [CD-hit](http://weizhongli-lab.org/cd-hit/) at 40% sequence identity, then aligning sequences with [ClustalOmega](http://www.clustal.org/omega/), trimming multiple sequence alignments with [TrimAl](http://trimal.cgenomics.org/), and building HMMs with [HMMBuild](http://hmmer.org/). Subsequently, all input proteins were scanned against the HMMs and for each HMM a model-specific bitscore threshold (GA) was set based on the distribution of bitscores for the sequences that were used to build the original model. Specifically, the threshold was set so that any sequences were be called as homologous to those in the profile HMM if the bitscore hit against the HMM was greater than or equal to the mean - 2 sigma of bitscores from the sequences used to build the HMMs (i.e. the known true positive sequences).

### Antibiotic resistance ![figure 1](https://github.com/chris-rands/annotated_profile_HMMs/blob/master/figures/ar_profile_hmm_figs.png)
Profile HMMs annotated for antibiotic resistance. a) Overlap at 100% sequence identity of the three databases used as inputs for the pipeline to build the HMMs. b) An example from a single HMM where the bitscores are shown for scanning the sequences used to build the HMM (i.e. the true positive sequences) and the sequences used to build other HMMs (possibly true negatives, although may be part of the subfamilies). The model-specific bitscore threshold (gathering threshold; GA), was calculated based on the ‘true positives’ only. c) The number of HMMs for each class of antibiotic.

### Virulence ![figure 2](https://github.com/chris-rands/annotated_profile_HMMs/blob/master/figures/virluence_profile_hmms_figs.png)
Profile HMMs annotated for antibiotic resistance. a) Overlap at 100% sequence identity of the 2 databases used as inputs for the pipeline to build the HMMs; VFDB is a subset of VirulenceFinder. b) An example from a single HMM where the bitscores are shown for scanning the sequences used to build the HMM (i.e. the true positive sequences) and the sequences used to build other HMMs (possibly true negatives, although may be part of the subfamilies). The model-specific bitscore threshold (gathering threshold; GA), was calculated based on the ‘true positives’ only. c) The number of HMMs for each type of virulenece protein.
