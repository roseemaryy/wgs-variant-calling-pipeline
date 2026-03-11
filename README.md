# WGS Variant Calling Pipeline — Clinical Genomics

## Overview
A production-grade whole genome sequencing variant calling pipeline implementing
the GATK Best Practices workflow. Designed for somatic variant detection in cancer
genomics, targeting the TP53 locus on chromosome 17 — the most commonly mutated
gene in human cancer.

## Pipeline Architecture
FASTQ → FastQC (QC) → BWA-MEM (Alignment) → SAMtools (Processing) → GATK HaplotypeCaller (Variants) → VCF

## Key Results
| Metric | Value |
|--------|-------|
| Reference | hg38 chr17 |
| Target Region | TP53 locus (chr17:7,668,402-7,687,550) |
| Total Reads | 8,000 |
| Mapping Rate | 100% |
| Variants Called | 2 SNVs |
| Tool | GATK HaplotypeCaller v4.4.0 |

## Variants Identified
| Chromosome | Position | Ref | Alt |
|------------|----------|-----|-----|
| chr17 | 7,668,903 | A | T |
| chr17 | 7,669,403 | C | G |

## Tools
- **FastQC v0.11.9** — Raw read quality control
- **BWA-MEM v0.7.17** — Read alignment via Burrows-Wheeler transformation
- **SAMtools v1.13** — Alignment file processing and indexing
- **GATK HaplotypeCaller v4.4.0** — Local haplotype reassembly and variant calling

## Why GATK HaplotypeCaller
Unlike position-based variant callers, HaplotypeCaller locally reassembles
regions of the genome before calling variants. This catches complex variants
that simpler tools miss by thinking in haplotypes rather than individual positions.

## Biological Context
TP53 (chromosome 17p13.1) encodes the p53 tumor suppressor — the guardian of
the genome. Mutated in over 50% of all human cancers. Detecting TP53 variants
from tumor sequencing directly informs prognosis and treatment decisions.

## Limitations
- Synthetic tumor data used for demonstration
- Clinical WGS requires 30x minimum coverage and matched tumor/normal pairs
- Single chromosome analysis; production pipelines process all 24 chromosomes

## Tech Stack
Python, Bash, BWA, SAMtools, GATK, FastQC, hg38 reference genome
