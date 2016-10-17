# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

#echo $TERM
#xterm

# If not running interactively, don't do anything
case $- in
    *i*) ;;
      *) return;;
esac

source /etc/profile

non_root_user=`getent passwd 1001 | grep :1001: | sed -r 's/([a-zA-Z0-9]+):(.*)$/\1/g'`

export SERVER_ID=`hostname | sed -r 's/SERVER//g'`
export SERVER=`hostname`
export ALIAS='.alias_s'$SERVER_ID
export SERV_HOME=$HOME/$SERVER
export SHELL_CONFIG=.bashrc
export ROOT=root
export ROOT_GRP=root
export SSHFS=/usr/bin/sshfs

# Create var for sending with SSH
export CLIENT_HOST=$SERVER 

# setup quick folders for sharing among ubuntu cluster
for n in 1 2 4 5; do
    if [[ $n != $SERVER_ID ]]; then
	x=`printf "export SHARE%s=/Volumes/ub%s/home/ub%s" $n $n $n`
	eval $x
	x=`printf "export SHARE%s_SERVER=SERVER%s" $n $n`
        eval $x

	y=`printf "export SERV%s=/Volumes/ub%s/$J" $n $n`
	eval $y
	y=`printf "export SERV%s_SERVER=SERVER%s" $n $n`
	eval $y
   fi
done
if [[ $SERVER_ID != 3 ]]; then
    export SHARE3=/Volumes/mbp2/Users/admin
    export SHARE3_SERVER=SERVER3
fi

export BD=$SHARE2/BD_Scripts
#export GIT_BD=$J/BD_Scripts
#export GIT_SERV_HOME=$J/system_config
#export APORO=$J/aporo
#export APRINTO=$J/aprinto
#export IPY=$SERV_HOME/ipython
#export PYTHONPATH=$IPY/scripts/startup.py
export LIBDIR=/usr/local/lib/syslog-ng

export PKG_CONFIG_PATH=/usr/lib/pkgconfig/:$PKG_CONFIG_PATH

function assign() {  eval "$1=\$(cat; echo .); $1=\${$1%.}";}
#assign tmp < <(luarocks path --bin)
#eval $tmp

#export LUA_PATH=$LUA_PATH:$BD/Lua:$BD/Lua/luajit:$BD/Lua:$BD/Lua/lualib";/usr/local/openresty/luajit/share/lua/5.1/?.lua;"
#export LUA_CPATH=$LUA_CPATH";/usr/local/openresty/luajit/lib/lua/5.1/socket/?.so;"
#export LUAJIT_LIB=/usr/local/openresty/luajit/lib
#export LUAJIT_INC=/usr/local/openresty/luajit/include/luajit-2.1
#export LUA_DIR=/usr/lib/x86_64-linux-gnu/pkgconfig:/usr/include/lua5.1:/usr/local/openresty/luajit/bin/lua:/usr/lib/x86_64-linux-gnu/:/usr/local/openresty/luajit/:/usr/local/

#export LD_LIBRARY_PATH=/usr/local/lib/:/opt/drizzle/lib/:$LD_LIBRARY_PATH

#export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib/rsyslog/

#export LUA= /usr/local/openresty/luajit/bin/luajit-2.1.0-alpha
#export LUAINC= /usr/local/openresty/luajit/include
#export LUALIB= /usr/local/openresty/luajit/lib
#export LUABIN= /usr/local/openresty/luajit/bin

#export TERM=screen-256color
#export TERM=xterm-256color tmux
export TERM=xterm-color
export LANG="en_US.UTF-8"
export LANGUAGE="en_US:en"
export LC_COLLATE="C"
export CLICOLOR=1
#export LS_OPTIONS='--color=always'
#export GREP_OPTIONS='--color=always'
export HISTCONTROL=ignoredups:erasedups
export HISTTIMEFORMAT="%d/%m/%y %T  "
export HISTIGNORE='*sudo -S*'
export HISTSIZE=1000000
export HISTFILESIZE=10000000
shopt -s histappend
export PROMPT_COMMAND="echo \[\$(date +%H:%M:%S)\]\ "
#export PROMPT_COMMAND="history -n; history -w; history -c; history -r; $PROMPT_COMMAND"
export EDITOR=emacs
export LESS='-R'
export LESSOPEN='|~/.lessfilter %s'
# ---------------------------------------
# Git
#export GIT_CONFIG=$HOME/.gitconfig # set somewhere else apparently
#export GIT_TRACE=$HOME/.git/trace_log.txt

# check the window size after each command and, if necessary,
# update the values of LINES and COLUMNS.
shopt -s checkwinsize

# If set, the pattern "**" used in a pathname expansion context will
# match all files and zero or more directories and subdirectories.
shopt -s globstar

# make less more friendly for non-text input files, see lesspipe(1)
[ -x /usr/bin/lesspipe ] && eval "$(SHELL=/bin/sh lesspipe)"

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
    debian_chroot=$(cat /etc/debian_chroot)
fi

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
export color_prompt=yes
if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
unset color_prompt force_color_prompt

d=/etc/dircolors
test -r $d && eval "$(dircolors $d)"

# Add an "alert" alias for long running commands.  Use like so:
#   sleep 10; alert
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'


# enable programmable completion features (you don't need to enable
# this, if it's already enabled in /etc/bash.bashrc and /etc/profile
# sources /etc/bash.bashrc).
#if ! shopt -oq posix; then
#  if [ -f /usr/share/bash-completion/bash_completion ]; then
#    . /usr/share/bash-completion/bash_completion
#  elif [ -f /etc/bash_completion ]; then
#    . /etc/bash_completion
#  fi
#fi

_home=$HOME
_dir=$_home/.completers
if [ -d $_dir ]; then
    for i in `env ls $_dir`; do
	#echo $_dir/$i
	. $_dir/$i
    done
fi

if [ -f $_home/.scripts/.alias_shared ]; then
#    echo ".alias_shared"
    . $_home/.scripts/.alias_shared
fi
if [ -f $_home/.scripts/.alias_linux ]; then
#    echo ".alias_linux"
    . $_home/.scripts/.alias_linux
fi

if [ -f $SERV_HOME/local_config/$ALIAS ]; then
#    echo ".alias_(local)"
    . $SERV_HOME/local_config/$ALIAS
fi
