# Available Commands

## completion

The `completion` command **Generates** **autocompletion** script for the specified shell.

### Usage

```
cxsast_exporter completion [command] <flags>
```

### Available Commands

- `bash` - Generates the autocompletion script for bash
- `fish` - Generates the autocompletion script for fish
- `powershell` - Generates the autocompletion script for powershell
- `zsh` - Generates the autocompletion script for zsh

### Flags

| **Name** | **Default** | **Description** |
|---|---|---|
| --help, -h | | help for the completion command |

### Examples

```
C:\User>cxsast_exporter completion powershell
# powershell completion for cxsast_exporter -*- shell-script -*-

function __cxsast_exporter_debug {
    if ($env:BASH_COMP_DEBUG_FILE) {
        "$args" | Out-File -Append -FilePath "$env:BASH_COMP_DEBUG_FILE"
    }
}
```

## version

The `version` command **Print** the **version number** of cxsast_exporter tool.

### Usage

```
cxsast_exporter version <flags>
```

### Flags

| **Name** | **Default** | **Description** |
|---|---|---|
| --help, -h | | help for the version command |

### Examples

```
C:\User>cxsast_exporter version
cxsast_exporter 0.0.2+20211013173125
```
