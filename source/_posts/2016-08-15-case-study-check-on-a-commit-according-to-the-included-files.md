---
layout: post
title: "Case Study: Check on a commit according to its included files"
date: 2016-08-15 19:43:21 -0700
comments: true
categories: case-study
---

# Problem Description

Suppose one task in your Continuous Integration (CI) pipeline is triggered on every commit to the project repository. Some the files in the repository require passing the check of the CI task, while some other files do not require passing the check. What should the CI task do to decide if it is needed to perform the needed checking on the commit?

# Design the CI task

The CI task need have the ability to analyze the files included in the commit, and decide whether the commit requires passing a check, or not. We need tell the CI task which files require passing a check through configurations.

<!--more--> 

## Configuration

There are multiple ways to design the configurations, such as:

1. Only list the files or paths requiring the check

2. Only list the files or paths do not require the check

3. List the files or paths requiring the check, and also list the subset files or paths that do not require the check

The 3rd way probably is the optimal one because it provides the flexibility for you to put a large scope path as the files need check, and then exclude a subset from the large scope path. For example:

```

check: my_project/dev/

skip: my_project/dev/test/

```

To apply the 3rd method, the configuration of the CI task will include two types: inclusion, and exclusion.

## Analyze files in the commit

The needed analysis process of the CI task is:

- If none of the files in the commit matches the inclusion in configuration, skip the check

- If all the files in the commit matching the inclusion in configuration also matching the exclusion in configuration, skip the check

- In other cases, the check for this commit is needed

The complexity of the given process is *O(n<sup>2</sup>)*.

A mistake that could happen in the analysis process is when you analyze the exclusion cases, you should do the analysis only on the files that match inclusion configuration, which is a subset of files in the commit.

# Example with the Python

Here is the code written in Python for demonstrating the case discussed above.

- ```commit_files```: a list containing all the files in the commit

- ```config```: a dictionary containing inclusion and exclusion configurations

- ```config['include']```: a list containing all the files or paths need check

- ```config['exclude']```: a list containing the files or paths do not need check

```

def analyze_commit_files(commit_files, config):

    need_check = False    

    

    # commit need_check is False if:    

    # - No files in this commit    

    # - Config does not have any 'include' defined    

    if commit_files is None or len(commit_files) == 0:

        return need_check

    if not 'include' in config or config['include'] is None or len(config['include']) == 0:

        return need_check

    # commit need_check is False if:    

    # - All file in the commit matches the configured inclusion, OR    

    # - All files in the commit that matches the inclusion, also match the configured exclusion    

    # First check inclusion    

    files_need_check = list()

    for cf in commit_files:

        for check_file in config['include']:            

            if re.search(check_file, cf):                            

                files_need_check.append(cf)

    

    if len(files_need_check) > 0:

        # Check skip_path

        if not 'exclude' in config or config['exclude'] is None or len(config['exclude']) == 0:

            need_check = True

         else:

             for cf in files_need_check:

                 for skip_file in config['exclude']:                         

                    if not re.search(skip_file, cf):                       

                        need_check = True

                        break

    return need_check

```


