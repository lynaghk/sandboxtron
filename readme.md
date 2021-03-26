# Sandboxtron

A wrapper around Mac's `sandbox-exec` that lets you easily run terminals/programs within sandboxes for a slightly safer day-to-day computing experience.

Useful if you don't want every npm/cargo/pip transitive dependency to have full access to your filesystem and network.


## Install

Add `bin/` to your path.

## Usage

+ `sb` opens a shell in an offline sandbox that can only read/write the current directory and its children.
See [base.sb](/mac/base.sb) for the default sandbox profile.

+ `sb online` opens a shell in an online sandbox.

+ `sb online -- ping www.google.com` runs `ping www.google.com` in an online sandbox and returns.

+ In general: `sb foo bar baz -- command` sources profiles `foo.sb`, `bar.sb`, `baz.sb` from the [profile directory](/mac/) and runs `command` within that sandbox.

If an app doesn't work a sanbox, search for "sandbox" in `Console.app` to see what permissions the app was denied and try granting these permissions via a custom profile.

When running in a sandbox, the following env vars will be defined:

+ `SANDBOX_MODE_NETWORK`
  + online
  + offline
  
I find it helpful to add emoji to my ZSH prompt to remind me of my shell's capabilities:

```sh
PROMPT="%(?.%F{green}.%F{red})"

PROMPT="%(?.%F{green}.%F{red})"
if [[ "online" = "${SANDBOX_MODE_NETWORK:-online}" ]]; then
    PROMPT+="📡"
fi

if [[ -r "$HOME" ]]; then
    PROMPT+="🏠"
fi

PROMPT+=" |%f "
```

## Todo

+ `deny forbidden-sandbox-reinit` is thrown by:
  + Electron
  + `swift build` (though `swift` starts a REPL just fine)


## Further reading

+ https://www.karltarvas.com/2020/10/25/macos-app-sandboxing-via-sandbox-exec.html
+ Take a look around Apple's built-in profiles in /System/Library/Sandbox/Profiles
