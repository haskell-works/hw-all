# hw-all
[![CircleCI](https://circleci.com/gh/haskell-works/hw-all.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-all)

* hw-balancedparens
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-balancedparens/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-balancedparens/tree/0-branch)
* hw-bits
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-bits/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-bits/tree/0-branch)
* hw-conduit
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-conduit/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-conduit/tree/0-branch)
* hw-diagnostics
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-diagnostics/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-diagnostics/tree/0-branch)
* hw-eliasfano
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-eliasfano/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-eliasfano/tree/0-branch)
* hw-excess
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-excess/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-excess/tree/0-branch)
* hw-int
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-int/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-int/tree/0-branch)
* hw-json
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-json/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-json/tree/0-branch)
* hw-json-lens
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-json-lens/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-json-lens/tree/0-branch)
* hw-mquery
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-mquery/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-mquery/tree/0-branch)
* hw-parser
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-parser/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-parser/tree/0-branch)
* hw-prim
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-prim/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-prim/tree/0-branch)
* hw-rankselect
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-rankselect/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-rankselect/tree/0-branch)
* hw-rankselect-base
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-rankselect-base/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-rankselect-base/tree/0-branch)
* hw-string-parse
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-string-parse/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-string-parse/tree/0-branch)
* hw-succinct
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-succinct/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-succinct/tree/0-branch)
* hw-xml
  [![CircleCI](https://circleci.com/gh/haskell-works/hw-xml/tree/0-branch.svg?style=svg)](https://circleci.com/gh/haskell-works/hw-xml/tree/0-branch)



# Nix setup

Install `nix`:

    curl https://nixos.org/nix/install | sh

Your `~/.nixpkg/config.nix` needs to look something like this where `$SRC` is the directory where you will clone `hw-all`:

    {
      packageOverrides = super: let self = super.pkgs; in
      {
        haskellPackages = super.haskellPackages.override {
          overrides = self: super: {
            ambiata-mafia = self.callPackage $SRC/hw-all/ambiata-mafia {};
            hw-bits = self.callPackage $SRC/hw-all/hw-bits {};
            hw-conduit = self.callPackage $SRC/hw-all/hw-conduit {};
            hw-diagnostics = self.callPackage $SRC/hw-all/hw-diagnostics {};
            hw-prim = self.callPackage $SRC/hw-all/hw-prim {};
            hw-parser = self.callPackage $SRC/hw-all/hw-parser {};
            hw-rankselect = self.callPackage $SRC/hw-all/hw-rankselect {};
            hw-xml = self.callPackage $SRC/hw-all/hw-xml {};
          };
        };
        haskell = super.haskell // {
          packages = super.haskell.packages // {
            ghc7103 = super.haskell.packages.ghc7103.override {
              overrides = self: super: {
                ambiata-mafia = self.callPackage $SRC/hw-all/ambiata-mafia {};
                hw-bits = self.callPackage $SRC/hw-all/hw-bits {};
                hw-conduit = self.callPackage $SRC/hw-all/hw-conduit {};
                hw-diagnostics = self.callPackage $SRC/hw-all/hw-diagnostics {};
                hw-prim = self.callPackage $SRC/hw-all/hw-prim {};
                hw-parser = self.callPackage $SRC/hw-all/hw-parser {};
                hw-rankselect = self.callPackage $SRC/hw-all/hw-rankselect {};
                hw-xml = self.callPackage $SRC/hw-all/hw-xml {};
              };
            };
          };
        };
      };
    }


# Building hw-json
    git clone git@github.com:haskell-works/hw-all.git
    git submodule init
    git submodule update
    cd hw-json
    git checkout v0.0-branch
    ./scripts/nix-mk
    nix-shell "<nixpkgs>" -A haskellPackages.hw-json.env
    cabal sandbox init
    cabal install --only-dependencies
    cabal build

# Building hw-xml
    git clone git@github.com:haskell-works/hw-all.git
    git submodule init
    git submodule update
    cd hw-xml
    git checkout master
    ./scripts/nix-mk
    nix-shell "<nixpkgs>" -A haskellPackages.hw-xml.env
    cabal sandbox init
    cabal install --only-dependencies
    cabal build
