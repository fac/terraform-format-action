# terraform-format-action

GH Action to check terraform fmt, optionally fix and push commit.

By default the action checks for terraform formatting problems, passing the
check if none found or errors, failing the check if there are issues.

As auto commits can be annoying and cause issues with workflow triggering
from automatic commits, we don't fix problems by default, if you want that
set the fix-format input to true. Then if it finds terraform formatting
issues it will fix those by running terraform format, then commit and push
those changes using the author of the triggering commit. Note that the pushed
commit will **not** trigger a new run of this workflow (a protection in the
actions system against loops).

## Inputs

### fix-format

Defaults to false, set to true to have the action push auto commits fixing formatting errors found.

## Usage

As this action may modify the workspace when fixing formatting issues it is recommended that you run it as it's own workflow job. To check the format:

```yaml
on:
  push:
jobs:
  terraform-format:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
        with:
          ref: ${{ github.head_ref }}

      - name: Terraform Format Action
        uses: fac/terraform-format-action@release/v1
```

If you want auto fixing and commits pushing you most likely want this running on branches and PR, so the final merges have good formatting but not on your main branch as auto commits may trigger other effects such as deploys. If so use you can set that up with:

```yaml
on:
  push:
    branches-ignore:
    - $default-branch
jobs:
  terraform-format:
    runs-on: ubuntu-latest
    steps:
      # v2 and with.ref ensures we checkout a branch and not detached, as we might push.
      - name: Checkout
        uses: actions/checkout@v2
        with:
          ref: ${{ github.head_ref }}

      - name: Terraform Format Action
        uses: fac/terraform-format-action@release/v1
        with:
          fix-format: true
```
