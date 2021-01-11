# renovate-issue-8250

## About this repository
Repository to reproduce https://github.com/renovatebot/renovate/issues/8250

This repository requires two (random) PHP packages, installed via Composer:
- `"symfony/console": "^5.2.0"` - strict caret-style constraint
- `"symfony/event-dispatcher": "^5.2"` - less strict caret-style constraint

## How to reproduce

```
npm install
renovate
```

**Expected behavior:**

**Actual behavior:**


## Interesting logs
```
❯ composer outdated
symfony/console          v5.2.0 v5.2.1 Symfony Console Component
symfony/event-dispatcher v5.2.0 v5.2.1 Symfony EventDispatcher Component
```
