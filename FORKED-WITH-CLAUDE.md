# Forked with Claude

The upstream `luajson` package on LuaRocks.org hasn't been updated in years. The fix for lpeg 1.1
compatibility had already been merged into the upstream GitHub repo, but the maintainer hadn't
published an updated package to LuaRocks — leaving anyone who tried to `luarocks install luajson`
with a broken package.

Rather than waiting indefinitely for the upstream maintainer to act, I forked the repo and asked
Claude to help make the fork actually usable. Claude created a new rockspec pointing at the fork,
wrote a GitHub Actions workflow that automatically builds and publishes a `.src.rock` file to a
GitHub Release on every tag push, and added a one-liner install command to the README.

The result: anyone can install the working, fixed package immediately with:

```bash
luarocks install https://github.com/dossy/luajson/releases/download/v1.3.4.dossy/luajson-1.3.4.dossy-1.src.rock
```

No waiting on upstream. No manual packaging. Just fork, tag, and go.

---

*Even this write-up was authored by Claude.*
