# annotated_profile_HMMs
Sets of protein familes represented as profile HMMs annotated for antibiotic resistance (AR) and virulence function.

## Description and usage

Each sub-directory contains a catalogue of HMMs and some corresponding `.txt`files that describe the profile HMMs. There is also a `.pdf` file that shows how the gathering (GA) thresholds were set for each HMM.

The profile HMMs can be scaned with [HMMER3](http://hmmer.org/) to identify likely AR or virulence protein sequences. It is recommend that the scans are running using the model-specific gathering thresholds, using the `--cut_ga` flag, for example:

    cat hmms/*.hmm > all.hmm
    hmmsearch --cut_ga --cpu 1 --tblout output.table all.hmm target.faa

Note: The HMMs only include genes where presence or absence of the gene causes the resistance/virulence phenotype. Therefore, genes are not detected where only specific mutations (SNPs or indels) underly the phenotype as these will require a different approach to detect. The HMMs are recommended for research and exploratory studies and not validated for clinical use.

## Methods overview

The initial sequencing databases were [card](https://card.mcmaster.ca/) 1.1.3 homolog, [ResFinder](https://cge.cbs.dtu.dk/services/ResFinder/) 2.1, and [ResFinderFG](https://cge.cbs.dtu.dk/services/ResFinderFG/) 1.0 antibiotic resistance sequences, and [VFDB](http://www.mgc.ac.cn/VFs/) July 2017 and [VirulenceFinder](https://cge.cbs.dtu.dk/services/VirulenceFinder/) 1.5 virulence sequences. Profile HMMs were constructed by first clustering these sequence databases using [CD-hit](http://weizhongli-lab.org/cd-hit/) at 40% sequence identity, then aligning sequences with [ClustalOmega](http://www.clustal.org/omega/), trimming multiple sequence alignments with [TrimAl](http://trimal.cgenomics.org/), and building HMMs with [HMMBuild](http://hmmer.org/). Subsequently, all input proteins were scanned against the HMMs with HMMsearch and for each HMM a model-specific bitscore threshold (gathering threshold; GA) was set based on the distribution of bitscores for the sequences that were used to build the original model. Specifically, the threshold was set so that any sequences were be called as homologous to those in the profile HMM if the bitscore hit against the HMM was greater than or equal to the mean - 2 sigma of bitscores from the sequences used to build the HMMs (i.e. the known true positive sequences).
