## Gene expression profiling of human NK cells in HIV, HCV and HBV patients

### Background Summary

There are two main types of immunity, i.e. innate and adaptive immunity. Innate immunity is usually regarded as our body first line defense mechanism. One of the components of human innate immune system is natural killer cells. </br>

What are natural killer cells?</br>

Natural killer cells, also known as NK cells, are large granular lymphocytes (a type of white blood cell). NK cells respond quickly to a wide variety of pathological challenges. They play a major role in fighting tumours or cancerous cells, as well as useful in combating virally infected cells (Caligiuri, 2008). </br>

NK cells are cytotoxic; small granules in their cytoplasm contain special proteins such as perforin and proteases known as granzymes. Upon release in close proximity to a cell slated for killing, perforin forms pores in the cell membrane of the target cell through which the granzymes and associated molecules can enter, inducing apoptosis. The distinction between apoptosis and cell lysis is important in immunology: -lysing a virus-infected cell would only release the virions, whereas apoptosis leads to destruction of the virus inside (https://www.sciencedaily.com/terms/natural_killer_cell.htm). </br>

NK cells serve to contain viral infections while the adaptive immune response is generating antigen-specific cytotoxic T cells that can clear the infection. Individuals with NK cell deficiency or abnormalitiy are more susceptible to viral infection. Studies reported that this immunological defect in some cases can lead to overwhelming fatal infection during childhood (Caligiuri, 2008).</br>

Acute viral infection is usually accompanied by early production of infectious virions and rapid eradication of the virus by the host immune system (Boeijen et. al, 2018). However, ineffective clearance of the virus can result in latent and even persistent infection within the host. In contrast to viruses like Epstein Barr virus (EBV), cytomegalovirus (CMV), or herpesviruses that may reinitiate replication after long periods of latency (Traylen et. al, 2011), three viruses have the capacity to persistently replicate resulting in considerable viral loads in the blood of immune competent individuals: human immunodeficiency virus (HIV), hepatitis C virus (HCV) and hepatitis B virus (HBV). Untreated patients with these diseases may harbor high viral loads for decades, which can be associated with variable degrees of immune activation or inflammation, but their antiviral host immune responses are insufficient to eradicate the virus (Zuniga et. al, 2015).</br>

Manipulation of NK cells seems to hold promise in efforts to improve organ transplantation, promote antitumor immunotherapy and control inflammatory and autoimmune disorders (Vivier et. al, 2008). Hence, with sequencing techniques have significantly improved and popularized, gene expression profiling of human NK cells could provide a better picture and important details necessary to uncover the origin of functional and phenotypical differences between viremic patients and healthy subjects (Boeijen et. al, 2018). The results from this study could benefit and facilitate future in vitro manipulation experiments.</br>

### Goals
1.	to compare NK cell transcripts of viremic HIV, HCV and HBV untreated patients.
2.	to utilize the published sequencing datasets and apply a different transcriptomics analysis approach.

### Data Description
| Information   | Description |
| ------------- |-------------| 
| Assay type     | RNA-Seq |
| Instrument      | Illumina HiSeq 2500 |   
| Library selection | cDNA     |
| Library source | transcriptomic |
| Data store | GSE125686 |
| Location | Patients recruited from outpatient clinic </br>
of the Erasmus MC Rotterdam |
| Number of subjects | Healthy control 1 (Asian): 8 |
|                    | Healthy control 2 (Caucasian): 12 |
|                    | HIV (Caucasian): 6 |
|                    | Hepatitis C, HCV (Caucasian): 8 |
|                    | Hepatitis B, HBV (Asian): 32 |
|                    | Total: 66 |

### Analysis Plan
1. Sequence reads pre-processing
    - trim adapters and low quality score sequences
    - measure GC content of reads
    - tool: Fastp

2. Align reads to human reference genome hg19
    - tool: HISAT2 or STAR
3. Assemble and quantify reads
    - tool: StringTie
4. Differential gene expression analysis
    - to compare NK cells gene expression between disease infected patients and healthy individuals
    - tool: DESeq2/ edgeR
5. Statistical testing


