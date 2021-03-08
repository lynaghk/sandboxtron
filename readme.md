# Sandboxtron

Use `sandbox-exec` on Mac to easily run terminals/programs within sandboxes for a slightly safer day-to-day.


## Install

Add `bin/` to your path.

## Usage

Run `sb` to execute a command (or open a shell, if no command provided) within a sandbox

```sh

sb # opens a shell in the default, most restricted sandbox (offline, limited to current working directory and subfolders)
sb online #as above, but full online access

sb -- ls ~ # run `ls ~` in the sandbox; this will fail unless you are invoking from ~

sb online gui #online, limited to subdir but have extra permissions
sb gui online #ditto, order doesn't matter

sb most #offline, but access to most folders on computer (except the secret ones)
```


When running in a sandbox, the following env vars will be defined:

+ `SANDBOX_MODE_NETWORK`
  + online
  + offline
  
+ `SANDBOX_MODE_FILE`
  + most: no file restrictions within a set of directories
  + full: no file restrictions

I use these to add emoji to my ZSH prompt to remind me of my shell's capabilities:

```sh
PROMPT="%(?.%F{green}.%F{red})"

# Assume starting outside of sandbox
export SANDBOX_MODE_FILE=${SANDBOX_MODE_FILE:-full}
export SANDBOX_MODE_NETWORK=${SANDBOX_MODE_NETWORK:-online}

if [[ "online" = "$SANDBOX_MODE_NETWORK" ]]; then
    PROMPT+="📡"
fi

if [[ "most" = "$SANDBOX_MODE_FILE" ]]; then
    PROMPT+="🏠"
elif [[ "full" = "$SANDBOX_MODE_FILE" ]]; then
    PROMPT+="⚡"
fi

PROMPT+=" |%f "
```
