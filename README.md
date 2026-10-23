# [vmlinux-to-elf](https://flathub.org/apps/details/re.fossplant.vmlinux-to-elf)

This repository contains a Flatpak template for building the https://github.com/marin-m/vmlinux-to-elf GUI

## Utilities

These command will generate a `python3-modules.json` file that can serve as a template for the dependencies included from `re.fossplant.vmlinux-to-elf.yaml`:

```bash
cd
git clone git@github.com:flatpak/flatpak-builder-tools.git
git clone git@github.com:flathub/re.fossplant.vmlinux-to-elf.git

cd ~/flatpak-builder-tools/pip
uv add PyYAML
uv sync --all-groups --frozen
source .venv/bin/activate

cd ~/re.fossplant.vmlinux-to-elf
~/flatpak-builder-tools/pip/flatpak-pip-generator --yaml vmlinux-to-elf[gui] --checker-data -o python3-modules.yaml
```

Note 1: add `--use-deprecated=legacy-resolver` to the `pip3 install` command for the `lz4` module in order to bypass the `Inconsistent version: filename has '4.4.5', but metadata has '0.0.0'` error.

Note 2: Don't keep `pygobject`/`pycairo` in the dependencies as these are already present in the base Flatpak environment.
