 dotfiles
==========
[![Build Status](https://travis-ci.org/chaos-bodensee/role_dotfiles.svg?branch=master)](https://travis-ci.org/chaos-bodensee/role_dotfiles)

<a href="https://galaxy.ansible.com/do1jlr/dotfiles"><img width="80px" src="https://galaxy.ansible.com/assets/galaxy-logo-02.svg"/></a>

### Get it directly from Ansible Galaxy
```bash
$ ansible-galaxy install do1jlr.dotfiles
```

Function of this role
-----------------------
Ansible role to deploy some dotfiles which may be useful

Affected files:
```ini
/etc/bash.bashrc
~/.bashrc
~/.vimrc
```
 our variables:
---------------
```ini
# enable basic version check for this role
# set it to true to use it (recomended)
submodules_versioncheck: false

# for some ansible features we need the python selinux package at fedora
# disable it, if you don't want it
dotfiles__install_python_selinux: true

# modify bashrc
base__modify_bashrc: true

# list of aliases used in bashrc
base__aliases:
  - { alias: "ls", command: "ls ", color: True }
  - { alias: "grep", command: "grep", color: True }
  - { alias: "ll", command: "ls -alF", color: False }
  - { alias: "la", command: "ls -A", color: False }
  - { alias: "l", command: "ls -CF", color: False }
  - { alias: "lz", command: "ls -Z", color: False }
  - { alias: "EDITOR", command: "/usr/bin/vim", color: False }
  - { alias: "VISUAL", command: "/usr/bin/gedit", color: False }
  - { alias: "gitsubpull", command: 'git submodule foreach "(git checkout $(git symbolic-ref --short refs/remotes/origin/HEAD | sed "s@^origin/@@"); git pull)"', color: False }
  - { alias: "pwgen", command: "/usr/bin/pwgen --num-passwords=3000 --numerals --capitalize --secure --no-vowels  --symbols 42 | grep -v '0' | grep -v 'o' | grep -v 'O' | grep -v '\"' | grep -v 'I' | grep -v 'l' | grep -v '1' | grep -v '´' | grep -v '@'  | tail -1 ", color: false }


# enable bash completion
base__bash_completion_enabled: true

# fancy promt
base__user_promt: '\[\033[01;33m\] $(printf "\xE2\x9D\xA4") \[\033[01;32m\]\u\[\033[01;36m\]@\[\033[01;32m\]\H\[\033[01;34m\] <\A> \[\033[01;35m\] \j \[\033[01;36m\] \w \[\033[01;33m\]\n\[\033[01;33m\] $(git branch 2>/dev/null | sed -n "s/* \(.*\)/\1 /p")$\[\033[01;00m\] '
base__root_prompt: '\[\033[01;31m\] $(printf "\xE2\x9D\xA4") \[\033[01;32m\]\u\[\033[01;36m\]@\[\033[01;32m\]\H\[\033[01;34m\] <\A> \[\033[01;35m\] \j \[\033[01;36m\] \w \[\033[01;33m\]\n\[\033[01;33m\] $(git branch 2>/dev/null | sed -n "s/* \(.*\)/\1 /p")$\[\033[01;00m\] '

# log terminal to syslog
base__log_to_syslog: true

# modify bash history
history_control: 'ignoreboth'
history_size: '-1'
history_file_size: '-1'

# optional additional entries to bashrc
base__additional_bashrc_lines: []
# - eval `foo`
# - tmux new-session

# optionally allow custom bashrc for root
base__allow_own_root_bashrc: false

# otional custom commands
base__additional_bashrc_lines: []
# - eval `foo`
# - tmux new-session

# optionally allow custom bashrc for root
base__allow_own_root_bashrc: false

# otional custom commands
base__custom_config: []
#  - { user: "l3d", cmd: "eval $(keychain --eval --quiet id_ed25519)"

# show hidden files in ranger
base__ranger_hidden_files: true

accounts:
  - "{{ ansible_user_id }}"
```

Please have a look into ``defaults/main.yml`` for more configuration options!
