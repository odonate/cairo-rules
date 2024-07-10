# Cairo Rules
This repo provides Cairo and Starknet build rules for the [Please](https://please.build) build system.

## Basic usage
First add the plugin to your project. In `plugins/BUILD`:
```python
plugin_repo(
    name = "cairo",
    owner = "odonate",
    revision = "<Some git tag, commit, or other reference>",
)
```

Set up the Cairo toolchain for your project in `third_party/cairo`:
```python
subinclude("///cairo//build_defs:cairo")

cairo_toolchain(
    name = "toolchain",
    hashes = ["<hash>"],
    version = "vX.XX.X",
    visibility = ["PUBLIC"],
)
```

Then add the plugin config to `.plzconfig`:
```ini
[Plugin "cairo"]
Target = //plugins:cairo
```

You can then compile Starknet contracts like so:
```python
subinclude("///cairo//build_defs:cairo")

starknet_contract(
    name = "your_contract",
    root = "src/lib.rs",
)
```
