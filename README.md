# Setup Cylc Action

A GitHub action to install Cylc (and optionally Rose).

This action uses micromamba to install Cylc (and optionally Rose) into an
environment called `cylc`. It puts the `cylc`, `isodatetime` (and optionally
`rose`) commands in `$PATH` so they can be called by later steps in your
workflow.

This action runs on the Linux and Mac OS runners (but not Windows).


## Example Workflow

```yaml
jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Cylc
        uses: cylc/setup-cylc@v1.0.1
        with:
          cylc_rose: true

      - name: Run Cylc Tests
        run: |
          cylc validate ./my-workflow
          cylc lint ./my-workflow

      - name: Run Rose Tests
        run: |
          rose macro -V -C ./my-workflow
          rose metadata-check -C ./my-workflow/meta
          rose metadata-check -C ./my-workflow/app/my-app/meta
```


## Options

**``cylc_version``** [default 8]

The version of Cylc to install e.g:

```
# install the latest version of Cylc 8
cylc_version: 8

# install the latest version of Cylc 8.1
cylc_version: 8.1

# install Cylc 8.1.1
cylc_version: 8.1.1
```


**``cylc_rose``** [default false]

Install Rose along with Cylc Rose support.
