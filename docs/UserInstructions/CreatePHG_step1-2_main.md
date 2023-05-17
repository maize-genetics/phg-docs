# Create and Populate a PHG database with haplotypes

Before creating the db, you need to setup the PHG directory structure.  We recommend using the default directory structure, which can be created as described in step 1A below. 
When the default directory is created, two of the files created are config.txt and load_genome_data.txt. Those files need to have values added or modified by the user before other steps can be run.

A sample config file can be viewed [here](https://bitbucket.org/bucklerlab/practicalhaplotypegraph/wiki/UserInstructions/SampleHaplotypeConfigFile)

There are two steps to building and populating a PHG database. The first step creates the PHG database and 
populates it with the reference genome. The second step populates the database with additional haplotypes that have been aligned to the
reference genome reference intervals.

# Step 1: Create database and load the reference genome and genome intervals

![CreateAndPopulatePHGDatabase_step1.png](../images/CreatePHG_step1.png)

This part of the pipeline populates the database with the reference genome, broken into "reference ranges" based on user-defined genome intervals. These same reference ranges are used to create haplotype blocks in later steps. The user can define different groups of reference ranges for different analyses.

# Run Step 1
# Use the links below to work through each step in the Step 1 flow chart

A. [Create the default directory structure](MakeDefaultDirectory.md)

B. [Create a PHG database](MakeInitialPHGDBPipeline.md)

C. [Create bed file to define genome intervals](CreatePHG_step1_bedfile.md)

D. [Optionally, set up additional groups of PHG intervals](CreatePHG_step1_groupGenomeIntervals.md)

Step 1D can be done at any time after the initial genome intervals have been loaded.

# Step 2: Add haplotypes to a database

![CreateAndPopulatePHGDatabase_step2.png](../images/CreatePHG_step2.png)

# To run the Step 2 pipeline with default values
After replacing "/path/to" with the correct path on your computer and my_container_name with a meaningful name,
    run `docker run --name small_example_container --rm -v /path/to/dockerBaseDir/:/phg/ -t maizegenetics/phg /tassel-5-standalone/run_pipeline.pl -Xmx2G -debug -configParameters /phg/configSQLiteDocker.txt -PopulatePHGDBPipelinePlugin -endPlugin`

For information on setting config parameters, see details for running [PopulatePHGDBPipelinePlugin](PopulatePHGDBPipeline.md).

## Individual parts of the step 2 pipeline can be run separately

A. Align assemblies to reference genome, add to DB, use one of these options. The alignment with mummer4 will take less time to run and is only available with PHG versions 0.0.40 and older.  Anchorwave alignment can be very slow.  But the quality of alignment when using anchorwave has been shown to be superior to other methods.  Please check out [this paper](https://www.pnas.org/doi/10.1073/pnas.2113075119) for more information on the anchorwave alignment process:

1. [Align assemblies using anchorwave aligner](CreatePHG_step2_assemblyViaAnchorwave.md)
2. [Align assemblies using mummer4 aligner](CreatePHG_step2_assemblyHaplotypeParameters.md)

B. [Align WGS fastq files to reference genome](CreatePHG_step2_addHapsFromFastq.md)

C. [Call variants from BAM file](CreatePHG_step2_addHapsFromBAM.md)

D. [Filter GVCF, add to database](CreatePHG_step2_addHapsFromGVCF.md)

Important: A GVCF file contains more information than a regular VCF file. We use the [GATK GVCF format](https://gatk.broadinstitute.org/hc/en-us/articles/360035531812-GVCF-Genomic-Variant-Call-Format) for the PHG.

E. [Create consensus haplotypes](CreatePHG_step2_consensus.md)

F. [Optionally, set up groups of PHG taxa](CreatePHG_step2_taxaGroupTables.md)

[Return to PHG version 0.0.40 Home ](../Home_variantTables.md)

[Return to PHG version 1.0 Home](../Home_variantsInGVCFFiles.md)

[Return to Wiki Home](../Home.md)
