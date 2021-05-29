## DISCLAIMER

THIS REPOSITORY IS JUST FOR TESTING POURPOSE SO DO NOT SEND PR UNLESS YOU HAVE CONTRIBUTED TO DOTLY PROJECT


## Not allowed context names
* core
* self
* script
* scripts
* dotly
* context

This context are absolute reserved to core team. It is considered good practice not to reuse a dotly core context:
* core
* dotfiles
* package
* self
* symlinks

This script names are reserved
* init/enable
* init/disable

The `git` and `shell` are not considered a dotly core scripts. But this must be discussed.

## How to add a command

1. Fork & Clone this repository
2. Create the new context and command if it does not exists or just modify one
3. Test if the script works properly on your system, if you need help just add the tag "[HELP]" in the title. If it is a Work in progress just add "[WIP]" (even if you only need some testing or code checks). When its ready to approval just remove the tags.

Anyway remember that is a good practice use tags in title like:
* [Feature]
* [Fix]
* [Doc]

## Scripts Requirements

### 1. Code
All scripts must provide default values for arguments or fail if a variable is not set.

It is recommended to use:

```bash
set +euo pipefail
```

Every script should handle all possible errors.

Explicit way of doing something is always preferred than non explicit way. Example:

Non recommended way:
```bash
{
  conditional_command_that_not_output &&\
    anotherconditional_command_that_not_output &&\
    end_conditional_command_that_not_output
} || error_command
```

Recommended code:

```bash
if ! {
    conditional_command_that_not_output &&\
    anotherconditional_command_that_not_output &&\
    end_conditional_command_that_not_output
}; then
  error_command
fi
```

In comparisons use of `[[` is preferred over `[`.

Follow all possible shellcheck recommendations is very recommended but we know that sometimes shellcheck fails.

### 2. Additional Libraries

Additional libraries should be in src subdir which would be downloaded all src folder if any script of the context is installed.

### 3. Installation scripts

If any context provide any functionality that must change something in the user dotfiles, provide a script to do it automatically after installing the context or script is required. You can require user iteraction but a wizard or script is mandatory.

It is also mandatory provide a script to uninstall and undo changes.

To do this the install script must be in the context folder in 'src/<name>/install.sh' and 'src/<name>/uninstall.sh' respectively.

If a installation script is requires for full context name is the context folder if it is just for a script it is the script name. It is not recommended to name a script with the same name as the context.

Use `dot::get_script_src_path` to include libraries and be explicit in second param if you want a core library. If you want to requre `output.sh` library from core dotly library require it as:

```bash
dot::get_script_src_path "output.sh" "core"
```

Include file extension always, we know that without extension will work but is preferred is this work in the first conditional and loop iteraction.

#### 4. Dotbot installation yaml file

Any call to a dotbot file must be in the un/installation of the script and yaml files must be in `src/symlinks` subfolder.

## Feature: Create commands with dotly
WARNING: THIS WAY OF CREATING COMMANDS IS PENDING APPROVAL

```bash
dot dotly create --path "/to/my/dev/path" <context> <command> <description>
```

<!--
WARNING: TYPESCRIPT COMMANDS IS A DEVELOPMENT FEATURE AND IS NOT AVAILABLE
If you prefer to create a Typescript command:

```bash
dot dotly create --typescript --path "/to/my/dev/path" <context> <command> <description>
```
-->
