# Session-12 

# Shell Expansion: Shell History | Managing Shell History In RHEL
Your shell keeps a record of the commands you've executed, which is known as shell history. This feature is incredibly useful for repeating commands, editing previous commands, and analyzing your past actions.

## Re-executing previous command
Following command is used to re-execute the previously executed command.

```sh
$ !!             # Will execute the most recent command
```

## History
In linux terminal you can see all the previously executed commands using the `history` command.

```bash
$ history
```
You can also use the `history number` to repeat the command. For this you required the index number of the executed command.

```sh
$ !444
clear
```

> [!NOTE]
> Replace `444` with the actual number of the command you want to run from the history list.

You can also use the few character of the previously executed command to re-run it. Linux shell automatically recognises whcih previous command to execute.

```sh
$ echo Hello world!
Hello world!

$ !ec
echo Hello world!
Hello world!
```

## Search in history
You can press `Ctl + r` to search in the command.

## HISTSIZE && HISTFILESIZE
These are the environmental variables which defines how many number of commands shall the shell is going to store in the history

```sh 
$ echo $HISTSIZE    # Number of commands in memory
1000

$ echo $HISTFILESIZE    # Number of commands in the history file
1000
```

## HISTFILE
This is file location wheather linux stores all the commands
once logout all the commands are saved to this file

```sh
$ echo $HISTFILE
/home/prathamesh/.zsh_history
```

## Skip a command from history
if you want to skip any command you need to execute the command after a whitespace.


```sh
$ history | tail
 2199  env | grep -i HIST*
 2200  env | grep -i HIST.*
 2202  echo Hello world!
 2205  sudo su
 2206  history | tail
 2207  cd
 2209  sudo apt install hcitool
 2210  sudo apt install bluez
 2211  sudo apt install neofetch
 2212  clear

$  pwd              #Note there is a whitespace
/home/prathamesh

$ history | tail
 2199  env | grep -i HIST*
 2200  env | grep -i HIST.*
 2202  echo Hello world!
 2205  sudo su
 2206  history | tail
 2207  cd
 2209  sudo apt install hcitool
 2210  sudo apt install bluez
 2211  sudo apt install neofetch
 2212  clear
```
>[!NOTE]
 There is a whitespace while excuting `pwd` command.