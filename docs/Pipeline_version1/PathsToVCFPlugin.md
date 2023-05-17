The PathsToVCFPlugin is used to create VCF files from haplotype paths.  The user may specific specific reference ranges to be included in the exported file.  This plugin would likely be chained with the HaplotypeGraphBuilderPlugin and the [ImportHaplotypePathFilePlugin](ImportHaplotypePathFilePlugin).  It takes input from both and uses this to create the requested VCF files.

The parameters to this plugin are:

* -outputFile <Output File> The file name for storing the VCF data. (Default=null) (REQUIRED)
* -RefRangeFileVCF <Ref Range File VCF> Reference Range file used to further subset the paths for only specified regions of the genome.  It not provided, all references ranges are used.  (Default=null) (OPTIONAL)
