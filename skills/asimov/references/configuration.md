# Module configuration

Installation may leave a module disabled until its required variables are set. Check state:

```bash
asimov --color never module list -o jsonl
```

Configure:

```bash
asimov module config "$NAME"              # interactive
asimov module config "$NAME" key value    # set a non-secret value
asimov module config "$NAME" key          # read a value
asimov module enable "$NAME"
```

For interactive or secret-bearing setup (passwords, tokens, keys, OAuth, device linking), ask the user to run `asimov module config "$NAME"` in their own terminal and report back only whether it succeeded. Never have secrets pasted into the chat or placed on command lines you run.

The module's `.asimov/module.yaml` declares its variables under `config` and environment under `uses`; its `README.md` covers provider-specific steps such as app passwords or linked devices.

After setup, confirm resolution:

```bash
asimov module resolve "$URL"
```
