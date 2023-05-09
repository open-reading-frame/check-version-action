# check-version

This action will inspect the changed files in a pull request and inspect a JSON file with version information to determine if the configured version should have been bumped but was not in a given pull request.
It will create a comment on the pull request reminding the author to update the version if it thinks a bump is needed.
A list of directories, file names, or patterns to include for the check, and ones to exclude for the check can be submitted as a list of space-delimited strings.
This action will *not* gate pull request merges, its purpose is only to act as a reminder.

## Example

```yaml
name: check-version
description: Check that the repo data JSON was updated if functional changes were made

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  check-version:
    name: Check Version
    runs-on: ubuntu-latest
    steps:
      - name: Run the check-version action
        id: run-check-version
        uses: open-reading-frame/check-version-action@main
        with:
          json: path/to/repo-data.json  # Remove if repo-data.json lives in root directory of the repo
          include-paths: '*.py static'
          exclude-paths: 'docs tests static/*.txt'
```
