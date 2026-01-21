# nur-packages

**My personal [NUR](https://github.com/nix-community/NUR) repository**

![Build and populate cache](https://github.com/complex-gh/nur/workflows/Build%20and%20populate%20cache/badge.svg)

## Packages

### seedify

A command line tool to generate seed phrases from SSH keys.

## Usage

### With Flakes

```nix
{
  inputs.nur.url = "github:nix-community/NUR";

  outputs = { self, nixpkgs, nur }: {
    nixosConfigurations.myMachine = nixpkgs.lib.nixosSystem {
      modules = [
        { nixpkgs.overlays = [ nur.overlays.default ]; }
        ({ pkgs, ... }: {
          environment.systemPackages = [ pkgs.nur.repos.complex-gh.seedify ];
        })
      ];
    };
  };
}
```

### With nix-env

```bash
nix-env -f '<nixpkgs>' -iA nur.repos.complex-gh.seedify
```

### With nix-shell

```bash
nix-shell -p nur.repos.complex-gh.seedify
```
