# jimmyff blog

A little personal blog hosted on github pages using the fabulous HUGO static site generator and the lovely PaperMod theme with a bit of personalisation.

[https://www.jimmyff.co.uk](https://www.jimmyff.co.uk)

## Setup

Reqiures git submodule initalised and cloned.

```sh
git submotdule init
git submodule update
```

Git LFS needs installing as Webp images stored in LFS. To install & initalise:

```sh
brew install git-lfs
git lfs install
sudo su lfs install --system
git lfs fetch
git lfs checkout
```

### Running locally

- Use the `-D` parameter to show draft artciles.

```sh
hugo server -D
```
