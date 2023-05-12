Working in progress.

These scripts have been created by myself (using as reference tmux-sessionizer by the The Primeagen).

These scripts help me a lot in my tmux workflow.

# About myself:

I a senior Network engineer, I currently work as a mix of an Architect and Project Delivery engineer.
I AM NOT A PROGRAMMER, I am self tought in programming so most likely you will find bugs, or not the best code to
   achieve my goals, but it usually does the job I want.

# My system

   - OS: Gentoo
   - Window Manager: I3-WM
   - Terminal: ST
   - Shell: zsh

# Purpose of these scripts

I use a lot terminal based applications, so I spend a lot of time in my terminal and these scripts help me a lot with my
workflow. One of the main reason I use TMUX, is that even though I have 3 monitors in my setup, I like the ability of
having all in one terminal window and be able to organise it and jump into folders and projects quick.

# Scripts


|  Name               | Purpose                                                       |
|--------------------------|--------------------------------------------------------------|
| tmux-keys | Shows key bindings for either nvim or tmux from a user populated list |
| tmux-sipcalc | CLI subnet calculator |
| tmux-wiki | Easy way to search through wiki files and open them in neovim |
| tmux-ssh-session | SSH to a server from a user populated list in a new tmux session |
| tmux-ssh-split |  SSH to a server from a user populated list in existing tmux window in split pane mode |
| tmux-lxexplorer | opens nvim with Lexplore in a remote server user selected folder |
| tmux-sessionizer-session | Creates new tmux session on a folder selected by the user |
| tmux-sessionizer-split | Creates a new split pane in existing tmux window on a folder selected by the user |
| tmux-docker-net | Opens dvmfa90/net-tools docker container |

# Important notes

I am always in tmux, when I start my terminal, I have some code in my zsh config where it checks if there is an existing tmux
session and if doesn't, it starts a tmux session called "diogo". So everytime I open a terminal I will be already
attached to a tmux session.

# Overall requirements for these scripts to work:

- Enviroment variable called TMUXSCRIPTSDIR pointing to the path where these scripts will be located. EX: export TMUXSCRIPTSDIR=~/github/tmux-scripts
- Enviroment variable called SSHLISTDIR pointing to the path where the SSH servers list will be located. EX: export SSHLISTDIR=~/.config/ssh
- Enviroment variable called TMUXOPTIONSDIR pointing to the path where the folder options will be located. EX: export TMUXOPTIONSDIR=~/github/tmux-scripts/options
- Enviroment variable called TMUXKEYSDIR pointing to the path where the folder keys will be located. EX: export TMUXKEYSDIR=~/github/tmux-scripts/keys
- sipcalc installed for the sipcalc script
- FZF installed
- RIPGREP installed

# Instructions of each script + Demo video

## tmux-keys:

### Requirements:

- Two text files, one for tmux key bindings and another one with nvim key bindings. For these scripts to work they need
  to be called tmux.txt and nvim.txt, but of course you can change the code in the scripts if you want to use different
  names.

- Enviroment variable called TMUXKEYSDIR with the folder path that contains the two text files, example: export
  TMUXKEYSDIR=~/github/tmux-scripts/keys

### Tmux Keybinding example(to be added to your .tmux.conf):

bind -r K run-shell "tmux display-popup -w 40% -h 90% -E "$TMUXSCRIPTSDIR/tmux-keys""

### Usage:

So when I am in my terminal, if I press my tmux prefix + K, a pop up shows up with a menu(Cats the file
options/options_keys.txt) where I have the option to chose Tmux keys or Nvim keys.

No matter what option I chose, this will open tmux-keys script, if I chose tmux it opens in fzf tmux.txt file, if I
chose nvim it opens nvim.txt. This open the files using fzf, which means you can search on it for strings.



https://github.com/dvmfa90/tmux-scripts/assets/51400932/ddef6389-d9c4-41da-bec7-94e64a662fa1



## tmux-sipcalc:

### Requirements:

- sipcalc installed

### Tmux Keybinding example(to be added to your .tmux.conf):

bind -r M-c display-popup -w 70% -h 70% -E "tmux new-session -A -s test ~/scripts/tmux/tmux-sipcalc"


### Usage:

So when I am in my terminal, if I press my tmux prefix + ALT + c, a pop up shows up asking for subnet.
Once you type in the subnet and press enter, it will then run sipcalc + subnet entered and show the result. This is now
been added to a loop, so it asks again for user input to calculate a new subnet, if you press q or ctrl+c it will than
exit the script.
This means you can now "call" the script once, and calculate multiple subnets and exist when you done.


https://github.com/dvmfa90/tmux-scripts/assets/51400932/1bd2eab5-7f4f-46c6-a9f7-341c49b8a7b9


## tmux-ssh-session:

### Requirements:


- Text file, with list of servers you usually log on to via ssh. This works priv/pub key authentication for the servers
- Enviroment variable called SSHLISTDIR with the folder path that contains the list of servers, example: export SSHLISTDIR=~/.config/ssh

### Tmux Keybinding example(to be added to your .tmux.conf):

bind -r M-s run-shell "tmux display-popup -w 70% -h 40% -E "$TMUXSCRIPTSDIR/tmux-ssh-session""

### SSH text file list example:

==== HOME ====

diogo@192.168.100.11 - gns3client

diogo@192.168.100.10 - gns3server

diogo@192.168.100.12 - ubuntu-dev

diogo@192.168.100.13 - ubuntu-secure

### Usage:

So when I am in my terminal, if I press my tmux prefix + ALT + s, this runs tmux-ssh-session script.
The script cats the ssh list text file with fzf, and once you chose the server, it saves the first bit of the line,
using awk to a variable. It then creates a new tmux session where it ssh to the save variable.

