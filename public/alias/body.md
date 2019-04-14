# 世の中のエンジニアのalias設定
reireias

---

先日、同僚と「世の中のエンジニアはターミナルにどんなalias設定をしているんだろう？」という談義になったので、GitHub上の**1000リポジトリ**のコードから調査してみました。

---


## aliasとは
wikipediaより
>UNIXなどにおいてコマンドを別名で登録したもの。別名を登録するコマンド名。

- 長いコマンドやいつも利用するオプションを毎回入力するのは手間ですよね？
- ターミナルの設定ファイルにaliasを記述することで、別名として定義することが可能というわけです。

---

## 調査方法
- GitHub APIを利用
- `dotfiles`トピックが付いているリポジトリを1000件、スター数でソート
- `.bashrc`、`.bash_profile`、`.zshrc`、`.zsh_profile`というファイル名でリポジトリ内を検索
  - 先頭のドットはあっても無くてもよい
- ファイル中から`alias`を含む行を抽出
- 対象ファイルは**1602ファイル**となった

API実行のソースコードは[こちら](https://github.com/reireias/dotseeker)

---

## 結果
とりあえず、登場回数の多い順とアルファベット順をそれぞれgistに掲載しておきます。

### 登場回数の多い順
https://gist.github.com/reireias/b986af3382d41c962ca6e8a78664c651
### アルファベット順
https://gist.github.com/reireias/253ba410244e999a15002efb17311d34

---

## 紹介
当初はランキング形式で記事を書こうとおもったのですが、登場回数だけではあまりおもしろいランキングにならなかったので、グルーピングした結果や気になったaliasを紹介していきます。

---

## ls系
登場回数の上位にかなりがランクインしていました。
まあ、鉄板ですね。

```sh
alias ls='ls --color=auto'
alias ls='ls -G'
alias ll='ls -alF'
alias ll='ls -lh'
alias ll='ls -l'
alias la='ls -A'
alias la='ls -a'
alias l='ls -CF'
# こんなのも
alias l='clear && ll'
alias l='clear && ls'
```

---

## cd系
ディレクトリ移動系は下記のようなものがありました。
よく利用するディレクトリに素早く移動するためのコマンドがいくつかありました。

```sh
# よく利用するディレクトリの頭文字の連結
alias abc='cd ~/aaa/bbb/ccc'

# 'd'と言っても人それぞれ
alias d='cd ~/.dotfiles'
alias d='cd ~/Desktop'
alias d='cd ~/Documents/Dropbox'
alias d='cd ~/Dropbox'
```

---

意外とみんな定義していたやつ。
数字で表現するやり方はけっこう便利そうですね。

```sh
# ドットの数で表現
alias ..='cd ..'
alias ...='cd ../..'
alias ....='cd ../../..'

# 数字で表現
alias ..2='cd ../..'
alias ..3='cd ../../..'
```

---

## git系
gitコマンドは多い順に並べるとこんな感じでした。
私もほぼ同等のalias設定を行っています。

```sh
alias g='git'
alias ga='git add'
alias gd='git diff'
alias gs='git status'
alias gp='git push'
alias gb='git branch'
alias gst='git status'
alias gco='git checkout'
alias gf='git fetch'
alias gc='git commit'
```

---

## dotfiles関連
aliasを設定するdotfilesに関するaliasをいくつか紹介。
編集系は地味に便利そうなので、設定してみようかな。

```sh
# 省略度合いも人それぞれ
alias d='/path/to/dotfiles'
alias dot='/path/to/dotfiles'
alias dotfiles='/path/to/dotfiles'
# 編集系
alias zshrc='vi /path/to/dotfiles/.zshrc'
alias zshconfig='vi /path/to/dotfiles/.zshrc'
```

---

## apt系
主にubuntu向けの設定ですね。

```sh
# apt
alias agi='sudo apt install'
alias agr='sudo apt remove'
alias agu='sudo apt update'

# apt-get
alias ag='sudo apt-get'
alias agi='sudo apt-get install'
alias agr='sudo apt-get remove'
alias agu='sudo apt-get update'
```
ちなみに、`apt-get`より`apt`コマンドを利用したほうがよいです。
参考：[「apt-get」はもう古い？新しい「apt」コマンドを使ったUbuntuのパッケージ管理](https://linuxfan.info/package-management-ubuntu)

---

## bundle系
Ruby on Railsでお馴染みの`bundle`です。
こちらはいくつか流派があるようです。

```sh
alias b='bundle'
alias be='bundle exec'
alias bx='bundle exec'
alias bi='bundle install'
alias bo='bundle outdated'
alias bu='bundle update'
alias rc='bundle exec rails c'
```

---

## top系
意外と定義されていた系その2。
`cpu`や`mem`は忘れっぽい人にはいいかもしれないです。

```sh
# 人それぞれ
alias top='htop'
alias top='gtop'
alias top='vtop'
alias top='gotop'
# 別名
alias mem='top -o rsize'
alias cpu='top -o cpu'
```

---

## 安全策
`-i`(`--interactive`)オプションで上書き時には対話形式で質問するようにしておくやつ。

```sh
alias cp='cp -i'
alias mv='mv -i'
alias rm='rm -i'
```

---

## 宗教戦争系
使用すると宣戦布告とみなされるaliasもあるようです。

```sh
# 異教徒への攻撃
alias atom='code'
alias v='code'
alias emacs='vi'
# 熾烈なedit争い
alias ed='atom .'
alias ed='emacs --daemon'
alias ed='vim'
alias edit="emacs -nw"
alias edit='subl'
alias edit='subl3'
alias edit='vim'
```

---

## 1文字系
ちょっと過激な気はしますが、慣れると使いやすいです。
長くなるので参考になるor面白そうなもののみ。

```sh
# a
alias a='alias'
alias a='ansible'
alias a='apt'
alias a='apt-get'
alias a='atom'

# b
alias b='brew'
alias b='bundle exec'
alias b='bundle'
alias b='bundler'
alias b='cd ..'
```

---

```sh
# c
alias c='curl'
alias c='cd'
alias c='clear'
alias c='cat'
alias c='rails console'
alias c='pbcopy' # これは便利そう
# d
alias d='cd ~/.dotfiles'
alias d='cd ~/Desktop'
alias d='cd ~/Dropbox'
alias d='date +%Y%m%d'
alias d='docker' # これ使ってます
alias d='du -h -d=1'
alias d='git diff'
alias d='less' # display?
alias d='pwd'
```

---

```sh
# e
alias e='atom'
alias e='emacs'
alias e='emacsclient'
alias e='exit' # ちょっと過激かな？
alias e='vim'

# f
alias f='fg'
alias f='file'
alias f='find . -name'
alias f='finger'
alias f='fuck'
alias f='open -a Finder ./'
```

---

```sh
# g
alias g='git status'
alias g='git' # 鉄板その1
alias g='googleit' # ググる
alias g='googler' # ググる
alias g='grep --color=auto'
alias g='grep' # 鉄板その2

# h
alias h='cd ~' # home的な
alias h='git reset HEAD' # head的な
alias h='heroku'
alias h='history | grep'
alias h='history'
alias h='tldr' # これは普通に便利そう。help?
```

---

```sh
# i
alias i='sudo apt install --yes'

#j
alias j='jobs'
alias j='jump'

# k
alias k='kill -9'
alias k='kubectl' # 使ってる
alias k='kwrapper'
alias k='tree' # lの隣だから?
```

---

```sh
# l
# ほとんどls系でしたので割愛
# m
alias m='cd ~/Music && ls -a' # musicのm!!!
alias m='make'
alias m='man'
alias m='mkdir' # 個人的にはこれかなあ
alias m='rake db:migrate db:rollback && rake db:migrate db:test:prepare' # やりすぎ感
alias m='mv'
alias m='mvn'
# n
alias n='git checkout -b' # new branch
alias n='nano'
alias n='npm run'
alias n='npm' # 実はnodeよりもこっちの方が多く打つ？
alias n='nvim'
alias n='node'
```

---

```sh
# o
alias o='open' # ほぼこれの亜種

# p
alias p='cd ~/Documents/projects'
alias p='cd ~/Dropbox/Projects'
alias p='cd ~/Pictures && ls -a'
alias p='cd ~/Projects'
alias p='ping' # 意外と激戦区？
alias p='popd' # zshのAUTO_PUSHDとセットかな？
alias p='pwd'
alias p='python'
alias p='python3'
alias p='pacman' # ゲームじゃないよ
```

---

```sh
# q
alias q='exit' # これ以外あんまない

# r
alias r='cd / && ls -a' # rootのr
alias r='rails' # rails開発者はrはけっこう迷うかも?
alias r='rake'
alias r='ranger'
alias r='rgrep'
alias r='rm -i'
alias r='rspec'
alias r='screen -D -R'
alias r='source ~/.zshrc' # reload?
alias r='radian'
```

---

```sh
# s
alias s='cd ~/src'
alias s='git status'
alias s='ls' # タイポ対策
alias s='screen'
alias s='spring'
alias s='ssh -l root'
alias s='ssh'
alias s='sudo su'
alias s='sudo'
alias s='svn'
```

---

```sh
# t
alias t='date +"%H%M%S"' # time
alias t='telnet'
alias t='terraform'
alias t='tig'
alias t='tmux -2'
alias t='tmux attach'
alias t='tmux new-session -A -s main'
alias t='tmux'
alias t='tree -C'
alias t='tree -Cfh'
alias t='tree -I "node_modules"' # 私のかな？
```

---

```sh
# u
alias u='cd ..' # up

# v
alias v='code' # VSCode
alias v='vagrant'
# vimの一族
alias v='mvim'
alias v='nvim'
alias v='vi'
alias v='vim'

# w 特になし
```

---

```sh
# x
alias x='exit'
alias x='screen -A -x'
alias x='startx' # IBM?
alias x='/mnt/c/Windows/explorer.exe' # cygwinかな?

# y
alias y='yarn' # これ使おう
alias y='yaourt' # ArcLinux

# z
alias z='zathura' # PDFビューワーらしい
```

---

## その他
```sh
# 短いが...
alias _='sudo'

# オプションを覚えづらい場合はアリ？
alias allps='ps aux'

# カレントディレクトリのパスをクリップボードにコピー(cpwd, copypathなど)
alias pwdc='pwd | tr -d "\n" | pbcopy'
```

---

## 番外編

---

### global alias
- zshの機能
- aliasはコマンドの先頭でしか働かないが、`-g`オプション付きで定義すると、コマンドの途中でも展開される
- パイプ等でよく呼び出すコマンドで利用する

```sh
# 便利そうなものをいくつか
alias -g A='| awk'
alias -g C='| pbcopy' # copy
alias -g C='| wc -l' # count
alias -g G='| grep --color=auto' # 鉄板
alias -g H='| head' # 当然tailもね
alias -g L='| less -R'
alias -g X='| xargs'
```

---

### suffix alias
zshの機能
コマンドの末尾を見てよろしくやってくれる

```sh
alias -s gz='tar -xzvf' # ./hoge.tar.gz で展開できる
alias -s html='open' # ./index.html でブラウザで開く
# こんな定義も可能
alias -s {mp3,mp4,wav,mkv,m4v,m4a,wmv,avi,mpeg,mpg,vob,mov,rm}='mplayer'
```

---

## 感想
- aws系は少ない
  - CLIとしてけっこう理想のサブコマンド構成？
  - or どうせ補完するからalias不要？
- dockerとkubectlは思ったほどなかった
- 知らないコマンドの勉強にもなった
