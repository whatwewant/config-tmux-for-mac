# Config Tmux For Mac

- install tmux@latest
- install tmux plugin with tpm

![pic](https://github.com/tmux-plugins/tmux-resurrect/raw/master/video/screencast_img.png)

## Install 

```bash
wget -O - https://raw.githubusercontent.com/whatwewant/config-tmux-for-mac/master/install | bash
```

<i>__Attention:__ This shell script contains lots of plugins and tools, if you have never installed, it may takes a little long time, about 15+ mins in good network.</i>

__bash code__
```bash
#!/bin/bash
# @author Zero <tobewhatwewant@gmail.com>

PROGRAM_NAME=tmux
DESTINATION=~/.tmux/plugins/tpm
URL="https://github.com/tmux-plugins/tpm.git"

which tmux >> /dev/null
if [ "$?" != "0" ]; then
  echo "Install tmux ..."
  brew install tmux
fi

which wget >> /dev/null
if [ "$?" != "0" ]; then
  echo "Install wget ..."
  brew install wget
fi

# Backup
[[ ! -d ~/.backup ]] && mkdir ~/.backup
if [ -f ~/.tmux.conf ]; then
    echo "Backup Tmux Configure to $HOME/.backup ..."
    [[ ! -d ~/.tmux ]] && mkdir ~/.tmux
    mv ~/.tmux.conf ~/.tmux
    tar -zcvf ~/.backup/tmux-$(date +%Y-%m-%d-at-%H-%M).tgz  ~/.tmux >> /dev/null 2>&1
fi
rm -rf ~/.tmux* >> /dev/null 2>&1

# DESTINATION
echo "Cloning $PROGRAM_NAME to $DESTINATION ..."
git clone $URL $DESTINATION

# Config file .tmux.conf
echo "Get new .tmux.conf ..."
wget https://whatwewant.github.io/confs/tmux.conf -O ~/.tmux.conf

# Reload TMUX environment so TPM is sourced:
echo "Reload TMUX environment ..."
tmux source-file ~/.tmux.conf

# Manual to click prefix + I to download tmux plugins
echo "Now You need munual to click prefix + I to download plugins"
```

## Thanks & LICENSE

MIT LICENSE.

