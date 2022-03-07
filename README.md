Setup Puccini TOSCA GitHub Action
=================================

Installs [Puccini](https://github.com/tliron/puccini) in your GitHub action runner,
allowing you to validate and compile TOSCA and CSAR.

Here's an example of using it to validate TOSCA on every push. The file would be
`.github/workflows/validate-tosca.yaml` in a git repository:

```yaml
name: Validate TOSCA
on: [push]
jobs:
  CompileTOSCA:
    runs-on: ubuntu-latest
    steps:
    - name: Setup Puccini
      uses: tliron/setup-puccini@v1
      with:
        version: main
    - name: Check out repository code
      uses: actions/checkout@v3
    - name: Compile TOSCA
      run: puccini-tosca compile --coerce ${{ github.workspace }}/my-tosca.yaml
```

Note that `version` is optional, with the default being `main`, which will install
the latest HEAD commit. You can use any version tag (or branch name) instead from
the Puccini repository.

See [this example repository](https://github.com/tliron/puccini-action-example).
