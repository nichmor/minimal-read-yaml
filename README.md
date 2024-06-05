# Read YAML Github action

This action reads a .yaml file, and sets one output for every key it has. 

It aim to be minimal and simple.



## Configuration keys

There are 1 mandatody configuration which is 'config'.

### config

This configuration is mandatory and is the path to the yaml file that action should use as its source configuration.

## Example usage


The config file contains the following keys:

> ```yaml
> name: example
> environment:
>   name: example
>   permissions:
>     - name: example
>       permission: read
>     - name: example2
>       permission: write
> deployment:
>   code:
>     source:
>       libs: path/to/libs
>       entry: path/to/entry
> ```

Note that this is contained nested values. 
The action reads the yaml file in the same way as the example above, and outputs:

> ```
> name: example
> environment.name: example
> environment.permissions.0.name: example
> environment.permissions.0.permission: read
> environment.permissions.1.name: example2
> environment.permissions.1.permission: write
> deployment.code.source.libs: path/to/libs
> deployment.code.source.entry: path/to/entry
> ```

To access some key, use 
```
echo ${{ steps.read-yaml.outputs['environment.name'] }}

```