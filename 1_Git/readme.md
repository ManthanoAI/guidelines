# Git Guidelines

To be aligned with all developers in one organization we should follow a unified git structure.

- [Repository](#Repository)
- [Readme](#Readme)
- [Gitignore](#Gitignore)
- [Commits](#Commits)
- [Repository](#Authors)

## Repository

To create a repository (repo) please use following structure:
- one repo per project (even if the same client)
- name: choose wisely, lowercase, seperate-words-with-dashes
- format: [client]-[projectName], e.g. `manthano-mobile-app`
- permissions: default private

### Readme
- name: readme.md
- use: <a href="https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet" rel="nofollow">markdown syntax</a>
- language: english
- content: instructions, set-up, access, urls
- optional content: architecture, dependencies, access points (APIs), teams, resources

### Gitignore
- add .gitignore with initial commit
- use <a href="https://gitignore.io" rel="nofollow">Gitignore.io</a> to generate gitignore files
- remove dependencies (e.g. `node-modules`)
- remove system files (e.g. `.DS_Store`)

### Commits
- one feature per commit
- informative, clear, simple (not more than 50 characters)
- format: [emoji] [location] [message] [#bug tracker]
- message: Begin with a verb like: e.g. `add, update, remove, reformat, move, create, delete`
- bug tracker: Bug tracking ID e.g. `#420`
- location (Noncompulsary): seperated by > => e.g. `contact > form > parts >`

- MVP emojis: <a href="https://gitmoji.dev/">https://gitmoji.dev/</a><p>
  - :art: `:art:` Improve structure / format of the code  
  - :fire: `:fire:` Remove code or files  
  - :rocket: `:rocket:` Deploy stuff  
  - :construction: `:construction:` Work in progress  
  - :sparkles: `:sparkles:` Introduce a new feature  
  - :memo: `:memo:` Documentation updated  
- full examples:<p>
  - :art: contact > form > parts > updated view component #420
  - :memo: updated documentation
  - :sparkles: backtesting > implemented LSTM #1312

### Authors

<a href="https://github.com/Man7hano">Manthano</a>

Inspired by: <a href="https://github.com/immersive-garden/guidelines">Immersive Garden</a> (Thanks: :blue_heart:)
