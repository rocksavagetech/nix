# nix

This repo contains several different branches and is meant to be used as a submodule for development.



## Directions (Ubuntu)

These directions are provided to set up a fresh Ubuntu 24.04 image so it is able to be used for development with nix.

### Prerequisites

- Install Curl: `sudo apt install curl`
- Install Git: `sudo apt install git`

### Install Nix Package Manager

- Run: `sh <(curl --proto '=https' --tlsv1.2 -L https://nixos.org/nix/install) --daemon`
    - https://nixos.org/download/#nix-install-linux  
    - You will want to respond `y` to most prompts.
- Restart your shell session.

### Set Up Repo

- Download a ChiselWare repository & ensure that it has a flake.nix file in the root folder:

```sh
git clone https://github.com/rocksavagetech/dynamicfifo.git $HOME/Downloads/dynamicfifo
cd $HOME/Downloads/dynamicfifo

# For demonstration purposes, we will use the following branch to ensure that it contains a flake.nix and flake.lock file
git fetch origin pull/6/head:nix_branch
git checkout nix_branch

# The files can alos just be added from this repo to the root of the repository being set up
```

If you encounter an issue when running sbt where it cannot compile compiler-bridge_2.13, this is an issue with the specific version of scala and is fixed in the next release. See https://github.com/rocksavagetech/dynamicfifo/pull/6



### Enter Developement Shell

- Any time you need to want to use the packages needed for development for a ChiselWare project run the following:
    - `nix develop --extra-experimental-features 'nix-command flakes' -c $SHELL`
    - This can be aliased to a more convenient command, and you may notice some ChiselWare repositories do this by containing a dev_shell.sh script to do this command.
- Note that this can take up to a few minutes the first time it is run but will cache the results so subsequent times will be much faster.
- That should be it, all the tools needed to develop ChiselWare cores should be available in your current shell session