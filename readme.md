# Sandboxtron

Use `sandbox-exec` on Mac to easily run terminals/programs within sandboxes for a slightly safer day-to-day.


## Install

Add `bin/` to your path.

## Usage

```sh
sb # default sandbox, offline, limited to folder and localhost connections
sb online #as above, but full online access

sb online gui #online, limited to subdir but have extra permissions
sb gui online #ditto, order doesn't matter

sb most #offline, but access to most folders on computer (except the secret ones)
```


When running in a sandbox, the following env vars will be defined:

```
SANDBOX_MODE_NETWORK
SANDBOX_MODE_FILE
SANDBOX_MODE_UI
```
