#My PS1 and some "alias" for .bahsrc!

- [ ] PS1
 ```sh
PS1='\n\n<\#> \[\e[1m\][\[\e[0;4m\]\u\[\e[0;1m\]]\[\e[0;2m\] - \[\e[0;1m\][\[\e[0m\]\w\[\e[1m\]]\[\e[0;2m\] - \[\e[0;1m\]|\[\e[0;97;2m\]$(ip route get 1.1.1.1 | awk -F"src " '"'"'NR == 1{ split($2, a," ");print a[1]}'"'"')\[\e[0;1m\]|\n\[\e[2m\]>_\[\e[0m\]'
```

```sh
alias ls='ls -al --color=auto'
```

```sh
alias dir='dir --color=auto'
```

```sh
alias vdir='vdir -a --color=auto'
```

```sh
alias cat='batcat'
```

```sh
alias npp='/mnt/c/Program\ Files/Notepad++/Notepad++.exe'
```
