# Steps to config Forge+Github
This will guide you on how to install the connection between your project in Github and Forge to deploy.  


1. Create a new site on Forge. Github repo link must be: `git@github-PROJECTNAME:DeboNL/PROJECTNAME.git`
   - This doesn't work yet, we will fix this along the way
2. Make sure you have the `forge-deployer` installed in your project
3. Add the required PRD repository secrets to your repository (if applicable):
   - FORGE_PRD_SERVER_ID
   - FORGE_PRD_SITE_ID
4. Add the required STG repository secrets to your repository (if applicable):
   - FORGE_STG_SERVER_ID
   - FORGE_STG_SITE_ID
5. Ssh into the server (`ssh forge@{IP}`)
6. Create ssh key: `ssh-keygen -t ed25519 -f ~/.ssh/PROJECT_NAME -C "forge-PROJECT_NAME" -q -N ""`
7. Copy ssh key `cat ~/.ssh/PROJECT_NAME.pub`
8. Add SSH key to Github project (Settings > Deploy keys)
9. Expand ssh config on the server (`vim ~/.ssh/config`):
    ```
    Host github-*
      HostName github.com
      User git
      IdentitiesOnly yes

    Host github-PROJECT_NAME
      IdentityFile ~/.ssh/PROJECT_NAME
    ```


---
## Good to knows:
👉 This works by a little Git quirk: We update the Forge 'Branch' to a release version, which is a tag. Then we trigger a deploy and Forge handles the tag the same way it would a branch, so no hacky stuff going on.

👉 It creates a custom SSH key for each site because a key can only be be used once in Github. If you only have one site per server, you can skip those steps.
