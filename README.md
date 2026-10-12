# Reproduction for issue of symlinks created by post-upgrade tasks are falsely converted into regular files   

Reproduction for https://github.com/renovatebot/renovate/discussions/46967

## Current behavior

When a Renovate post-upgrade task creates a symlink, it is then falsely converted into a regular file before the commit, resulting in a regular file instead of a symlink as part of the commit.  
See the post-upgrade tasks in the [`renovate.json`](./renovate.json) and [the resulting PR](https://github.com/jschacher-dg-i/renovate-reproduction-post-upgrade-task-eating-symlinks/pull/1/changes).

> **Side note**: post-upgrade tasks creating symlinks, which are already present in the repo, won't get converted. (See `symlink_to_dockerfile_already_existing` being untouched in the PR.)

### `config.js`

This was tested by running Renovate locally with the following `config.js`:

```js
module.exports = {
  username: "jschacher-dg-i",
  token: "github_pat_...",
  platform: "github",
  autodiscover: true,
  autodiscoverFilter: ["jschacher-dg-i/renovate-*"],
  allowedCommands: [".*"],
}

```

## Expected behavior

Renovate should leave symlinks as symlinks and commit them accordingly.
