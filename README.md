# parse-version-action

A GitHub action to parse release &amp; tags versions.

## Inputs

| Name | Description | Required |
| --- | --- | --- |
| *ref* | The git reference to parse | `true` |
| *trim-start* | Expect the version to begin with a string (for example 'v') and remove it | `false` |

## Example

```yml
jobs:
  decipher:
    name: Decipher
    runs-on: ubuntu-latest
    outputs:
      version: ${{ steps.parser.outputs.version }}
    steps:
      - name: Parser
        id: parser
        uses: johngeorgewright/parse-version-action@v1.0.2
        with:
          ref: ${{ github.ref }}
          trim-start: v

  publish:
    name: Publish
    runs-on: ubuntu-latest
    needs: [decipher]
    steps:
      - name: Checkout project
        uses: actions/checkout@v2
      # ...
      - name: Publish to NPM
        run: |
          npm version ${{ needs.decipher.outputs.version }}
          npm publish
```
