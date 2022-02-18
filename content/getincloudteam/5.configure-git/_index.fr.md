---
title: "Configure Git"
weight: 205
disableToc: true
---

# Configure _the_ `Git`

* Execute the below commands, **after** you changed the values of **at least** `YOUR_GITHUB_USER_NAME`, `YOUR_GIT_USERNAME`, and `YOUR_GIT_USEREMAIL` (you may change other values if you understand what yopu are doing, but they are optional) :

```bash
# -+- #
# -
# go to https://github.com/Jean-Baptiste-Lasselle
export YOUR_GITHUB_USER_NAME="Jean-Baptiste-Lasselle"
# ---
# Git is not github, and github is not git : you
# could just as well take any name, it won't prevent you from
# pushing to any github repository at all.
# ---
export YOUR_GIT_USERNAME="bernard tremplin"
export YOUR_GIT_USERNAME="${YOUR_GITHUB_USER_NAME}"
# same here : you could input ANY email address, it will work
export YOUR_GIT_USEREMAIL="votreadressemail@mimitcho.io"
export YOUR_GPG_SIGHNING_KEY="7B19A8E1574C2883"


git config --global user.name "${YOUR_GIT_USERNAME}"
git config --global user.email "${YOUR_GIT_USEREMAIL}"



git config --global commit.gpgsign false
git config --global user.signingkey "${YOUR_GPG_SIGHNING_KEY}"

# Now, to sign GIt commits, for example inside an SSH session
# (where TTY is a bit different ...)
export GPG_TTY=$(tty)


# end with SSH Agent config and github / ssh test
export DOCTOTHON_SSH_HOME=~/.ssh.doctothon

# will re-define the default identity in use
# https://docstore.mik.ua/orelly/networking_2ndEd/ssh/ch06_04.htm
ssh-add ${DOCTOTHON_SSH_HOME}/id_rsa

export GIT_SSH_COMMAND='ssh -i ~/.ssh.doctothon/id_rsa'
ssh -Tvvvai ${DOCTOTHON_SSH_HOME}/id_rsa git@github.com
# ssh -Tvvvai ${DOCTOTHON_SSH_HOME}/id_rsa git@gitlab.com

```

* check the configuration you just applied is there :

```bash
git config --global --list
```
