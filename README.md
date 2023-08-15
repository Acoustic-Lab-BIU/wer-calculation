# asr_evaluation

[![Build Status](https://travis-ci.org/belambert/asr-evaluation.svg?branch=main)](https://travis-ci.org/belambert/asr-evaluation)
[![PyPI version](https://badge.fury.io/py/asr_evaluation.svg)](https://badge.fury.io/py/asr_evaluation)
[![codecov](https://codecov.io/gh/belambert/asr-evaluation/branch/main/graph/badge.svg)](https://codecov.io/gh/belambert/asr-evaluation)

Python module for evaluting ASR hypotheses (i.e. word error rate and word
recognition rate).

### BIU CHANGES

here's a simple example

```
from asr_evaluation import asr_evaluation as asr

ref = 'hello my name is ari it is nice to meet you'
hyp = 'hi my name is eri it is mice to meet you'

wer = asr.process_line_pair(ref, hyp, return_values=True)

print(wer)

ref = 'calculate for another sentence'
hyp = 'culculute fir anithir sintince'

wer = asr.process_line_pair(ref, hyp, return_values=True)

print(wer)

asr.get_total_wer(print_results=True)
```

output:

```
>0.2727272727272727
>1.0
>WER:    46.667% (         7 /         15)
>WRR:    53.333% (         8 /         15)
>SER:     0.000% (         2 /          0)
```

to get the WER per sentence, use `process_line_pair` and make sure to set `return_values=True`

to get the total WER use `get_total_wer`
arguments:
print_results, wer_only

if `wer_only` is set to False, the return value will be a tuple:

`(Word Error Rate, Word Right Rate, Sentence Error Rate)` `

---

This module depends on the [editdistance](https://github.com/belambert/edit-distance)
project, for computing edit distances between arbitrary sequences.

The formatting of the output of this program is very loosely based around the
same idea as the align.c program commonly used within the Sphinx ASR community.
This may run a bit faster if neither instances nor confusions are printed.

Please let me know if you have any comments, questions, or problems.

## Output

The program outputs three standard measurements:

- [Word error rate (WER)](https://en.wikipedia.org/wiki/Word_error_rate)
- Word recognition rate (the number of _matched_ words in the alignment divided by the number of words in the reference).
- Sentence error rate (SER) (the number of incorrect sentences divided by the total number of sentences).

## Installing & uninstalling

    git clone git@github.com:Acoustic-Lab-BIU/wer-calculation.git
    cd asr-evaluation
    python3 setup.py install

to confirm you have the correct version:

    pip show asr-evaluation

should show version 2.0.5.2

To uninstall with pip:

    pip uninstall asr-evaluation

## Command line usage

For command line usage, see:

```
    wer --help
```

It should display something like this:

```
usage: wer [-h] [-i | -r] [--head-ids] [-id] [-c] [-p] [-m count] [-a] [-e]
           ref hyp

Evaluate an ASR transcript against a reference transcript.

positional arguments:
  ref                   Reference transcript filename
  hyp                   ASR hypothesis filename

optional arguments:
  -h, --help            show this help message and exit
  -i, --print-instances
                        Print all individual sentences and their errors.
  -r, --print-errors    Print all individual sentences that contain errors.
  --head-ids            Hypothesis and reference files have ids in the first
                        token? (Kaldi format)
  -id, --tail-ids, --has-ids
                        Hypothesis and reference files have ids in the last
                        token? (Sphinx format)
  -c, --confusions      Print tables of which words were confused.
  -p, --print-wer-vs-length
                        Print table of average WER grouped by reference
                        sentence length.
  -m count, --min-word-count count
                        Minimum word count to show a word in confusions.
  -a, --case-insensitive
                        Down-case the text before running the evaluation.
  -e, --remove-empty-refs
                        Skip over any examples where the reference is empty.
```

## Contributing and code of conduct

For contributions, it's best to Github issues and pull requests. Proper
testing and documentation suggested.

Code of conduct is expected to be reasonable, especially as specified by
the [Contributor Covenant](http://contributor-covenant.org/version/1/4/)
