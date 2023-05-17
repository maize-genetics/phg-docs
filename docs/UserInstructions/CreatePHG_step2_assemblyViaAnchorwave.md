# Quick Start

Aligning assemblies to the reference genome and adding the resulting haplotypes to the PHG database  can be done by running the AssemblyMAFFromAnchorWavePlugin, the MAFToGVCFPlugin, and the LoadHaplotypesFromGVCFPlugin.

The first plugin runs the anchorwave aligner and creates a UCSC Multiple Alignment Format (MAF) file.
The second plugin takes the MAF output from the AssemblyMAFFromAnchorWavePlugin and creates a GVCF file (when running PHG versions 0.0.40 and below) or both the bgzipped and tabix'd version of the bgzipped file (when running PHG version 1.0 or above).
The LoadHaplotypesFromGVCFPlugin takes the GVCF files created in the second step and loads this data
as assembly haplotypes to the PHG database. 


While supported, it is not recommended to run anchorwave via the PopulatePHGDBPipelingPlugin.  Running the anchorwave aligner is very memory and time intensive.  If running through PopulatePHGDBPipelinePlugin, all the genome alignments are done before the MAFs are converted to GVCFs and then stored to the database.  It may prove optimal for a user to run the AssemblyMAFFromAnchorWavePlugin separately on a machine with larger memory than needed for the rest of the pipeline.  The generated MAF files could then be transferred to a single machine for processing into GVCFs and loaded to the database.  


For details on running each of these plugins, click on the links below:


[AssemblyMAFFromAnchorWavePlugin](CreatePHG_step2_assemblyAnchorWavePluginDetails.md)

[MAFToGVCFPlugin](CreatePHG_step2_MAFToGVCFPluginDetails.md)

[LoadHaplotypesFromGVCFPlugin](CreatePHG_step2_LoadHaplotypesFromGVCFPluginDetails.md)
