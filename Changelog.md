# Changelog

## 1.0.0
Initial app release. Converted from the `cnv-backbone-purple-atlas` `cgp-cobalt` **applet**
into a versioned, namespaced DNAnexus **app** (`org-emee_1`, `aws:eu-central-1`) for the
`eggd_atlas_cnv` somatic CNV workflow.

Conversion changes only:
- App metadata (`version`, `developers`, `authorizedUsers`).
- Explicit `timeoutPolicy` (6 h).
- System dependencies moved from an inline `apt-get install` in `code.sh` to
  `runSpec.execDepends` (`openjdk-21-jre-headless`, `samtools`, `tabix`).

COBALT tool flags, reference inputs and the output name (`cobalt_tar`) are unchanged.
