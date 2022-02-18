---
title: "Git et SSH"
weight: 203
disableToc: true
---

Git permet de collaborer, et pour ce faire, il permet d'établir des connexions réseau, pour échanger, partager du code source.

Dans l'équipe Cloud Doctothon, on utilise git **exclusivement à travers des connexions `SSH`**.


Pour pouvoir "pousser" vos commit `git`, vers github, et en particulier dans l'[organisation Doctothon](https://github.com/Doctothon), vous aurez donc besoin d'un **paire de clefs SSH**.

Si vous avez déjà votre clef `SSH`, vous pouvez passer à l'étape suivante.


## Créez votre paire de clef SSH

* Si vous êtes sur Windows, exécutez les commandes ci dessous dans `Git Bash for Windows`, (`MacOS` et `GNU/Linux`, attention, passez en shell `bash`, en exécutant la commande `bash` dans votre terminal, attention, `Mac OS` est par défaut en `zsh`) sans comentaire :

```bash
export MONPTI_NOM_SANS_ESPACE="tryphon"
export DOCTOTHON_SSH_HOME=~/.ssh.doctothon
mkdir -p ${DOCTOTHON_SSH_HOME}
chmod 700 ${DOCTOTHON_SSH_HOME}

ssh-keygen -t rsa -b 4096 -C "${MONPTI_NOM_SANS_ESPACE}@cloud.doctothon.io" -P "" -f ${DOCTOTHON_SSH_HOME}/id_rsa

echo "Bien, vous avez désormais 2 nouveaux fichiers sur votre machine, dans le répertoire [${DOCTOTHON_SSH_HOME}] : "

ls -alh ${DOCTOTHON_SSH_HOME}
ls -alh ${DOCTOTHON_SSH_HOME}/id_rsa
ls -alh ${DOCTOTHON_SSH_HOME}/id_rsa.pub

echo ""
echo "Voci la valeur de votre clef publique (NE DONNEZ JAMAIS À PERSONNE VOTRE CLEF PRIVEE) : "
cat ${DOCTOTHON_SSH_HOME}/id_rsa.pub
```

## Ajoutez votre clef publique SSH aux clefs de votre utilisateur Github

* Sur https://github.com , dans le **menu settings** de votre utilisateur github :

![github menu user settings](/images/docto/gh_user_settings_menu.png)


* Dans la section "**SSH KEYS**" utilisez le bouton "**Add SSH Key**" pour ajouter votre clef publique à celles de votre utilisateur Github :

![github menu user settings](/images/docto/gh_user_ssh_key_menu.png)


## Testez la clef SSH de votre utilisateur Github


* Le test consistre à vérifier que vous arrrivez à vosu authentifier auprès de github, à l'aide de votre clef SSH privée :

```Bash
export DOCTOTHON_SSH_HOME=~/.ssh.doctothon

# will re-define the default identity in use
# https://docstore.mik.ua/orelly/networking_2ndEd/ssh/ch06_04.htm
ssh-add ~/.ssh.doctothon/id_rsa

export GIT_SSH_COMMAND='ssh -i ~/.ssh.doctothon/id_rsa'
ssh -Ti ${DOCTOTHON_SSH_HOME}/id_rsa git@github.com
# ssh -Ti ${DOCTOTHON_SSH_HOME}/id_rsa git@gitlab.com

```

* Et si vous souhaitez diagnostiquer la connexion SSH établie avec Github :

```Bash
export DOCTOTHON_SSH_HOME=~/.ssh.doctothon

# will re-define the default identity in use
# https://docstore.mik.ua/orelly/networking_2ndEd/ssh/ch06_04.htm
ssh-add ${DOCTOTHON_SSH_HOME}/id_rsa

export GIT_SSH_COMMAND='ssh -i ~/.ssh.doctothon/id_rsa'
ssh -Tvvvai ${DOCTOTHON_SSH_HOME}/id_rsa git@github.com
# ssh -Tvvvai ${DOCTOTHON_SSH_HOME}/id_rsa git@gitlab.com

```
