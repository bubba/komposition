# Installation

Komposition runs on Linux, macOS, and Windows. The main way to install
Komposition is from source, but binary packages are [available for
macOS from Homebrew](https://formulae.brew.sh/formula/komposition).

## Binary Packages

### Homebrew

Komposition is available for macOS through [a Homebrew
formula](https://formulae.brew.sh/formula/komposition). Given that you
have Homebrew installed, run the following in your terminal to install
Komposition:

```shell
brew install komposition
```

Komposition is now on your `PATH` and can be run from a terminal:

```shell
komposition
```

!!! note
    
    There's currently no application launcher in the Homebrew formula,
    but that might be added in the future.

## Install from Source Code

Komposition can be built on macOS, Windows, and Linux. If you're not
an experienced Haskell developer, it's recommended to use
[Stack](https://docs.haskellstack.org/en/stable/README/) to build the
application. The following instructions will be based on Stack, so go
ahead and [install that
first](https://docs.haskellstack.org/en/stable/README/#how-to-install).

!!! note "Using another build tool"
    If you know your way around building Haskell programs, you might want to
    build it using Nix or regular Cabal, instead.

### Getting the Source Code

Next, clone the source code repository using Git.

```shell
git clone https://github.com/owickstrom/komposition.git
cd komposition
```

Alternatively, if you're not using Git, download a [ZIP
archive](https://github.com/owickstrom/komposition/archive/master.zip):

```shell
wget https://github.com/owickstrom/komposition/archive/master.zip -O komposition-master.zip
unzip komposition-master.zip
cd komposition-master
```

You now have the source code. Jump on to the instructions below specific to
your operating system.

### Debian/Ubuntu

First, install the required dependencies:

```shell
sudo apt-get install \
    ffmpeg \
    sox \
    libgmp-dev \
    libavutil-dev \
    libavformat-dev \
    libavcodec-dev \
    libswscale-dev \
    libavdevice-dev \
    libgirepository1.0-dev \
    libgtk-3-dev \
    libpango1.0-dev \
    libgdk-pixbuf2.0-dev \
    libgstreamer1.0-dev \
    gstreamer1.0-libav \
    gstreamer1.0-gtk3 \
    gstreamer1.0-plugins-base \
    gstreamer1.0-plugins-good \
    gstreamer1.0-plugins-bad
```

!!! warning
    If you find additional packages that needs to be installed, please [submit
    an issue on GitHub](https://github.com/owickstrom/komposition).

Next, build and install the application using Stack:

```shell
stack install
```

You should now have Komposition available:

```shell
~/.local/bin/komposition
```

If you have added `~/.local/bin` to your `PATH`, run:

```shell
komposition
```

!!! warning "Older GTK+ Versions"

    If you see an error like the following when installing, it means your
    version of GTK+ is too old:

    ```
    Not in scope: data constructor ‘Gtk.FileChooserNative’
    ```

    This has been detected on Ubuntu 16.04. You may fix the issue by
    upgrading to Ubuntu 18.04, or by compiling and installing a newer version of
    GTK+ from source.

### macOS

```shell
brew install pkg-config gobject-introspection gtk+3 ffmpeg sox gstreamer libffi gst-plugins-base gst-plugins-good gst-libav

export PKG_CONFIG_PATH="/usr/local/opt/libffi/lib/pkgconfig"

# if you get an error in the next step about 'happy' not being on your
# PATH, run this command first:
stack build happy
stack install
```

### Windows

Komposition can be built on Windows in an MSYS2 environment. The
precise instructions are not available in this documentation yet, but
you should be able to install the dependencies using a command like
the following, and then compile and run Komposition using Stack.

```
# something like this...
pacman -S mingw-w64-x86_64-gstreamer mingw-w64-x86_64-gst-libav mingw-w64-x86_64-gst-plugins-{base,good,bad}
# TODO: also gtk+3, ffmpeg, and sox
```

### Nix/NixOS

Komposition is not yet in [nixpkgs](https://github.com/NixOS/nixpkgs), but it
can be installed with Nix from an archive on GitHub.

First, consider installing [Cachix](https://cachix.org/) and using the
Komposition binary cache. It's not strictly required, but will save you time
waiting on compilation.

```shell
cachix use komposition
```

Next, use `nix-env` to install Komposition from the `master` branch:

```shell
nix-env -iA komposition -f https://github.com/owickstrom/komposition/archive/master.tar.gz
```

Run it from the command line:

```shell
komposition
```
