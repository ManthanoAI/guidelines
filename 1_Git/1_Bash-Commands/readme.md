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

  - You may update the default cache timeout

     `git config --global credential.helper 'cache --timeout=3600'`

  - Login into your account, use the generated token, the token should be saved