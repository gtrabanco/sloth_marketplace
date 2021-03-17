# DISCLAIMER

THIS REPOSITORY IS JUST FOR TESTING POURPOSE SO DO NOT SEND PR UNLESS YOU HAVE CONTRIBUTED TO DOTLY PROJECT


# Not allowed context names
* core
* self
* dotly
* scripts
* context
* script

This context are absolute reserved to core team

# How to add a command

1. Fork & Clone this repository
2. Create the new context and command if it does not exists or just modify one
3. Test if the script works properly on your system, if you need help just add the tag "[HELP]" in the title. If it is a Work in progress just add "[WIP]" (even if you only need some testing or code checks). When its ready to approval just remove the tags.

Anyway remember that is a good practice use tags in title like:
* [Feature]
* [Fix]
* [Doc]


# Feature: Create commands with dotly
WARNING: THIS WAY OF CREATING COMMANDS IS PENDING APPROVAL

```bash
dot dotly create --path "/to/my/dev/path" <context> <command> <description>
```


WARNING: TYPESCRIPT COMMANDS IS A DEVELOPMENT FEATURE AND IS NOT AVAILABLE
If you prefer to create a Typescript command:

```bash
dot dotly create --typescript --path "/to/my/dev/path" <context> <command> <description>
```
