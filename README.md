# Unofficial crDroid v11 (Android 15) for OnePlus 5 (cheeseburger)

Local manifests to build crDroid v11 (Android 15 version of crDroid) for the OnePlus 5 (cheeseburger) with the Android Security Bulletin patches merged from LineageOS 22.2.

## 1. Grabbing the source

Repo is a tool provided by Google that simplifies using Git in the context of the Android source:
- Repo docs: https://source.android.com/source/developing.html
- Git docs: https://git-scm.com/book

### 1.1 Installing dependencies and Repo

Several packages are needed in order to build crDroid. Example (we are using Ubuntu):
```bash
sudo apt install bc bison build-essential ccache curl flex g++-multilib gcc-multilib git git-lfs gnupg gperf imagemagick lib32ncurses-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses6 libncurses-dev libsdl1.2-dev libssl-dev libwxgtk3.2-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev
```
(Some of those packages may need adjustment for your linux distribution)

Install the Repo tool:
```bash
# create ~/bin and add to PATH for this session (or add to your shell profile)
mkdir -p ~/bin
export PATH=~/bin:$PATH

# download Repo
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo

# make Repo executable
chmod a+x ~/bin/repo
```

Tip: Add `export PATH=~/bin:$PATH` to `~/.bashrc` or your shell profile so Repo is available in future sessions.

### 1.2 Initializing Repo

Create a workspace and initialize the crDroid 15.0 manifest:
```bash
mkdir -p ~/crDroid
cd ~/crDroid
repo init -u https://github.com/crdroidandroid/android.git -b 15.0 --git-lfs --no-clone-bundle
```

### 1.3 Add my unofficial forks

**Warning:** these manifests target the OnePlus 5 (cheeseburger) only.

```bash
cd ~/crDroid
git clone -b 15.0 https://github.com/ES-Six/android_local_manifests .repo/local_manifests
```

### 1.4 Sync source tree

Sync the source tree (may take a long time on first run):
```bash
repo sync
```

Notes and useful flags:
- To recover from interrupted syncs or to force a fresh copy:  
  `repo sync --force-sync --no-tags --no-clone-bundle -j8` (adjust `-j` to match your bandwidth/CPUs).
- Use `repo sync -c` to only sync the current branch per project (saves time/space) when appropriate.

---

## 2. Building

Prepare the build environment:
```bash
. build/envsetup.sh
breakfast cheeseburger
```

Build using:
```bash
m -j4 bacon
```

Troubleshooting tips:
- Out-of-RAM: lower the `-j` value if you run out of RAM.
- Out-of-disk-space: ensure enough free space (Android tree can require ~380+ GB).
- If builds fail after repo sync, try `repo sync --force-sync` and a clean build: `mka clean` then rebuild.
