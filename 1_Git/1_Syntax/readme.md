# Git Setup syntax

## Clone, Pull

- Create a local copy  
  `git clone`

- Update the local copy
   `git pull` or  
   `git fetch + git merge`

## Remote

- Add a remote URL
   `git remote add origin https://github.com/USERNAME/REPOSITORY.git`
- Change the remote's URL
   `git remote set-url`
if you are updating to an HTTPS:
   `git remote set-url https://github.com/USERNAME/REPOSITORY.git`
if you are updating using SSH:
   `git remote set-url git@github.com:USERNAME/REPOSITORY.git`
- List existing remotes
   `git remote -v`

## Access Token

- Create an access token on platform (Github, GitLab, SourceForge)
  - GitHub: Your profile > Settings > Devloper setting > Personal access tokens

- Name it, Scope it, Generate it, Secure it

- Save the credentials
  - Enable credential memory
     `git config --global credential.helper cache`
  - You may update the default cache timeout
     `git config --global credential.helper 'cache --timeout=3600'`