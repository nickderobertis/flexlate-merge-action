# Flexlate After-Merge Action

Official Flexlate Github Action to be run after merges. Merges Flexlate feature branches into main branches and handles merge conflict resolution flow.

## Inputs

- `branch_name`: The name of the base branch that the Flexlate branches were created on or the full name of a flexlate-templates-for-conflicts branch
- `gh_token`: The Github token to use for authentication

## Outputs

## Examples

## Development Status

This project uses [semantic-release](https://github.com/semantic-release/semantic-release) for versioning.
Any time the major version changes, there may be breaking changes. If it is working well for you, consider
pegging to the current major version, e.g. `flexlate-merge-action@v1`, to avoid breaking changes. Alternatively,
you can always point to the most recent stable release with the `flexlate-merge-action@latest`.

## Developing

Clone the repo and then run `npm install` to set up the pre-commit hooks.

## Author

Created by Nick DeRobertis. MIT License.
