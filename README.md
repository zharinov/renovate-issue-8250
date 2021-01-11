# renovate-issue-8250

## About this repository
Repository to reproduce https://github.com/renovatebot/renovate/issues/8250

This repository requires two (random) PHP packages, installed via Composer:
- `"symfony/console": "^5.1"` - strict caret-style constraint
- `"symfony/event-dispatcher": "^5.1.0"` - less strict caret-style constraint

This demonstrates that the Renovate option `"rangeStrategy": "update-lockfile"` is not working as (I) expected, for not-strict caret-style version constraints.

## How to reproduce

```
npm install
GITHUB_TOKEN=YOUR_GITHUB_TOKEN
renovate --token=$GITHUB_TOKEN --print-config=true --log-level="debug" "annuh/renovate-issue-8250"   
```

**Expected behavior:**
PR for `symfony/console` only updates the `composer.lock`, because v5.2.1 matches `^v5.1.0`

**Actual behavior:**
PR for `symfony/console` updates `composer.json` AND `composer.lock`: https://github.com/annuh/renovate-issue-8250/pull/5

## Interesting logs
```
❯ composer outdated
symfony/console          v5.1.0 v5.2.1 Symfony Console Component
symfony/event-dispatcher v5.1.0 v5.2.1 Symfony EventDispatcher Component
```

```
# logs from renovate command

DEBUG: composer command (repository=annuh/renovate-issue-8250, branch=renovate/symfony-console-5.x-lockfile)
       "cmd": "composer",
       "args": "update symfony/console --with-dependencies --ignore-platform-reqs --no-ansi --no-interaction --no-scripts --no-autoloader"
DEBUG: Executing command (repository=annuh/renovate-issue-8250, branch=renovate/symfony-console-5.x-lockfile)
       "command": "composer update symfony/console --with-dependencies --ignore-platform-reqs --no-ansi --no-interaction --no-scripts --no-autoloader"
DEBUG: exec completed (repository=annuh/renovate-issue-8250, branch=renovate/symfony-console-5.x-lockfile)
       "cmd": "composer update symfony/console --with-dependencies --ignore-platform-reqs --no-ansi --no-interaction --no-scripts --no-autoloader",
       "durationMs": 399,
       "stdout": "",
       "stderr": "Loading composer repositories with package information\nUpdating dependencies\nLock file operations: 0 installs, 1 update, 0 removals\n  - Upgrading symfony/console (v5.1.0 => v5.2.1)\nWriting lock file\nInstalling dependencies from lock file (including require-dev)\nNothing to install, update or remove\n12 packages you are using are looking for funding.\nUse the `composer fund` command to find out more!\n"
DEBUG: Returning updated composer.lock (repository=annuh/renovate-issue-8250, branch=renovate/symfony-console-5.x-lockfile)
DEBUG: Commiting vendor files in vendor (repository=annuh/renovate-issue-8250, branch=renovate/symfony-console-5.x-lockfile)
DEBUG: Updated 1 package files (repository=annuh/renovate-issue-8250, branch=renovate/symfony-console-5.x-lockfile)
DEBUG: Updated 1 lock files (repository=annuh/renovate-issue-8250, branch=renovate/symfony-console-5.x-lockfile)
       "updatedArtifacts": ["composer.lock"]
DEBUG: 2 file(s) to commit (repository=annuh/renovate-issue-8250, branch=renovate/symfony-console-5.x-lockfile)
DEBUG: Committing files to branch renovate/symfony-console-5.x-lockfile (repository=annuh/renovate-issue-8250, branch=renovate/symfony-console-5.x-lockfile)
DEBUG: No file changes detected. Skipping commit (repository=annuh/renovate-issue-8250, branch=renovate/symfony-console-5.x-lockfile)
       "branchName": "renovate/symfony-console-5.x-lockfile",
       "fileNames": ["composer.json", "composer.lock"]
```
