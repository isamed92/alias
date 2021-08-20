# Git Alias utils


## Installation 

Open your git config file or use this command in git bash and paste the alias do you need. 

1) See the file gitalias.txt.
2) Copy/paste anything you like into your own .gitconfig file.

###For windows 
Go to 
```C://Users/UserName/.gitconfig```

or in gitbash
```git config --global alias.[paste alias here] ```


#### Git status
```git config --global alias.s 'status -sb'```
#### Git log
```git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"```
