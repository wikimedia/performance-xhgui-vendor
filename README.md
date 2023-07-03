# XHGui-Vendor

Mirror of Composer-managed depencencies used by XHGui.

This repository is maintained for Wikimedia Foundation's production
installation of XHGui to facilitate security review and auditing, to
ensure offline and independent availability of our dependencies, and
to make it easy to perform code review on upstream changes.

## See also

* https://gerrit.wikimedia.org/g/operations/software/xhgui
* https://wikitech.wikimedia.org/wiki/XHGui

## Contribute

1. Ensure you're using [Composer] 2.5.1 locally (`composer --version`).

   Using the same version ensures minimal diffs, and eases review and
   rebasing. To use the correct Composer version, you can opt to
   use the Docker image provided by WMF CI:
   ```
   alias composer-wmf='docker run --rm -it -u "$(id -u):$(id -g)" -v "$PWD/.git:/src/.git:ro" -v "$PWD:/src" -w /src docker-registry.wikimedia.org/releng/composer-php74'
   ```
2. Edit composer.json to add/change the relevant library.

   The chosen versions should match or be in-range of the composer.json
   file in the `wmf_deploy` branch of the `operations/software/xhgui`
   repository. Or, when applying an upgrade from upstream, you should
   use the versions that the next deployment will need, and update the
   submodule in `operations/software/xhgui` right after the merge commit
   that pulls in upstream changes.

   You can automate editing of composer.json via
   `composer-wmf require <package> <version> --no-update`.
   This way automatically keeps the composer.json file sorted.
3. Run `composer-wmf update --no-dev` to download new files,
   and rebuild the autoloader.
4. Stage and commit changes as a Gerrit patch.
5. Review and merge changes.
6. Update the submodule `operations/software/xhgui@wmf_deploy`.

If in doubt, seek advice from regular commiters to this repository.
