## DISCLAIMER

THIS REPOSITORY IS JUST FOR TESTING POURPOSE SO DO NOT SEND PR UNLESS YOU HAVE CONTRIBUTED TO [SLOTH](https://github.com/gtrabanco/sloth) PROJECT


## Not allowed context names
* autoupdate
* core
* context
* marketplace
* package
* script
* scripts
* self
* self-update
* sloth
* symlinks
* init
* shell/zsh (only `zsh` script because it is necessary in the core to reload completions when installing)
* dotfiles/create (only `create` script because it is necessary for creating dotfiles at first install)

These context are absolute reserved to core team. It is considered good practice not to reuse a sloth core context if you do, maybe you are contributing to SLOTH core and not to the marketplace.


The `git` and `shell` are not considered a dotly core scripts. But this must be discussed.

## How to add a command

1. Fork & Clone this repository
2. Create the new context and command if it does not exists or just modify one. You can import from your dotfiles by copying it.
3. Test if the script works properly on your system first, if you need help just add the tag "[HELP]" in the title. If it is a Work in progress just add "[WIP]" (even if you only need some testing or code checks). When its ready to approval just remove the tags.
4. Use the `sloth core lint` and `sloth core static_analysis` before set your PR as ready to review. CI Checks are required to approve your script.

Anyway remember that is a good practice use tags in title like:
* [Feature]
* [Fix]
* [Doc]

## Scripts Requirements

### 1. Code

#### Shebang
Shebang should be defined with `#!/usr/bin/env` to load the user desired version of a shell (see (Stackoverflow)[https://unix.stackexchange.com/questions/29608/why-is-it-better-to-use-usr-bin-env-name-instead-of-path-to-name-as-my])

#### Set Options
It is recommended to use:

```bash
set +euo pipefail
```

#### Bash variables
All scripts must provide default values for arguments or fail if a variable is not set.

#### Blocks
All code blocks should have a tab

#### Error handling
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
}
then
  error_command
fi
```

Multiple conditionals should have `then` in a new line at the same level of the if.

In comparisons use of `[[` is preferred over `[`.

#### Other
- Al identation is two spaces
- Code blocks should have a tab
- Follow all possible shellcheck recommendations is very recommended but we know that sometimes shellcheck fails.

### 2. Additional Libraries

Additional libraries should be in src subdir which would be downloaded all src folder if any script of the context is installed.

### 3. Installation scripts

If any context provide any functionality that must change something in the user dotfiles, provide a script to do it automatically or wizard for use guidance is required. The script must also check if this migration has happened. 

It is also mandatory provide a script to uninstall and undo changes.

To do this the install script must be in the context folder in 'src/<name>/install.sh' and 'src/<name>/uninstall.sh' respectively.

If a installation script is requires for full context name is the context folder if it is just for a script it is the script name. It is not recommended to name a script with the same name as the context.

Use `dot::load_library` to include libraries and be explicit in second param if you want a core library or library from another context. Example, if you want to requre `output.sh` library from core dotly library require it as:

```bash
dot::load_library "output.sh" "core"
```

Include file extension always, we know that without extension will work but is preferred if this work in the first conditional and loop iteraction (see <a href="https://github.com/gtrabanco/sloth/blob/master/scripts/core/dot.sh" target="_blank" alt="dot library code">dot.sh file code</a>).

#### 4. Dotbot installation yaml file

Any call to a dotbot file must be in the un/installation of the script and yaml files must be in `src/symlinks` subfolder.

## Feature: Create commands from terminal
WARNING: THIS WAY OF CREATING COMMANDS IS PENDING APPROVAL

```bash
lazy script create <context> <command> <description>
```

If you develop in a diferent path than your dotfiles you can provide a custom path
```bash
lazy script create --path "/to/my/dev/path" <context> <command> <description>
```
