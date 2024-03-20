You can remove the "sudo" prefix from a command using `sed` and execute the modified command in a single line like this:

```
eval $(echo "sudo apt-get update" | sed 's/sudo //g')
```

Here's how it works:

1. `echo "sudo apt-get update"` outputs the original command with the "sudo" prefix.
2. The output is piped to `sed 's/sudo //g'`, which replaces all occurrences of "sudo " (note the space after "sudo") with an empty string, effectively removing the "sudo" prefix.
3. The modified command is captured by surrounding the `sed` command with `$(...)`, which is a command substitution in Bash that replaces the `$(...)` part with the output of the command.
4. Finally, `eval` is used to execute the modified command without the "sudo" prefix.

So, in this single line, we're using `echo` to provide the original command, `sed` to remove the "sudo" prefix, command substitution to capture the modified command, and `eval` to execute it.

Note that using `eval` can be a security risk if the input is not properly sanitized, as it can potentially execute arbitrary code. In this specific case, where the input is a hardcoded command, it should be safe. However, if you're processing user input or untrusted data, it's essential to sanitize the input before using `eval`.
