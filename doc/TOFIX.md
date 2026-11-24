# TOFIX

Findings from a code scan on 2026-10-04.

## Medium

- `README.md:2` - the repo promises "Demos for the dpkg packaging system" but contains no demo at all (only fleet config files, and `git log` shows none was ever committed). Add at least one real demo (e.g. a minimal package tree with `DEBIAN/control` built by `dpkg-deb --build`, plus a build step for it in `rsconstruct.toml`) or retire the repo.
- `rsconstruct.toml:1-17` - there is no `[processor.tera]` / `[analyzer.tera]`, so `tera.templates/.github/dependabot.yml.tera` is never rendered and `.github/dependabot.yml` is a hand-kept copy that will silently drift from the fleet template. Add the tera analyzer and processor (with `dep_auto = ["config/project.lua"]` and `src_dirs = ["tera.templates"]`) as in the other templated repos.

## Low

- `README.md:2` vs `config/project.lua:3` - two different descriptions ("Demos for the dpkg packaging system" vs "Demos for the dpkg system"); pick one, ideally by generating the README from `tera.templates/README.md.tera` like the rest of the fleet.