So for example, if from the list I chose diogo@192.168.100.11 - gns3client, this will save diogo@192.168.100.11, then
when it starts the new tmux session it does ssh -Y diogo@192.168.100.11.

https://github.com/dvmfa90/tmux-scripts/assets/51400932/67300db7-2161-4bab-82b0-5cc10f628d5b


## tmux-ssh-split:

### Requirements:


- Text file, with list of servers you usually log on to via ssh. This works priv/pub key authentication for the servers
- Enviroment variable called SSHLISTDIR with the folder path that contains the list of servers, example: export SSHLISTDIR=~/.config/ssh

### Tmux Keybinding example(to be added to your .tmux.conf):

bind -r M-S run-shell "tmux display-popup -w 70% -h 40% -E "$TMUXSCRIPTSDIR/tmux-ssh-split""

### SSH text file list example:

==== HOME ====

diogo@192.168.100.11 - gns3client

diogo@192.168.100.10 - gns3server

diogo@192.168.100.12 - ubuntu-dev

diogo@192.168.100.13 - ubuntu-secure


### Usage:

So when I am in my terminal, if I press my tmux prefix + ALT + S, this runs tmux-ssh-split script.
The script cats the ssh list text file with fzf, and once you chose the server, it saves the first bit of the line,
using awk to a variable. It then creates a new tmux pane in split mode on the current tmux session,  where it ssh to the
saved variable.

So for example, if from the list I chose diogo@192.168.100.11 - gns3client, this will save diogo@192.168.100.11, then
when it starts the new tmux pane in splt mode and it does ssh -Y diogo@192.168.100.11.


https://github.com/dvmfa90/tmux-scripts/assets/51400932/10a72b96-e350-4464-a64a-b108db659417


## tmux-wiki:


### Tmux Keybinding example(to be added to your .tmux.conf):

bind -r M-w run-shell "tmux display-popup -w 70% -h 70% -E "$TMUXSCRIPTSDIR/tmux-wiki""

### Usage:

So when I am in my terminal, if I press my tmux prefix + ALT + w, this runs tmux-wiki script.
This will then open a pop up with fzf listing all files within ~/vimwiki folder.
I can than search for keyworks and when I press enter on the one I want open, it opens a pop up with nvim with the
select file open.

https://github.com/dvmfa90/tmux-scripts/assets/51400932/c0ff49bb-2f3d-4618-a671-ee3d7c4e4189

## tmux-docker-net:


### Tmux Keybinding example(to be added to your .tmux.conf):

bind -r M-n run-shell "tmux display-popup -w 80% -h 80% -E "$TMUXSCRIPTSDIR/tmux-docker-net""

### Usage:

So when I am in my terminal, if I press my tmux prefix + ALT + n, this runs tmux-docker-net script.
This will open a pop up where I am on the docker container shell.
This docker container is a public one I created dvmfa90/net-tools.

https://github.com/dvmfa90/tmux-scripts/assets/51400932/9f59ad1f-8596-4c84-a9ee-6bca7fa72ad9


## tmux-lxexplorer:

### Requirements:

- nvim with lexplore
- Text file, with list of servers you usually log on to via ssh. This works priv/pub key authentication for the servers
- Enviroment variable called SSHLISTDIR with the folder path that contains the list of servers, example: export SSHLISTDIR=~/.config/ssh


### Tmux Keybinding example(to be added to your .tmux.conf):

bind -r M-l run-shell "tmux display-popup -w 70% -h 70% -E "$TMUXSCRIPTSDIR/tmux-lxexplorer""


### Usage:

So when I am in my terminal, if I press my tmux prefix + ALT + l, this runs tmux-lxexplorer script.
This will open a pop up where I chose form a text file list a remote server.
Once chosen, it uses fzf and lists folders and subfolders of the remote host where I can serach for specific folders
Once I chose a folder open nvim with lexplore on the remote host selected folder, fomr here I can then browse and open a
file and edit it.


https://github.com/dvmfa90/tmux-scripts/assets/51400932/665b28d2-7db9-4104-860a-763dff02bb5e

## tmux-sessionizer-session:

### Tmux Keybinding example(to be added to your .tmux.conf):

bind -r f run-shell "tmux display-popup -w 70% -h 80% -E "$TMUXSCRIPTSDIR/tmux-sessionizer-session""

### Usage:

So when I am in my terminal, if I press my tmux prefix + f , this runs tmux-sessionizer-session script.
A pop up will list subfolders within a set of folders.
Once a folder is chosen, it lists all files within the selected folder.

1. You chose a file: This will open the file using nvim in a pop up.
2. You did not chose file, it will create a new session with the folder you selected.

The one video will show both exmaples.



https://github.com/dvmfa90/tmux-scripts/assets/51400932/eac466b5-5ac3-45a7-b37c-a151eebf07ce



## tmux-sessionizer-split:

### Tmux Keybinding example(to be added to your .tmux.conf):

bind -r F run-shell "tmux display-popup -w 70% -h 80% -E "$TMUXSCRIPTSDIR/tmux-sessionizer-split""

### Usage:

So when I am in my terminal, if I press my tmux prefix + F , this runs tmux-sessionizer-split script.
A pop up will list subfolders within a set of folders.
Once a folder is chosen, it lists all files within the selected folder.

1. You chose a file: This will open the file using nvim in a pop up.
2. You did not chose file, it will create a pane in split mode in your existing tmux window with the folder you selected.

The one video will show both exmaples.



https://github.com/dvmfa90/tmux-scripts/assets/51400932/831ca5d8-2cb9-4afe-b7de-39d0e2196c05

# TO DO:

- Create instalation script
- Working on version 2 of the scripts
