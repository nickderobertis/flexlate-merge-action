# Flexlate After-Merge Action

Official Flexlate Github Action to be run after merges. Merges Flexlate feature branches into main branches and handles merge conflict resolution flow.

See an overview of using Flexlate on CI [here](https://nickderobertis.github.io/flexlate/core-concepts.html#ci-workflows).

See the explanation about using the Flexlate After-Merge Action [here](https://nickderobertis.github.io/flexlate/tutorial/saving.html#merge-flexlate-branches-automatically-with-github-actions).

## Inputs

- `branch_name`: The name of the base branch that the Flexlate branches were created on or the full name of a flexlate-templates-for-conflicts branch
- `gh_token`: The Github token to use for authentication
- `main_branch`: The main branch for the repository. Defaults to `master`.

## Examples

Here's an example workflow that uses the Flexlate After-Merge Action to merge the feature branches into the main branches, and
handle the merge conflict resolution flow. It also includes a trigger to run it manually via the Github Actions UI.

```yaml
name: Flexlate After-Merge
on:
  pull_request:
    branches:
      - master
      - flexlate-output-**
    types: [closed]
  workflow_dispatch:
    inputs:
      branch:
        description: "The name of the base branch that the Flexlate branches were created on"
        required: false
        type: string
        default: template-patches

jobs:
  merge_flexlate_branches:
    runs-on: ubuntu-latest
    strategy:
      max-parallel: 1
      matrix:
        python-version: [3.8]

    if: (github.event.pull_request.merged == true || github.event.inputs.branch )
    steps:
      - uses: actions/checkout@v3
        with:
          ref: master
          fetch-depth: 0
      - uses: nickderobertis/flexlate-merge-action@v1
        with:
          branch_name: ${{ inputs.branch }}
          gh_token: ${{ secrets.GH_TOKEN }}
```

## Development Status

This project uses [semantic-release](https://github.com/semantic-release/semantic-release) for versioning.
Any time the major version changes, there may be breaking changes. If it is working well for you, consider
pegging to the current major version, e.g. `flexlate-merge-action@v1`, to avoid breaking changes. Alternatively,
you can always point to the most recent stable release with the `flexlate-merge-action@latest`.

## Developing

Clone the repo and then run `npm install` to set up the pre-commit hooks.

## Author

Created by Nick DeRobertis. MIT License.
