# terraform-format-action

GH Action to check terraform fmt, fix if needed and push commit.

If the action finds terraform formatting issues it will fix those by running terraform format, then commit and push those changes using the author of the triggering commit. Note that the pushed commit will **not** trigger a new run of this workflow (a protection in the actions system against loops).

## Usage

As this action may modify the workspace when fixing formatting issues it is recommended that you run it as it's own workflow job.

```yaml
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
```

You most likely want this running on branches and PR, so the final merges have good formatting but not on your main branch as auto commits may trigger other effects such as deploys. If so use you can set that up with:

```yaml
on:
  push:
    branches-ignore:
    - $default-branch
```
