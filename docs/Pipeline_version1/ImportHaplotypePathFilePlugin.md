The ImportHaplotypePathFilePlugin takes the haplotypePath files produced by [HapCountBestPathToTextPlugin](HapCountBestPathToTextPlugin) and imports them to a data structure to be used by the [PathsToVCFPlugin](PathsToVCFPlugin).  The latter produces VCF files from the paths.

This plugin expects a PHG Haplotype Graph to be sent as an incoming parameter.  The plugin requires a PHG Haplotype Graph, which can be adquired by chaining the running of HaplotypeGraphBuilderPlugin and this plugin.  The output from the HaplotypeGraphBuilderPlugin will be input to the ImportHaplotypePathFilePlugin.  In addition, the ImportHaplotypePathFilePlugin provides the input to the PathsToVCFPlugin.  All 3 plugins are likely chained when called via the command line or a shell script.  See [ExportPath.sh](ExportPath),

The ImporthaplotypePathFilePlugin  takes the following parameters:

* -inputFileDirectory <Input File Directory> A directory containing the paths text files to imported and used to create the vcf files. (Default=null) (REQUIRED)


