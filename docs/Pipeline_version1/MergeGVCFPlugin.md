The plugin MergeGVCFPlugin pulls the variant context records stored in the database for all of the taxon at each reference range stored against a specified method id.  The calls and depth information are merged into a single VariantContext record to later be read into the [FindHaplotypeClustersPlugin](FindHaplotypeClustersPlugin).

The plugin requires a PHG Haplotype Graph as well as a GenomeSequence object.  MergeGVCFPlugin is currently invoked from the RunHapCollapsePlugin, which passes these objects via the DataSet parameter.

The parameters to this plugin are:

* -outputDir <Output Directory>  The direcotry where the output VCF files will be stored. (Default=null) (OBSOLETE)
* -dbConfig < DB Config File> Config file containing properties host,user,password,DB and DBtype where DBtype is either sqlite or postgres.  
* -hapMethod <Haplotype Calling Method> Name of the method used to call the haplotypes.  This must match the method name as stored in the database methods table.  It is needed to pull the correct sub-graph.

