# luajson fork (github.com/dossy/luajson)

## Background
The upstream `luajson 1.3.4-1` on LuaRocks is broken because:
- Its source URL uses `git://` which GitHub deprecated in 2021
- It lacks the lpeg 1.1 compatibility fix present in the upstream git master branch

## What we did
Created a custom fork release to distribute the fixed package via GitHub Releases.

### Key files added
- `rockspecs/luajson-1.3.4.dossy-1.rockspec` — custom rockspec versioned `1.3.4.dossy-1`, source points to `git+https://github.com/dossy/luajson.git` at tag `v1.3.4.dossy`
- `.github/workflows/release.yml` — GitHub Actions workflow triggered by `v*` tag pushes; runs `luarocks pack` and uploads the `.src.rock` to a GitHub Release
- `README.md` — added install instructions at the top

### Version naming
LuaRocks version format is `PACKAGE_VERSION-REVISION` where revision must be numeric. To create a distinguishable fork version, we used `1.3.4.dossy` as the package version (appending `.dossy` as an extra dot-separated segment) with revision `1`, giving `1.3.4.dossy-1`.

### Why git+https:// not git://
`git://` is the unauthenticated git protocol (not SSH) — GitHub dropped support in 2021. `git+https://` is the modern replacement for public repos in LuaRocks rockspecs.

### Releasing
```bash
git tag v1.3.4.dossy
git push origin v1.3.4.dossy
```
GitHub Actions builds `luajson-1.3.4.dossy-1.src.rock` and publishes it to the release.

### Installing
```bash
luarocks install https://github.com/dossy/luajson/releases/download/v1.3.4.dossy/luajson-1.3.4.dossy-1.src.rock
```

### Notes
- GitHub Actions may be disabled by default on forked repos — check Settings → Actions → General
- `luarocks make rockspecs/luajson-1.3.4.dossy-1.rockspec` tests the build locally (uses local source, ignores the source URL)
- `luarocks lint` validates rockspec syntax
