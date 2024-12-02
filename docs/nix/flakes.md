# Example Flake
## Building a configuration.nix the nixos-unstable channel
```
{
  description = "This is my first flake";

  inputs = {
    # nixpkgs = {
    #   url = "github:NixOS/nixpkgs/nixos-24.05";
    # };
    # nixpkgs.url = "github:NixOS/nixpkgs/nixos-nixos-unstable";
    nixpkgs.url = "nixpkgs/nixos-unstable";
  };

  outputs = {self, nixpkgs, ...}:
    let 
      lib = nixpkgs.lib;
    in {
    nixosConfigurations = {
      nixos = lib.nixosSystem {
        system = "x86_64-linux";
        modules = [ ./configuration.nix ];
      };
    };
  };
}
```
