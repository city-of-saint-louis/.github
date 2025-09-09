# Branch Name Check Workflow
The branch name check workflow is designed to enforce a standard branch naming convention across multiple repositories.  
It compares the branch name to a list of standard branch prefixes and a validation regex pattern and returns the results of each check.  
This workflow can be used in organizational repositories to require that a feature branch passes all validation checks before it can be merged into the main branch.

## Workflow components

### config/allowed-prefixes.yml
- The list of standard branch name prefixes.

### config/branch-name-pattern.yml
- The regex pattern used when validating branch names

### workflow/branch-name-check.yml
- The workflow file references both allowed-prefixes and branch-name-pattern


## Workflow usage
**These steps are required in order to activate this workflow for a specific repository:**
1. First, create a `.github` directory in the root of the target repository (if it does not already exist)
2. Now, create a `.github/workflows` directory (if it does not already exist)
3. In the `.github/workflows` directory, copy and paste the following yaml to a new file called `validate-branch-name.yml`. Save the file to create the new workflow.
```
name: Validate Branch Name

on:
  push:
    branches:
      - '**'

jobs:
  branch-name-check:
    uses: city-of-saint-louis/.github/workflow/branch-name-check.yml@main
```
4. In the target repository, navigate to `Settings > Branches`
5. Under `Branch protection rules`, click `Add rule`
6. Under `Branch name pattern`, enter `main` 
7. Check `Require status checks to pass before merging`
8. In `Status checks that are required`, select the workflow name (e.g., Branch Name Check or the name shown in your Actions runs)
9. Save Changes