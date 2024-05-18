## Ad Hoc Shell Environments

In a Nix shell environment, you can immediately use any program packaged with Nix, without installing it permanently.

Nix Manual `man nix-shell`

Install Package - `nix-shell -p packageName` https://search.nixos.org/packages

Check Package Version `which packageName`

Nested Shell Session - can create a nested session that gives you access to the packages in the current session and additionally the ones declared in your new session `nix-shell -p packageName` command

Exit Shell - `exit` or `CTRL-D`

## Scripts

In Nix you can specify dependencies for a script so that it always has its dependencies before running.

Nix Shebang `#!/usr/bin/env nix-shell`

[`env`](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/env.html) is a program available on most modern Unix-like operating systems at the file system path `/usr/bin/env`. It takes a command name as argument and will run the first executable by that name it finds in the directories listed in the environment variable `$PATH`

A shebang line is a line that starts with `#!`

```bash
#!/usr/bin/env nix-shell
#! nix-shell -i bash --pure
#! nix-shell -p bash cacert curl jq python3Packages.xmljson
#! nix-shell -I nixpkgs=https://github.com/NixOS/nixpkgs/archive/2a601aafdc5605a5133a2ca506a34a3a73377247.tar.gz

curl https://github.com/NixOS/nixpkgs/releases.atom | xml2json | jq .
```

#### Fully Reproducable Nix Pinning

Choose version here https://status.nixos.org/
- the **latest stable NixOS** release by using a specific version, such as `nixos-21.05`, **or**
- the latest **unstable release** via `nixos-unstable`.

```bash
{ pkgs ? import (fetchTarball "https://github.com/NixOS/nixpkgs/archive/06278c77b5d162e62df170fec307e83f1812d94b.tar.gz") {}
}:
```
``

## Flags

 `-i` tells which program to use for interpreting the rest of the file
    
`--pure` excludes most environment variables when the script is run
    
`-p` lists packages that should be present in the interpreter’s environment
    
`-I` explicitly sets [the search path](https://nixos.org/manual/nix/unstable/command-ref/opt-common.html#opt-I) for packages