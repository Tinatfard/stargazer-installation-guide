# Table of Contents
* [Setting up](#Setting-up)
* [Getting help](#Getting-help)
* [Logging](#Logging)









# Setting up


```
pip install pysam
```

Run Stargazer from the downloaded directory or alias it to the $HOME path 


# Getting help <a name="Getting-help"></a>

Enter the following:

```
python stargazer -h
```

To give:

```
usage:  [-h] [-v] [-i PATH] -o PATH -t TEXT [-a TEXT] [-d TEXT] [-c TEXT]
        [-g PATH] [-r PATH] [-s TEXT [TEXT ...]] [-p] [-b] [-st PATH]
        [-G NAME] [-B [LIST [LIST ...]]]

Stargazer is a bioinformatics tool for calling star alleles in pharmacogenes
using genomic data from next-generation sequencing or single nucleotide
polymorphism microarray. Required arguments are indicated with '[required]'.
In order to perform structural variation detection, you must provide both
'-c/--control-gene' and '-g/--gdf-file'. Otherwise, Stargazer will run in the
VCF-only mode. Stargazer switches to gdf-creation mode with '-G/--create-gdf-
file' argument. You must provide both '-c/--control-gene' and '-B/--bam-file. 
For more information, visit the official website:
https://stargazer.gs.washington.edu/stargazerweb.

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         Print the Stargazer version number and exit.
  -i PATH, --vcf-file PATH
                        Path to the input VCF file (.vcf or .vcf.gz). An empty
                        VCF file containing only the header and metadata is
                        still accepted by Stargazer as it means no variants
                        were detected from the sample(s). [required for
                        standard running]
  -o PATH, --output-dir PATH
                        Path to the output directory. If the directory with
                        the same name already exists, Stargazer will overwrite
                        it. [required for all processes]
  -t TEXT, --target-gene TEXT
                        Name of the target gene. Choices: {'abcb1', 'cacna1s',
                        'cftr', 'cyp1a1', 'cyp1a2', 'cyp1b1', 'cyp2a6',
                        'cyp2a13', 'cyp2b6', 'cyp2c8', 'cyp2c9', 'cyp2c19',
                        'cyp2d6', 'cyp2e1', 'cyp2f1', 'cyp2j2', 'cyp2r1',
                        'cyp2s1', 'cyp2w1', 'cyp3a4', 'cyp3a5', 'cyp3a7',
                        'cyp3a43', 'cyp4a11', 'cyp4a22', 'cyp4b1', 'cyp4f2',
                        'cyp17a1', 'cyp19a1', 'cyp26a1', 'dpyd', 'g6pd',
                        'gstm1', 'gstp1', 'ifnl3', 'nat1', 'nat2', 'nudt15',
                        'por', 'ptgis', 'ryr1', 'slc15a2', 'slc22a2',
                        'slco1b1', 'slco1b3', 'slco2b1', 'sult1a1', 'tbxas1',
                        'tpmt', 'ugt1a1', 'ugt1a4', 'ugt2b7', 'ugt2b15',
                        'ugt2b17', 'vkorc1', 'xpc', '2c_cluster', 'abcg2'}.
                        [required for all processes]
  -a TEXT, --genome-build TEXT
                        Build of the reference genome assembly used to create
                        the input data. Choices: {'hg19', 'grc38'}. [default:
                        'hg19']
  -d TEXT, --data-type TEXT
                        Type of the input data: wgs, whole genome sequencing;
                        ts, targeted sequencing including whole exome
                        sequencing; or chip, single nucleotide polymorphism
                        microarray. Choices: {'wgs', 'ts', 'chip'}. [default:
                        'wgs']
  -c TEXT, --control-gene TEXT
                        Name of a preselected control gene. Used for
                        intrasample normalization during copy number analysis.
                        Choices: {'egfr', 'ryr1', 'vdr'}. Alternatively, you
                        can provide a custom genomic region with the
                        'chr:start-end' format (e.g. chr12:48232319-48301814).
                        [required with --create-gdf-file]
  -g PATH, --gdf-file PATH
                        Path to a GDF file containing read depth for both the
                        target and control genes.
  -r PATH, --hap-panel PATH
                        Path to a reference haplotype panel file (.vcf or
                        .vcf.gz). By default, Stargazer uses the haplotype
                        panel from the 1000 Genomes Project (phase 3).
  -s TEXT [TEXT ...], --sample-list TEXT [TEXT ...]
                        List of space-delimited sample IDs to be used as
                        control for intersample normalization during copy
                        number analysis. This argument has an effect only when
                        the input data type is targeted sequencing.
  -p, --include-profiles
                        Use this tag to include profiles for read depth, copy
                        number, and allele fraction. This tag has no effect if
                        Stargazer is running in the VCF-only mode.
  -b, --impute-ungenotyped-markers
                        Use this tag to impute ungenotyped markers during
                        statistical phasing. Potentially useful for low-
                        density DNA microarray data.
  -st PATH, --star_table PATH
                        Use this tag to specify the path for star_table to be
                        used
  -G NAME, --create-gdf-file NAME
                        This tag causes Stargazer to run as a GDF-file
                        generator. Argument requires a file name (which will
                        be placed in the output directory).
  -B [LIST [LIST ...]], --bam-file [LIST [LIST ...]]
                        List of paths to BAM or CRAM files. [required for
                        --create-gdf-file runs]
```










# Logging <a name="Logging"></a>

Below is an example log from Stargazer.

```
[INFO] ----------------------------------------------------------------------
[INFO] Stargazer 1.0.9
[INFO] Author: Seung-been "Steven" Lee
[INFO] Enter 'python3 Stargazer -h' to view command line arguments
[INFO] For more details, please visit https://stargazer.gs.washington.edu/stargazerweb
[INFO] Date: 2021-01-20
[INFO] Start time: 18:58:56
[INFO] Command line: python3 /Users/sbslee/opt/anaconda3/envs/pypgx/bin/stargazer -o getrm-cyp2d6-vdr -d wgs -t cyp2d6 -c vdr -i getrm-cyp2d6-vdr.joint.filtered.vcf -g getrm-cyp2d6-vdr.gdf -p
[INFO] ----------------------------------------------------------------------
[INFO] ----------------------------------------------------------------------
[INFO] Step 1/9: Determining genotype mode...
[INFO] Target gene: CYP2D6
[INFO] Target paralog: CYP2D7
[INFO] Target region: chr22:42512500-42551883
[INFO] Control gene: VDR
[INFO] Control region: chr12:48232319-48301814
[INFO] Input data source: Whole genome sequencing
[INFO] VCF-only mode is turned on: False
[INFO] Impute ungenotyped markers: False
[INFO] Finished determining genotype mode
[INFO] ----------------------------------------------------------------------
[INFO] ----------------------------------------------------------------------
[INFO] Step 2/9: Assessing input VCF file...
[INFO] Samples total: 70
[INFO] Markers total: 555
[INFO] Markers with allelic depth: 555
[INFO] Markers unphased: 555
[INFO] Markers phased: 0
[INFO] Markers partially phased: 0
[INFO] Finished assessing input VCF file
[INFO] ----------------------------------------------------------------------
[INFO] ----------------------------------------------------------------------
[INFO] Step 3/9: Processing input VCF...
[INFO] Markers with allelic imbalance: 44
[INFO] Markers with high missingness: 1
[INFO] Markers with invalid allele: 0
[INFO] Finished processing input VCF
[INFO] ----------------------------------------------------------------------
[INFO] ----------------------------------------------------------------------
[INFO] Step 4/9: Conforming input VCF...
[INFO] Markers total: 555
[INFO] Markers filtered: 1
[INFO] Markers remaining: 554
[INFO] Markers phasable: 407
[INFO] Markers ready: 401
[INFO] Markers conformed: 6
[INFO] Markers unphasable: 147
[INFO] Markers absent in reference VCF: 139
[INFO] Markers with different REF allele: 4
[INFO] Markers with no overlapping ALT alleles: 4
[INFO] Finished conforming input VCF
[INFO] ----------------------------------------------------------------------
[INFO] ----------------------------------------------------------------------
[INFO] Statistically phasing input VCF...
[INFO] Markers attempted: 407
[INFO] Markers phased: 407
[INFO] Markers omitted: 0
[INFO] Finished statistically phasing input VCF
[INFO] ----------------------------------------------------------------------
[INFO] ----------------------------------------------------------------------
[INFO] Step 6/9: Annotating input VCF...
[INFO] Markers with Stargazer membership: 82
[INFO] Variants with low impact: 60
[INFO] Variants with moderate impact: 13
[INFO] Variants with high impact: 9
[INFO] Variants reverted to wild type: 20/21
[INFO] Finished annotating input VCF
[INFO] ----------------------------------------------------------------------
[INFO] ----------------------------------------------------------------------
[INFO] Step 7/9: Phasing input VCF by haplotype extension...
[INFO] Markers attempted: 7
[INFO] Markers phased: 7
[INFO] Markers omitted: 0
[INFO] Finished phasing input VCF by haplotype extension
[INFO] ----------------------------------------------------------------------
[INFO] ----------------------------------------------------------------------
[INFO] Step 8/9: Detecting structural variants...
[INFO] Use all samples for normalization: True
[INFO] Number of samples with SV: 24
[INFO] Finished detecting structural variants
[INFO] ----------------------------------------------------------------------
[INFO] ----------------------------------------------------------------------
[INFO] Step 9/9: Plotting various profiles...
[INFO] Step size: 500
[INFO] Step size adjusted for target gene: 73
[INFO] Step size adjusted for control gene: 8
[INFO] Finished plotting various profiles
[INFO] ----------------------------------------------------------------------
[INFO] ----------------------------------------------------------------------
[INFO] Elapsed time: 0:00:48
[INFO] Stargazer finished
[INFO] ----------------------------------------------------------------------
```
