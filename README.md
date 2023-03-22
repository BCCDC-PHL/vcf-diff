# vcf-diff
Check for differences between two vcf files

## Usage
```
usage: vcf-diff [-h] [-i INFO_ID_LOOKUP] [-f FORMAT_ID_LOOKUP] [-a] [--no-header] [--ref REF] [--test TEST]

optional arguments:
  -h, --help            show this help message and exit
  -i INFO_ID_LOOKUP, --info-id-lookup INFO_ID_LOOKUP
  -f FORMAT_ID_LOOKUP, --format-id-lookup FORMAT_ID_LOOKUP
  -a, --all-comparisons
  --no-header
  --ref REF
  --test TEST
```

If we have two vcf files `ref.vcf` and `test.vcf`, we can compare them

```
vcf-diff --ref ref.vcf --test test.vcf
```

By default, only differences will be output. If no differences are found, only the header will be printed:

```
variant_id,feature,ref_vcf,test_vcf,equal
```

If you would prefer a completely empty output when no differences are found, the `--no-header` flag can be used:

```
vcf-diff --no-header --ref ref.vcf --test test.vcf
```

To see all comparisons, use the `-a` or `--all-comparisons` flag:

```
vcf-diff --all-comparisons ref.vcf test.vcf
```

```
variant_id,feature,ref_vcf,test_vcf,equal
NA,num_variants,90,90,True
MN908947.3:241:C:T,variant/present,True,True,True
MN908947.3:241:C:T,info/AB,[0.0],[0.0],True
MN908947.3:241:C:T,info/ABP,[0.0],[0.0],True
MN908947.3:241:C:T,info/AC,[1],[1],True
MN908947.3:241:C:T,info/AF,[1.0],[1.0],True
MN908947.3:241:C:T,info/AN,1,1,True
MN908947.3:241:C:T,info/AO,[382],[382],True
MN908947.3:241:C:T,info/CIGAR,['1X'],['1X'],True
```

The following comparisons are made:

- The total number of variants in each file
- For each variant (CHROM:POS:REF:ALT):
  - Whether or not the variant is present in both files
  - For each INFO tag, whether the values match between files
  - For each FORMAT tag, whether the values match between files

