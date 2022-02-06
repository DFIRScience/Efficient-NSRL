## ENSRL

A script to filter and split the National Software Reference Library (NSRL) RDS.

## Why??

Known-good hash sets are extremely useful for digital investigators to filter known files in an investigation. However, more hashes mean more CPU cycles to process case data. As such, we have to be as efficient as possible with the hash sets we use.

### Filters

All NSRL entries are categorized as 362 - TBD. Which means we can't meaningfully categorize by OS. Product may be possible, but filtering NSRLProd.txt won't be very accurate.

ENSRL also filters out file names starting with "__" and "." a these seem to mostly be executable segmets and not whole files.

Split filters are built based on the NSRLOS.txt, and searching for the OS. For example "Windows." This mostly gives what we want with few false positives.

The UNIX/Linux entries get a bit more tricky, as expected. Our current filter looks like:

```shell
cat NSRLOS.txt | egrep -vi "(windows|android|ios|mac|msdos|ms dos|amstrad|netware|nextstep|aix|compaq|dos|dr dos|amiga|os x|at&t|apple)"
```

The first keywords are used for the OS filters, while things like msdos are simply removed. If you're analyzing an system running DOS... I'm so, so sorry.


## Install and Run

Make sure you have [Python 3](https://www.python.org/) installed. Download the repository. Download the [NSRL](https://www.nist.gov/itl/ssd/software-quality-group/national-software-reference-library-nsrl/nsrl-download/current-rds). Tested on Modern RDS (minimal) v2.75. Make sure NSRLOS.txt is in the same directory as NSRLFile.txt.
From a command prompt run:

```bash
pip install -r requirements.txt
python ensrl.py NSRLFile.txt
```

This will filter entries that are likely partial executable matches, java classes, etc. And will split the NSRL set by Operating System: Windows, Linux, MacOS, Android, iOS. The idea is that you choose
the database that is specific to your investigation at the time.

## Bug reports and suggestions

Pull requests considered! Otherwise create an issue or message me on [Twitter](https://twitter.com/dfirscience) if you find any bugs or have some recommendations.

## Thank you

Thanks to [Hexacorn]](https://www.hexacorn.com/blog/2022/02/04/analysing-nsrl-data-set-for-fun-and-because-curious/) for the excellent blog post that prompted this research.
