# Example Flake
see the [NixOS Wiki](https://nixos.wiki/wiki/Flakes) for helpful notes.

## Building a configuration.nix the nixos-unstable channel
```
{
  inputs = {
    nixpkgs.url = "nixpkgs/nixos-unstable";
  };
  outputs = { self, nixpkgs }: {
    # replace 'joes-desktop' with your hostname here.
    nixosConfigurations.media = nixpkgs.lib.nixosSystem {
      system = "x86_64-linux";
      modules = [ ./configuration.nix ];
    };
  };
}
```
