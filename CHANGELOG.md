# CHANGELOG

## [Unreleased]

## [2.3.0] - 2021-04-12

- Fix: Error message looked like the action had broken when it had in fact detected fmt errors. Changed the error message to be less confusing.

## [2.2.0] - 2021-04-09

- Added: `terraform-version` input. Allows setting or forcing the version to install, ignoring the `.terraform-version` file.
- Changed: Error messages now log as errors and showup in the build summary

## [2.1.0] - 2021-02-09

- Fix bug causing wrong terraform version to be used.
- When the check fails output the terraform command needed to fix the formatting at the place the details links to on the PR.


## [2.0.0] - 2021-01-09

- Change: default is now to just lint check for formatting, no edits are pushed.
- Added: fix-format input. Set true to fix formatting issues and push a commit.
- Fixed: Ensures status is set properly, so it can act as a merge check.

## [1.0.0] - 2021-02-14

- Uses version of terraform from .terraform-version.
- Checks for formatting errors.
- If errors found, fixes them and pushes a commit as the author.

----

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).
