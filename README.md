This is an example repo for managing VS Code and other user settings in Code Ocean (across capsules and rebuilds) using https://www.chezmoi.io/.

**To use**:
 - fork this repository to your own github - your user settings will be stored there, so make it private or public as desired.
 - copy your repository url and add it to a CO capsule, as a Custom Key secret or environment variable named DOTFILES_REPO (secret is preferred so it doesn't sync to collaborators, but requires selecting "Set environment variable names" from the menu to the right of the secret to change the default CUSTOM_KEY to DOTFILES_REPO).
 - to add to your capsule, use one of two approaches:
    - use the latest version of the "code-server python extensions pack" base image
    - or add the following to your postInstall 
      ```
      if test -n "$DOTFILES_REPO"; then
        sh -c "$(curl -fsLS get.chezmoi.io)" -- init --apply $DOTFILES_REPO
      fi
      ```
      and the first time you launch the capsule after rebuilding, run `chezmoi update` from the terminal.
 - changes made to the user settings, keymappings, or tasks will be automatically pushed to your dotfiles repo and available for use in other capsules! (checked in the background every minute)
 - new changes will be pulled from github each time the capsule is launched.

  Other useful commands:
   - `chezmoi status` to check if changes are up-to-date and synced (no output means fully synced).
   - `chezmoi doctor` to resolve other weirdness.
   - In general, all changes are tracked in git and issues can be resolved by opening the chezmoi local repo (`chezmoi cd`) and using standard git commands. See the chezmoi docs for more...
