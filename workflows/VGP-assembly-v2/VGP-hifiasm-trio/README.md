# VGP Workflow #2

This workflow performs a trio-phased assembly using PacBio HiFi long read data (for the child) and Illumina short reads (for the parents). This results in two phased assemblies: **maternal and paternal**. Since the trio information should prevent haplotypic duplication, these assemblies should not require purging of false duplicates afterwards. 

## VGP Assembly Pipeline

The collaboration between the [VGP](https://vertebrategenomesproject.org/) has led to the creation of a set of workflows dedicated to high-quality genome assembly with long reads. The pipeline includes the following workflows:
-   Creation of k-mer count databases and histograms with Meryl
-   HiFi long read assembly with Hifiasm (three modes available: pseudohaplotype, HiC-phased, and trio)
-   Scaffolding with Bionano optical map data (optional)
-   Scaffolding with HiC data


### Inputs

-   PacBio HiFi long reads for child (as a collection)
-   Interlaced reads collections for parents, generated by the workflow `VGP #1 : Meryl database creation trio`
-   Meryl database for child, generated by the workflow `VGP #1 : Meryl database creation trio`
-   Meryl hapmer databases for parents, generated by the workflow `VGP #1 : Meryl database creation trio`
-   GenomeScope summary for child, generated by the workflow `VGP #1: Meryl database creation trio`

### Outputs

-   Cutadapt trimmed reads for child (as a collection)
-   Hifiasm assembly:
    -   GFAs:
        -   hap1 contig graph
        -   hap2 contig graph
        -   Raw unitig graph
        -   Processed unitig graph
    -   Each assembly:
        -   hap1/hap2 assembly in fasta format
        -   BUSCO 
            -   Short text summary
            -   Missing Buscos table
            -   Full table
            -   Summary image
-   Parameter file containing the estimated genome size (for use in downstream workflows)
-   QUAST statistics for both assemblies:
        -   Tabular report
        -   HTML report
        -   PDF report
        -   Log
-   Merqury analysis of Hifiasm trio assemblies
    -   Stats (completeness stats)
    -   Size files
    -   QV files
    -   Images (spectra-cn & spectra-asm plots; trio: hapmer blob plot, block plots)
    -   BED files
    -   WIG files
-   gfastats
    -   gfastats on hap1 contig graph
    -   gfastats on hap2 contig graph