---
layout: default
has_children: true
title:  "Mambolab toolbox"
nav_order: 3
---

# Mambolab Toolbox

The [Mambolab Toolbox](https://github.com/mambolab/mambolab) is a Matlab based toolbox used by our group to analyze M/EEG data.
It heavily uses fieldtrip function to perform basic preprocessing and other analyses. We included functions for estimating functional connectivity using several coupling indices.

## Contribution Guidelines
In the past years, we have moved from pipelines made of homemade MATLAB routines to a more frequent use of a mixture of [FieldTrip](https://www.fieldtriptoolbox.org/) routines with homemade scripts. Given that we adopted a coding style similar to FieldTrip guidelines, you can find them [here](https://www.fieldtriptoolbox.org/development/guideline/code/).


### Functions
In brief our functions are should always behave like this:
```
[outputargs] = ml_functionname(cfg, inputargs)
```

### Data
We use [BIDS](https://bids-specification.readthedocs.io/en/stable/) guidelines to organize our data on folders, in order to use open-source and free readers for our data format.

Internally, the data is a MATLAB structure in a specific format, as explained in FieldTrip [data section](https://www.fieldtriptoolbox.org/development/datastructure/).



## Development workflow
Contributions to the software are made using `git` and [Github](https://github.com). 

Our repository can be accessed [here](https://github.com/mambolab/mambolab).

The workflow is common to the most of open-source software:
1. Fork the repository to your personal account, by clicking fork in the main repo page.
2. Clone your personal repository to your computer.
```
git clone https://github.com/USER/mambolab
```
This command clones the `mambolab` repo in the current directory.

3. Create a new branch with a name that has a meaningful name (e.g. `fix-iplv-formula-bug` or `nf-added-mpsi-algorithm`, not `new-branch`)
```
git checkout -b nf-added-hmm-algorithm
```
4. Make your bug fix or add your new feature (and tests ) and commit to your computer repo.
```
## added file mt_hmm.m
git add mt_hmm.m
git commit -m "NF: Added HMM algorithm for state detection
```
The `commit` add a message to the edits which must be explicative of the new feature (NF stands for New Feature).
5. Push your branch to your personal repository.
```
git push origin nf-added-hmm-algorithm
```
6. Open a Pull Request (PR) on the main repository. This can be made in your Github personal page by clicking `Open Pull Request`
7. Core developers review and test the PR (and suggest some changes, eventually).
8. The branch is merged on the main repo branch.
9. Clean up your repo.
```
git branch -D nf-added-hmm-algorithm
git push origin :nf-added-hmm-algorithm
```

You can find further information on [FieldTrip](https://www.fieldtriptoolbox.org/development/git/).