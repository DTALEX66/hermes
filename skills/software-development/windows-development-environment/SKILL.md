---
name: windows-development-environment
description: "Windows-specific quirks and fixes for Node.js/Next.js development: PATH shadowing, spawn EINVAL, lockfile registry portability, and environment setup."
tags: [windows, nodejs, nextjs, spawn, npm-ci, path, cross-platform]
---

# Windows Development Environment

## When to load

- Any task that involves **Node.js scripts**, **Next.js builds**, or **npm operations on Windows**.
- Any task where `child_process.spawn` or `npm ci` fails with obscure errors (`EINVAL`, `Exit handler never called!`, `ETIMEDOUT`).
- Any task where the wrong Node.js version is active and Hermes bundles Node v22.

## Key patterns

### 1. Node.js PATH shadowing

Hermes bundles Node v22 at `AppData/Local/hermes/node/node.exe`, but other tools may appear earlier in `$PATH`.

**Check:** `which node && node --version`

**Fix:** Prepend Hermes Node to PATH:
```bash
export PATH="$HERMES_HOME/node:$PATH"
```

### 2. `child_process.spawn` EINVAL on Windows

On Windows under Git Bash, `.cmd` files are not directly spawnable.

**Fix:** Use `cmd.exe` as the command:
```js
const child = spawn(
  process.platform === 'win32'
    ? process.env.COMSPEC || 'cmd.exe'
    : 'npx',
  process.platform === 'win32'
    ? ['/d', '/s', '/c', 'npx next build']
    : ['next', 'build'],
  { stdio: 'inherit', env, shell: false },
);
```

### 3. `package-lock.json` registry lock-in

When a lockfile hardcodes internal registry URLs, `npm ci` times out.

**Fix:** Regenerate:
```bash
rm -rf node_modules package-lock.json
npm install --ignore-scripts --no-audit --no-fund
```

### 4. Common Windows npm failures

| Error | Likely cause | Fix |
|---|---|---|
| `Exit handler never called!` | Registry unreachable | Regenerate lockfile |
| `spawn EINVAL` | `.cmd` without shell | Use `cmd.exe /d /s /c` |
| `ETIMEDOUT` | Internal registry URLs | Regenerate lockfile |
| Wrong Node version | PATH shadowing | Prepend Hermes Node |
