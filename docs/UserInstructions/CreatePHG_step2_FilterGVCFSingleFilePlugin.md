# FilterGVCFSingleFilePlugin 

This plugin filters a GVCF file and creates fasta sequence for loading to the PHG database.  BCFTools is used with a poissonProbability tuple to filter based on depth.

Tables populated via this method are:

* genotypes
* gametes
* gamete_groups
* methods
* haplotypes
* gamete_haplotypes

The parameters to this plugin are:

* -inputGVCFFile <input File > GVCF File to be filtered. (Default is null) (REQUIRED)
* -outputGVCFFile <output File> Output GVCF File Path and Name. (Default is null) (REQUIRED)
* -configFile <config File> Config file containing the filtering parameters. If not present, defaults will be used. (Default is null) (OPTIONAL)

The configFile parameter should contain key-value pairs.  If this file is present, the gvcf files will be filtered based on the file's parameters. To read more about the strucure of variant call records and the meaning of the fields below, please see [GATK Forum](https://gatkforums.broadinstitute.org/gatk/discussion/1268/what-is-a-vcf-and-how-should-i-interpret-it).  The supported key-value pairs for the config file are below.  Any fields left out will be ignored.

* exclusionString = String used for bcftools filtering.  If this is specified, no additional terms are added to exclude
* DP_poisson_min = minimum poisson bound used for filtering(absolute minimum is 0.0)
* DP_poisson_max = maximum poisson bound used for filtering(absolute maximum is 1.0)
* DP_min = minimum DP bound: the filtered depth at the sample level. Minimum number of filtered reads that support each of the reported alleles.
* DP_max = maximum DP bound: maximum number of filtered reads that support each of the reported alleles.
* GQ_min = minimum GQ bound: minimum confidence level that the genotype assigned to a particular sample is correct.
* GQ_max = maximum GQ bound: maximum confidence level that the genotype assigned to a particular sample is correct.
* QUAL_min = base quality minimum bound: confidence there exists variation at a given site.
* QUAL_max = base quality maximum bound: confidence there exists variation at a given site.
* filterHets = true/false or t/f, if true will filter sites where 2 or more alleles have above 0 
