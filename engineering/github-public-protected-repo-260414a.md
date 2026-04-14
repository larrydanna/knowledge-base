# Make a GitHub Repository Public but Protected

**Date:** 2026-04-14  
**Category:** engineering  
**Tags:** `github`, `repository`, `visibility`, `permissions`, `branch-protection`  
**Related:** *(none yet)*

---

## TL;DR

- Set the repository to **Public** if you want anyone to view it, clone it, and link to it
- A public repository is **not open for direct changes** unless you grant someone write access
- Protect `main`/`master` with branch protection or rulesets to restrict pushes, block force pushes, and optionally require pull requests
- Review collaborators and teams so **only you** have write or admin access
- Once a repository is public, **anyone can fork it**, and GitHub notes that visibility changes can disable existing push rulesets

---

## Understand what "public but protected" means

On GitHub, making a repository **public** means the code is visible to everyone. Anyone can browse it on the web, clone it locally, and fork it into their own account.

That does **not** mean other people can change your repository directly. Direct changes still require write access to *your* repository. Without that access, outsiders are limited to opening issues, discussions, or pull requests if those features are enabled.

---

## Change repository visibility

To make the repository publicly viewable:

1. Open the repository on GitHub.
2. Go to **Settings**.
3. In **Danger Zone**, use **Change repository visibility**.
4. Set the repository to **Public** and confirm.

Important caveat from GitHub Docs: when changing a repository from private to public, the code becomes visible to everyone, anyone can fork it, Actions logs become public, and **push rulesets are disabled**. If you were relying on rulesets before the visibility change, review and re-enable the protections you still want afterward.

---

## Limit who can change the repository

To keep the repository editable only by you:

1. Review **Settings -> Collaborators and teams** (or repository access controls if the repo belongs to an organization).
2. Remove any unnecessary collaborators.
3. Make sure only your account has **Write**, **Maintain**, or **Admin** access.

If no one else has write access, no one else can push directly to your repository.

---

## Protect the default branch

To reduce mistakes and lock down the main line of development, protect the default branch (`main` or `master`) with a branch protection rule or ruleset.

Useful protections include:

- **Restrict who can push** to the branch
- **Require a pull request before merging**
- **Block force pushes**
- **Block branch deletion**
- **Apply restrictions to administrators** if you want the rule to affect you too

For a solo repository, this gives you an extra layer of control even though you are the only writer.

---

## Reduce contribution surfaces

If your goal is public visibility with minimal outside interaction, disable features you do not want to manage.

Common choices:

- **Issues**
- **Discussions**
- **Wiki**

This does not affect read-only access to the code itself. It only reduces the ways other users can interact with the repository on GitHub.

---

## Practical checklist

Use this checklist when publishing a private repository:

1. Make the repository **Public**
2. Confirm only you have **write/admin** access
3. Re-check **rulesets/branch protection** after the visibility change
4. Protect `main` or `master`
5. Disable optional features you do not want
6. Assume the code is now **fully viewable and forkable**

---

## Sources

[1] [GitHub Docs - Setting repository visibility](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/managing-repository-settings/setting-repository-visibility)  
[2] [GitHub Docs - About protected branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches)  
[3] [GitHub Docs - Disabling issues](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/disabling-issues)
