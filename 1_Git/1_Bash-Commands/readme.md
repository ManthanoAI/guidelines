# Git Setup Syntax

- [Clone or Pull](#Clone-or-Pull)
- [Remote](#Remote)
- [Access Token](#Access-Token)

## Clone-or-Pull

- Create a local copy  

  `git clone`

- Update the local copy

   `git pull`  
   or  
   `git fetch + git merge`

## Remote

- Add a remote URL called origin

   `git remote add origin https://github.com/USERNAME/REPOSITORY.git`

- Change the remote's URL

   `git remote set-url`

  - if you are updating using HTTPS:

    `git remote set-url https://github.com/USERNAME/REPOSITORY.git`

  - if you are updating using SSH:

    `git remote set-url git@github.com:USERNAME/REPOSITORY.git`

- List existing remotes

   `git remote -v`

## Access-Token

- Create an access token on platform (Github, GitLab, SourceForge)
  - GitHub: Your profile > Settings > Devloper setting > Personal access tokens

- Name it, Scope it, Generate it, Secure it, Use it

- Save the credentials
  - Enable credential memory

     `git config --global credential.helper cache`

  - You may update the default cache timeout (1h = 3600s)

     `git config --global credential.helper 'cache --timeout=36000'`

  - Login into your account, use the generated token, the token should be saved

## Env-Variables
- Never safe your credentials to a git, however if your system is hacked also env variables will be accessible

- Save your access token into a global variable
   - `cd`
   - `nano .bash_profile`
   - Add `export GHUSER='username'`
   - Add `export GHTOKEN='token'`
- Save your access token into local .env file
   - create env file `credentials.env`
   - Add `GHUSER='username'`
   - Add `GHTOKEN='password'`
   - Add `credentials.env` to `gitignore`