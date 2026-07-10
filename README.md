# eggd_cgp-cobalt

[COBALT](https://github.com/hartwigmedical/hmftools/tree/master/cobalt) (Hartwig Medical Foundation, v3.0-beta.5) targeted tumour-only read-depth-ratio caller,
packaged as a DNAnexus app. It is a parallel stage (with AMBER/SAGE) of the
[`eggd_atlas_cnv`](https://github.com/eastgenomics/eggd_atlas_cnv) somatic CNV workflow: it
computes read-depth ratios (with a target-region normalisation file) that PURPLE uses to fit
copy number.

## Inputs

| Name | Class | Description |
|---|---|---|
| `tumour_bam` / `tumour_bai` | file | Tumour BAM (chr-prefixed GRCh38) + index |
| `sample_id` | string | Output file stem |
| `cobalt_jar` | file | COBALT 3.0-beta.5 JAR |
| `norm_file` | file | `target_regions_normalisation.tsv` |
| `diploid_regions` | file | `DiploidRegions.38.bed.gz` (chr) |
| `gc_profile` | file | `GC_profile.1000bp.38.cnp` (chr) |
| `ref_fasta` / `ref_fai` | file | reference FASTA (bgzf) + index |

## Outputs

| Name | Class | Description |
|---|---|---|
| `cobalt_tar` | file | `{sample_id}.cobalt.tar.gz` → PURPLE |

## Run example

```bash
dx run eggd_cgp-cobalt \
  -itumour_bam=... -itumour_bai=... -isample_id=SAMPLE_ID \
  -icobalt_jar=... -inorm_file=... -idiploid_regions=... \
  -igc_profile=... -iref_fasta=... -iref_fai=...
```

## Notes

- **GRCh38 only**: `tumour_bam`, `diploid_regions`, and `gc_profile` must use
  GRCh38 (`chr`-prefixed contigs); the app passes `-ref_genome_version 38` to
  COBALT and will not work with GRCh37 inputs.
- `ref_fasta` must be a **bgzipped** `.fa.gz` with no `chr` prefix (COBALT
  internal requirement); `ref_fai` must be the matching `.fa.fai` index.
