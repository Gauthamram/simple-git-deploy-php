# simple-git-deploy-php
simple git deploy snippet to automate continuous intergation 

## Forked from and modified as needed
https://github.com/markomarkovic/simple-php-git-deploy

## modified for iis server using php - modifications as follows
- Robocopy instead of rsync - since windows dont use rsync functionality
  - Robocopy returns various code that are more than 0 even when successfull
  - modification to check if command is robocopy then error handling accordingly
- Backup reomoved, run seperate as scheduled tasks
- Composer_working_dir config added to run artsian command after deployment

## Requirements

* `git`are required on the server that's running the script
  (_server machine_).
  - Optionally, `composer` is required for composer functionality (`USE_COMPOSER`
  option).
* The system user running PHP (e.g. `www-data`) needs to have the necessary
  access permissions for the `TMP_DIR` and `TARGET_DIR` locations on
  the _server machine_.
* If the Git repository you wish to deploy is private, the system user running PHP
  also needs to have the right SSH keys to access the remote repository.

## Usage

 * Configure the script and put it somewhere that's accessible from the
   Internet. The preferred way to configure it is to use `deploy-config.php` file.
   Rename `deploy-config.example.php` to `deploy-config.php` and edit the
   configuration options there. That way, you won't have to edit the configuration
   again if you download the new version of `deploy.php`.
 * Configure your git repository to call this script when the code is updated.
   The instructions for GitHub and Bitbucket are below.

### GitHub

 1. _(This step is only needed for private repositories)_ Go to
    `https://github.com/USERNAME/REPOSITORY/settings/keys` and add your server
    SSH key.
 1. Go to `https://github.com/USERNAME/REPOSITORY/settings/hooks`.
 1. Click **Add webhook** in the **Webhooks** panel.
 1. Enter the **Payload URL** for your deployment script e.g. `http://example.com/deploy.php?sat=YourSecretAccessTokenFromDeployFile`.
 1. _Optional_ Choose which events should trigger the deployment.
 1. Make sure that the **Active** checkbox is checked.
 1. Click **Add webhook**.
 
 ### Tips
 * You can have multiple scripts with different configurations. Simply rename
   the `deploy.php` to something else, for example `deploy_master.php` and
   `deploy_develop.php` and configure them separately. In that case, the
   configuration files need to be named `deploy_master-config.php` and
   `deploy_develop-config.php` respectively.
