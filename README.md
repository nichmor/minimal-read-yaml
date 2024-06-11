# Minimal YAML Reader: A GitHub Action 📝
This action reads a .yaml file and sets one output for every key it contains. It aims to be minimal and simple.

## Why? 🤔
Present solutions often do more than one thing (and do them well), but they are not intuitive to set up or use. Some have unresolved issues, and others don't work on Windows.

minimal-yaml-read is designed to be very simple to use and do only one thing: read a YAML file.

*Credits: pietrobolcato/action-read-yaml, which served as the base for this GitHub Action.*

# Configuration Keys 🔧
There is one mandatory configuration key: `config`.

## config
This key specifies the path to the YAML file that the action should read. It is required.

## Example Usage 📄
Let's use a simple example that contains some nested values:

```yaml
Copy code
name: example
environment:
  name: example
  permissions:
    - name: example
      permission: read
    - name: example2
      permission: write
```

To access a plain key, use:

```yaml
echo ${{ steps.read-yaml.outputs['name'] }}
```

To access a nested key, use:

```yaml
echo ${{ steps.read-yaml.outputs['environment.name'] }}
```

# Full Example Workflow 🛠️
Here is a complete example of a GitHub Actions workflow using the `minimal-yaml-read` action:

```yaml
name: Example Workflow

on: [push]

jobs:
  read-yaml-job:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2

      - name: Read YAML
        uses: nichmor/minimal-read-yaml@v0.0.2
        with:
          config: path/to/your/config.yaml

      - name: Access Output
        run: echo ${{ steps.read-yaml.outputs['environment.name'] }}
```
In this example, the `minimal-yaml-read` action reads the specified `YAML` file and sets outputs for each key. 
You can then access these outputs in subsequent steps using the `${{ steps.read-yaml.outputs['key'] }}` syntax.
