# parse-version-action

A GitHub action to parse release &amp; tags versions.

## Inputs

| Name | Description | Required |
| --- | --- | --- |
| `ref` | The git reference to parse | `true` |
| `trim-start` | Expect the version to begin with a string (for example 'v') and remove it | `false` |

## Example

```yml
jobs:
  decipher:
    name: Decipher
    runs-on: ubuntu-latest
    steps:
      - name: Parser
        id: parser
        uses: johngeorgewright/parse-version-action
        with:
          ref: ${{ github.ref }}
          trim-start: v

      - name: Debug
        run: echo 'version = ${{ steps.parser.outputs.version }}'
```
