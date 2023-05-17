# Make Default Directory Plugin

### Note: This Plugin is designed for use on PHG Version 0.0.21 or later.

MakeDefaultDirectoryPlugin is an optional first step to run in the PHG.  It will create a set of Directories on the local file system which will make the Docker commands in the next steps much easier.
This plugin will also make a default config file with all of the necessary parameters which the plugins need to have set along with any default values.  Some parameters will need to be set before the next steps so please fill them out after MakeDefaultDirectoryPlugin is run.
After this plugin is done, you must copy files into the required folders. 

## Quick Start
Note this can be run outside of the docker as well.

You will need to set WORKING_DIR for things to work correctly.  This should be the location where you are planning to put all the PHG files.  In the example below, change <phg version tag> to the specific tag you have downloaded from docker hub.

```
WORKING_DIR=local/directory/where/files/will/go/
docker run --name create_directory --rm \
	-v ${WORKING_DIR}/:/phg/ \
	-t maizegenetics/phg:<phg version tag> \
	/tassel-5-standalone/run_pipeline.pl -debug -MakeDefaultDirectoryPlugin -workingDir /phg/ -endPlugin
```


## Details

This plugin will make the following directories and files in WORKING_DIR.

```
${WORKING_DIR}/config.txt
${WORKING_DIR}/load_asm_genome_key_file.txt
${WORKING_DIR}/load_wgs_genome_key_file.txt
${WORKING_DIR}/readMapping_key_file.txt

${WORKING_DIR}/inputDir/
${WORKING_DIR}/inputDir/assemblies/
${WORKING_DIR}/inputDir/loadDB/
${WORKING_DIR}/inputDir/loadDB/bam/
${WORKING_DIR}/inputDir/loadDB/bam/temp/
${WORKING_DIR}/inputDir/loadDB/bam/dedup/
${WORKING_DIR}/inputDir/loadDB/bam/mapqFiltered/
${WORKING_DIR}/inputDir/loadDB/fastq/
${WORKING_DIR}/inputDir/loadDB/gvcf/
${WORKING_DIR}/inputDir/loadDB/temp/

${WORKING_DIR}/inputDir/reference/
${WORKING_DIR}/inputDir/reference/load_genome_data.txt

${WORKING_DIR}/outputDir/
${WORKING_DIR}/outputDir/align/
${WORKING_DIR}/outputDir/align/gvcfs/

${WORKING_DIR}/tempFileDir/

${WORKING_DIR}/README.txt
```

The PHG plugins expect certain files to be loaded into these directories.

The reference fasta will need to be copied/moved into 
```
${WORKING_DIR}/inputDir/reference/
```

You will also need to fill out the following:
```
${WORKING_DIR}/inputDir/reference/load_genome_data.txt
```

An example of this file for the PHG version 0.1.X can be found [here](../Files/B73Ref_load_data.txt).

An example of this file for the PHG version 0.0.X can be found [here](../Files/sample_load_data.txt).  

If you are planning on loading Haplotypes from Assemblies the assembly fasta files should be copied to folder:



```
${WORKING_DIR}/inputDir/assemblies/
```

When processing Haplotypes from Assemblies in the older PHG versions, you must split the assemblies by chromosome and copy each chromosome fasta to the folder mentioned above.  If you are running with PHG version  1.0 or later, there should only be 1 fasta file for each assembly genome. 

To process haplotypes from assemblies, you will also need to provide a valid keyfile or fill out the details in: 
```
${WORKING_DIR}/load_asm_genome_key_file.txt
```
An example of a keyfile for processing assemblies via anchorwave with the PHG 1.0 version can be seen here: [keyfile version 1.0](../Files/assembly_anchorWave_keyfile.txt)

Examples of key files for the older PHG versions can be seen here: [keyfile example 1](../Files/assemblies_keyfile1.txt) and [keyfile example 2](../Files/assemblies_keyfile2.txt).



When processing from the PHG version 1.0 or later, see the section devoted to assembly processing.

When processing from the old PHG version temporary files will be written to:
```
${WORKING_DIR}/outputDir/align/
${WORKING_DIR}/outputDir/align/gvcfs/
```

If you are planning on loading Haplotypes from WGS fastqs, bams or GVCFs, you should put the corresponding files in:
```
${WORKING_DIR}/inputDir/loadDB/fastq/
${WORKING_DIR}/inputDir/loadDB/bam/
${WORKING_DIR}/inputDir/loadDB/gvcf/
```
You will also need to provide a valid keyfile or fill out the details in:
```
${WORKING_DIR}/load_wgs_genome_key_file.txt
```

[Return to Step 1 pipeline version 0.0.40 or earlier](CreatePHG_step1-2_main.md)

[Return to Step 1 pipeline version 1.0 or later](CreatePHG_step1CreateDB_loadRef.md)
