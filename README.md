# ZSH 

Start using zsh as your default shell. There exist a lot of pre-configured themes and plugins for zsh.

https://github.com/robbyrussell/oh-my-zsh

Marcelka is currently quite happy with robbyrussell (default) zsh theme, you can further customize this to your needs. Also "agnoster" theme looks fine (if you have the proper fonts installed).

# ZSHRC

    # ALIASES
    
    # ls, the common ones I use a lot shortened for rapid fire usage
    alias ls='ls --color' #I like color
    alias l='ls -lFh'     #size,show type,human readable
    alias la='ls -lAFh'   #long list,show almost all,show type,human readable
    alias lr='ls -tRFh'   #sorted by date,recursive,show type,human readable
    alias lt='ls -ltFh'   #long list,sorted by date,show type,human readable
    alias ,='ls'
    alias ,,='la'
    
    # cd .. is a LOT of work!
    alias .='cd ../; ls'
    alias ..='cd ../../; ls'
    alias ...='cd ../../../; ls'
    alias ....='cd ../../../../; ls'
    
    # spawns new xterm in the current directory. 
    alias fork='nohup xterm -e zsh > /dev/null 2>&1 &'
    
    # find files recursively, ignore case 
    ff () { find ./ -iname "*${1}*" }
    
    # grep recursively, case insensitive (to me, this is default)
    gg () { grep -ir "${1}" * }
    
    # grep recursively, case sensitive (gc = Grep, Case)
    gc () { grep -r "${1}" * }
    
    # grep and search combined ftw (gs = Grep in Search results)
    # example: "gs .php todo" finds all todos in all .php files (well, it also matches sth.php.js)
    gs () { find ./ -iname "*${1}*" -exec grep -iH "${2}" \{\} \; }
    
    # 'cd' is one character too long. Also, after cd you usually want to know, where you are, so ls comes
    # handy
    function c() { cd "$@"; ls}
    
    function v() { vim "$@"; ls}
    
    # there are more project-specific aliases here. Examples:
    # alias ssskill='ssh ubuntu@skillandia.com'
    # alias cdskill='cd ~/projects/skillandia; ls'
    source ~/.aliases

# GIT 
zsh git plugin looks great:
https://github.com/robbyrussell/oh-my-zsh/blob/master/plugins/git/git.plugin.zsh

If you prefer something else, you may define your own aliases. For an inspiration, this is my .gitconfig:

    [user]
    	name = Tomas Kulich
    	email = tomas.kulich@gmail.com
    [push]
        # from SO: simple means git push will push only the current branch to the one that git pull would pull from
        # http://stackoverflow.com/questions/13148066/warning-push-default-is-unset-its-implicit-value-is-changing-in-git-2-0
    	default = simple
    [core]
        # I want to edit my commit messages in vim
        editor = vim
    [color]
        branch = auto
        diff = auto
        status = auto
    [alias]
        s = status
        co = commit
        ce = checkout
        b = branch -a
        r = reset
        rhh = reset HEAD --hard
        cf = clean -fd
        a = add
        d = diff
        pl = pull
        ps = push
        rmt = remote
        lgg = log --pretty=format:'%C(yellow)%h  %C(green)%an  %C(blue)%ar%Creset    %s'
        # awsm tree log 
        l = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit


# Command prompt
If you are like me (i.e. not satisfied by what zsh themes give you), you can set it up manually:

    PROMPT=$'%{\e]0;%3~\a\e\[00;32m%}% %3~$(git_super_status) > %{\e[0m%}'

I have no idea why this ugly piece of ascii-art works; it displays last 3 entries from the current path and git info. For git info I use git_super_status plugin; you can get it from https://github.com/olivierverdier/zsh-git-prompt, then you just source it in your .zshrc such as:

    source ~/zsh_plugins/zsh-git-prompt/zshrc.sh
    
