Installation
============

> This fork targets **KDE Plasma 6.3+ on Wayland** on amd64/x86\_64. X11 and other architectures are unsupported. Source-build commands use Qt 6 and KF6 package names.

Repository and binary-package installs resolve runtime dependencies through the
package manager. The development packages below are needed only when building
from source. KCMUtils, Kirigami and NewStuff QML modules are runtime
requirements. Plasma Wayland Protocols supplies build-time XML definitions;
it is not a separate runtime requirement. Match packages to your distribution
and Plasma ABI: Debian 13 uses libplasma6; Debian testing and Ubuntu 26.04 use
libplasma7.

## Kubuntu / KDE Neon (26.04+)

Use the Debian/Ubuntu source-build dependencies below. The same package list applies.

## Debian and Ubuntu

Debian 13 (trixie) is the minimum supported release. The source-build instructions also apply to Debian testing and Ubuntu 26.04+.

The signed [Latte Dock NG APT repository](https://ruizhi-lab.github.io/latte-dock-ng/)
supports amd64. Add its signing key:

```bash
sudo install -d -m 0755 /etc/apt/keyrings
curl -fsSL https://ruizhi-lab.github.io/latte-dock-ng/latte-dock-ng-archive-keyring.gpg \
  | sudo tee /etc/apt/keyrings/latte-dock-ng.gpg >/dev/null
sudo chmod 0644 /etc/apt/keyrings/latte-dock-ng.gpg
```

Add **one** source line matching your OS release:

```bash
# Debian 13 (trixie)
echo 'deb [arch=amd64 signed-by=/etc/apt/keyrings/latte-dock-ng.gpg] https://ruizhi-lab.github.io/latte-dock-ng trixie main' \
  | sudo tee /etc/apt/sources.list.d/latte-dock-ng.list

# OR Debian testing
echo 'deb [arch=amd64 signed-by=/etc/apt/keyrings/latte-dock-ng.gpg] https://ruizhi-lab.github.io/latte-dock-ng testing main' \
  | sudo tee /etc/apt/sources.list.d/latte-dock-ng.list

# OR Ubuntu 26.04+
echo 'deb [arch=amd64 signed-by=/etc/apt/keyrings/latte-dock-ng.gpg] https://ruizhi-lab.github.io/latte-dock-ng ubuntu main' \
  | sudo tee /etc/apt/sources.list.d/latte-dock-ng.list
```

Then install or upgrade:

```bash
sudo apt update
sudo apt install latte-dock-ng
```

The Ubuntu suite uses the package built and install-checked on Ubuntu 26.04.
Do not add multiple suites to one system. See
[`docs/debian-apt-repository.md`](docs/debian-apt-repository.md) for maintainer details.

Alternatively, download a prebuilt `.deb` from
[GitHub Releases](https://github.com/ruizhi-lab/latte-dock-ng/releases).
Choose the package matching your distribution:

```bash
# Debian testing
sudo apt install ./latte-dock-ng_<ver>-1_amd64.deb
# Debian 13 (stable)
sudo apt install ./latte-dock-ng_<ver>-1+deb13u1_amd64.deb
# Ubuntu 26.04
sudo apt install ./latte-dock-ng_<ver>-1ubuntu1_amd64.deb
```

To build from source instead, install the build dependencies and runtime QML modules:

```bash
sudo apt install \
  cmake extra-cmake-modules \
  qt6-base-dev qt6-base-dev-tools qt6-declarative-dev qt6-declarative-private-dev qt6-wayland-dev \
  libplasma-dev libplasmaactivities-dev libplasmaactivitiesstats-dev plasma-workspace-dev kwayland-dev \
  libkf6config-dev libkf6coreaddons-dev libkf6guiaddons-dev libkf6dbusaddons-dev \
  libkf6declarative-dev libkf6itemmodels-dev libkf6xmlgui-dev libkf6iconthemes-dev \
  libkf6kio-dev libkf6i18n-dev libkf6notifications-dev \
  libkf6newstuff-dev libkf6archive-dev libkf6globalaccel-dev \
  libkf6crash-dev libkf6windowsystem-dev libkf6package-dev libkf6svg-dev \
  plasma-wayland-protocols libwayland-dev \
  liblayershellqtinterface-dev \
  qml6-module-org-kde-kirigami qml6-module-org-kde-kcmutils qml6-module-org-kde-newstuff \
  gettext build-essential git pkgconf
```

The APT repository and release packages install these QML modules as dependencies.

## Arch Linux

```bash
sudo pacman -Syu
sudo pacman -S \
  cmake extra-cmake-modules \
  qt6-base qt6-declarative qt6-wayland \
  libplasma plasma-activities plasma-activities-stats plasma-workspace kwayland \
  kconfig kcoreaddons kguiaddons kdbusaddons kcmutils kirigami \
  kdeclarative kitemmodels kxmlgui kiconthemes kio ki18n knotifications \
  knewstuff karchive kpackage kglobalaccel kcrash kwindowsystem ksvg \
  plasma-wayland-protocols wayland \
  layer-shell-qt \
  gcc make gettext git pkgconf
```

## Gentoo

Install from the personal overlay:

```bash
eselect repository add ruizhi-overlay git https://github.com/ruizhi-lab/gentoo-overlay.git
emaint sync -r ruizhi-overlay
emerge -av kde-misc/latte-dock-ng
```

## Fedora (44+)

Install the prebuilt package from Fedora COPR:

```bash
sudo dnf copr enable ruizhi-lab/latte-dock-ng
sudo dnf install latte-dock-ng

# Upgrade all packages and refresh repository metadata
sudo dnf update --refresh
```

Restart Latte after upgrading to run the new binary. `--refresh` avoids using
cached repository metadata that predates a new COPR release.

To build from source instead, install these dependencies:

```bash
sudo dnf install \
  cmake extra-cmake-modules \
  qt6-qtbase-devel qt6-qtdeclarative-devel qt6-qtwayland-devel \
  kf6-plasma-devel plasma-activities-devel plasma-activities-stats-devel plasma-workspace-devel kwayland-devel \
  kf6-kconfig-devel kf6-kcoreaddons-devel kf6-kguiaddons-devel kf6-kdbusaddons-devel \
  kf6-kcmutils kf6-kirigami kf6-knewstuff \
  kf6-kdeclarative-devel kf6-kitemmodels-devel kf6-kxmlgui-devel kf6-kiconthemes-devel \
  kf6-kio-devel kf6-ki18n-devel kf6-knotifications-devel \
  kf6-knewstuff-devel kf6-karchive-devel kf6-kglobalaccel-devel \
  kf6-kcrash-devel kf6-kwindowsystem-devel kf6-kpackage-devel kf6-ksvg-devel \
  plasma-wayland-protocols-devel wayland-devel \
  layer-shell-qt-devel \
  gcc-c++ make gettext git pkgconf-pkg-config
```

## openSUSE Tumbleweed

Install from the `ruizhi-lab/latte-dock-ng` COPR repository. Follow the
openSUSE-specific repository instructions shown on the
[COPR project page](https://copr.fedorainfracloud.org/coprs/ruizhi-lab/latte-dock-ng/).

Use COPR on Tumbleweed x86_64 only; openSUSE Leap with Plasma 5 is unsupported.
To build from source instead, install these dependencies:

```bash
sudo zypper install \
  cmake extra-cmake-modules \
  qt6-base-devel qt6-declarative-devel qt6-wayland-devel \
  libplasma6-devel plasma6-activities-devel plasma6-activities-stats-devel plasma6-workspace-devel kwayland6-devel \
  kf6-kconfig-devel kf6-kcoreaddons-devel kf6-kguiaddons-devel kf6-kdbusaddons-devel \
  kf6-kcmutils kf6-kirigami kf6-knewstuff \
  kf6-kdeclarative-devel kf6-kitemmodels-devel kf6-kxmlgui-devel kf6-kiconthemes-devel \
  kf6-kio-devel kf6-ki18n-devel kf6-knotifications-devel \
  kf6-knewstuff-devel kf6-karchive-devel kf6-kglobalaccel-devel \
  kf6-kcrash-devel kf6-kwindowsystem-devel kf6-kpackage-devel kf6-ksvg-devel \
  plasma-wayland-protocols wayland-devel \
  layer-shell-qt6-devel \
  gcc-c++ make gettext git pkgconf
```

## Mageia Cauldron (Mageia 11 development)

Install from the `ruizhi-lab/latte-dock-ng` COPR repository using the
Mageia-specific repository instructions shown on the
[COPR project page](https://copr.fedorainfracloud.org/coprs/ruizhi-lab/latte-dock-ng/).
The Mageia build target is Cauldron. Confirm its latest build succeeded before
installing. Alternatively, download the Mageia RPM from
[GitHub Releases](https://github.com/ruizhi-lab/latte-dock-ng/releases). Do not
use the Fedora or openSUSE RPM. For a source build, install:

```bash
sudo dnf install \
  cmake extra-cmake-modules \
  qtbase6-common-devel lib64qt6base6-devel \
  lib64qt6qml-devel lib64qt6quick-devel lib64qt6quickwidgets-devel \
  lib64qt6wayland-devel lib64qt6waylandclient-devel \
  lib64plasma-devel lib64plasmaactivities-devel lib64plasmaactivitiesstats-devel \
  lib64plasma-workspace-devel lib64kwayland-devel \
  lib64kf6config-devel lib64kf6coreaddons-devel lib64kf6guiaddons-devel lib64kf6dbusaddons-devel \
  lib64kf6kcmutils6 lib64kirigami6 lib64kf6newstuffcore6 \
  lib64kf6declarative-devel lib64kf6itemmodels-devel lib64kf6xmlgui-devel lib64kf6iconthemes-devel \
  lib64kf6kio-devel lib64kf6i18n-devel lib64kf6notifications-devel \
  lib64kf6newstuff-devel lib64kf6archive-devel lib64kf6globalaccel-devel \
  lib64kf6crash-devel lib64kf6windowsystem-devel lib64kf6package-devel lib64kf6svg-devel \
  plasma-wayland-protocols-devel lib64wayland-devel lib64glvnd-devel \
  lib64layer-shell-qt-devel \
  gcc-c++ make gettext git pkgconf-pkg-config
```

## Building and Installing

**Recommended: use the install script.** It auto-detects available memory to prevent
out-of-memory failures on systems with limited RAM:

```bash
git clone https://github.com/ruizhi-lab/latte-dock-ng.git
cd latte-dock-ng
bash install.sh
```

The install script automatically:
- Picks an optimal number of parallel compile jobs based on available RAM
- Handles user-level (`~/.local`) vs system-level (`/usr`) installation
- Runs pre-install cleanup to avoid stale file conflicts

### Memory limits and OOM

Compiling C++ with many parallel jobs can consume 1-2 GiB per job. On machines with
limited RAM (VMs, single-board computers), cap the parallelism:

```bash
bash install.sh --jobs 1    # safest, slowest
bash install.sh --jobs 2    # good for 4 GiB VMs
```

### Manual build (not recommended)

If you prefer to build manually:

```bash
git clone https://github.com/ruizhi-lab/latte-dock-ng.git
cd latte-dock-ng
mkdir build && cd build
cmake .. -DCMAKE_INSTALL_PREFIX=/usr
cmake --build . --parallel $(nproc)   # may OOM on small systems
sudo cmake --install .
```

### Install script options

```bash
bash install.sh --help
bash install.sh Debug                  # debug build
bash install.sh --no-clean             # skip pre-install cleanup
bash install.sh --clean --purge-user-data
bash install.sh --user Debug           # install to ~/.local for testing
bash install.sh --jobs 2               # cap at 2 parallel compile jobs
```

## Uninstall

```bash
bash uninstall.sh
```

Uninstall script options:

```bash
bash uninstall.sh --help
bash uninstall.sh --dry-run
bash uninstall.sh --purge-user-data
bash uninstall.sh --manifest build/install_manifest.txt --dry-run
```

## NixOS

### Prerequisites

Unlike the distros above, there's no dependency-install step. `default.nix`
lists every Qt6/KF6 dependency and Nix builds them all in one derivation.
Have Nix installed and skip straight to building.

For getting it installed on your system rather than building it locally,
add the flake as an input and apply its module:

```nix
# flake.nix
inputs.latte-dock-ng.url = "github:ruizhi-lab/latte-dock-ng";

# in your nixosSystem call
nixpkgs.lib.nixosSystem {
  system = "x86_64-linux";
  modules = [
    inputs.latte-dock-ng.nixosModules.default
    ./configuration.nix
  ];
};
```

The module exposes `pkgs.latte-dock-ng`; add it to system packages:

```nix
# configuration.nix
{ pkgs, ... }: {
  environment.systemPackages = [ pkgs.latte-dock-ng ];
}
```

Or build/run it without adding it as a flake input:

```bash
nix build github:ruizhi-lab/latte-dock-ng
nix run github:ruizhi-lab/latte-dock-ng
```

### Ad hoc, without cloning

```bash
nix-build -E 'with import <nixpkgs> {}; callPackage (fetchTarball "https://github.com/ruizhi-lab/latte-dock-ng/archive/refs/heads/main.tar.gz") {}'
./result/bin/latte-dock-ng
```

### From a local clone

```bash
git clone https://github.com/ruizhi-lab/latte-dock-ng.git
cd latte-dock-ng
nix-build
./result/bin/latte-dock-ng
```

## Docker Build Verification

Docker images are provided to verify the build on each supported distribution.
Local Docker runs use USTC mirrors by default for fast package downloads in
China; GitHub Actions explicitly uses each distribution's official mirrors.

```bash
cd docker
docker compose run --rm arch       # Arch Linux
docker compose run --rm fedora     # Fedora 44
docker compose run --rm opensuse   # openSUSE Tumbleweed
docker compose run --rm mageia     # Mageia Cauldron (Mageia 11 development)
docker compose run --rm ubuntu     # Ubuntu 26.04
docker compose run --rm debian     # Debian 13 (current stable)
docker compose run --rm nixos      # NixOS (nixos-unstable)
```

For Debian testing and Gentoo, run the corresponding verifier directly:

```bash
docker build -f Dockerfile.debian-testing -t latte-debian-testing .
docker run --rm -v "$PWD/..:/src:ro" --tmpfs /build:exec -w /build \
  latte-debian-testing bash /src/docker/verify-install.sh debian-testing
docker build -f Dockerfile.gentoo -t latte-gentoo .
docker run --rm -v "$PWD/..:/src:ro" --tmpfs /build:exec -w /build \
  latte-gentoo bash /src/docker/verify-ebuild-gentoo.sh
```

Each command builds a container with all dependencies installed, then runs
the full verification pipeline:
1. cmake configure + compile
2. cmake --install (system install to /usr)
3. Verify key installed files exist
4. Uninstall dry-run + actual uninstall
5. Verify files are removed

A successful run ends with `=== <DISTRO>: BUILD + INSTALL + UNINSTALL SUCCESS ===`.

The GitHub Actions package job additionally builds and installs the native
`pkg.tar.zst`, RPM, or DEB with the target distribution's package manager.

`nixos` follows a different pipeline, since there's no apt/cmake step: it
builds `default.nix` with `nix-build`, then installs and uninstalls it with
`nix-env` instead of `install.sh`/`uninstall.sh`. `Dockerfile.nixos` points
at `nixos-unstable` explicitly and refreshes it at build time, rather than
relying on whatever channel ships with the base image.
