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
