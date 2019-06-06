<h1>git log 시각화</h1>

1.

```
$ open ~/.gitconfig
```

2.

```
[alias]
        lg1 = log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
        lg1a = log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%x09%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
        lg2 = log --graph --abbrev-commit --decorate --format=format:'%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n''          %C(white)%s%C(reset) %C(dim white)- %an%C(reset)' --all
        lg3 = log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset)%C(bold yellow)%d%C(reset) %C(white)%s%C(reset) %C(bold green)(%ar)%C(reset) %C(dim white)- %an%C(reset)' --all
        lg4 = log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset)%C(bold yellow)%d%C(reset) %C(white)%s%C(reset) %C(bold green)(%ar)%C(reset) %C(dim white)- %an%C(reset)'
        lg = !"git lg4"
        lga = !"git lg3"
        st = status
        co = checkout
        nb = checkout -b
        com = checkout master
        po = push origin
```

3.

```
git lg
git lg1
git lg2
git lg3
```

