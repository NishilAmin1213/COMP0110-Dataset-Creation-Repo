# README - COMP0110-Dataset-Creation-Repo

A Benchmark Suite for Evaluating LLMs on Real-World Source Code Migration (Java 8 to Java 11)

MSc Software Systems Engineering Research Project (24/25)

### Python Version
This project was developed in Python 3.10.0 on Windows 11 and has not been tested in other environments

### Environment Variables
When running 'gather_repos.py', 'analyse_repos.py' and 'find_functions.py' a GitHub API Key is required under the 'GITHUB_KEY' environment variable

### External Dependencies
The project has a number of external dependencies that can be installed via pip
* javalang
* requests
* tqdm
```
pip install javalang requests tqdm
```

### Python Files
The python files are expected to be run in the following order:
* gather_repos.py
* analyse_repos.py
* find_functions.py
This process will take a lot of time (due to sleep times between requests) and between 'analyse_repos.py' and 'find_functions.py' manual intervention will be required to analyse flagged items in 'flagged_repos.txt'. This will require pairs for Java 8 and Java 11 branches of a repository to be placed in 'repo_pairs.txt', pairs will need to be separated by a blank line.

#### gather_repos.py
This file will search github and look for repos on a surface level. It will generate 'all_repositories.pkl' which will hold a the repositories that are viable for further analysis.

#### analyse_repos.py
This file will use 'all_repositories.pkl' and perform further analysis deeper into each repository. It will store statistics for what was searched within each repo to 'repo_stats.csv' and will store any flagged issues, commits or releases to 'flagged_repos.txt'

#### fund_functions.py
If repo_pairs.txt is not present, you will need to perform manual analysis on 'flagged_repos.txt' to constuct 'repo_paris.txt' yourself. Once this is done, this file will extact suitable functions from the two repositories (Java 8 branch and the Java 11 branch that has been manually provoided). This dataset will be stored under 'candidate_functions_same_params.pkl' and 'candidate_functions_different_params.pkl'

####utils.py
'utlis.py' is not to be run on their own and is used by the other python files, so will be required when running the other python files in this project
