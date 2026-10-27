# git-hooks

Personal collection of Git hooks. Drop what you want into a repo (or your global `core.hooksPath`) and keep the rest out of the way.

## Hooks

| Script | Event | What it does |
| --- | --- | --- |
| [`hooks/commit-celebration`](hooks/commit-celebration) | `post-commit` | Plays a chime and a short terminal burst after a successful commit, then prints the subject. |

The celebration hook is fail-open: it never fails the commit, even if audio or the terminal animation cannot run. It skips the chime in CI.

Audio tries, in order: `pw-play`, `paplay`, `ffplay`, `mpv`, `mpg123`, then Windows MCI via PowerShell when running under WSL.

## Install

Git only runs hooks named after the event (`post-commit`, `pre-commit`, …). Point a repo or your global hooks path at a name Git recognizes:

```bash
# one repo
ln -s /path/to/git-hooks/hooks/commit-celebration .git/hooks/post-commit

# or globally (make sure other event names live in that directory too)
mkdir -p ~/.config/git/hooks
ln -s /path/to/git-hooks/hooks/commit-celebration ~/.config/git/hooks/post-commit
git config --global core.hooksPath ~/.config/git/hooks
```

The script looks for `hooks/assets/chime.mp3` next to itself, so keep that relative path intact (a symlink is fine).
