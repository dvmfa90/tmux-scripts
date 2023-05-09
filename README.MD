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
   - Shell: Fish shell, I know this might be a shock, but fish provides with a smart auto completion based on the actual
     path I am that others don't. When I am for example on my /home/ directory I like that when I do cd, the option
     available are actually folders in that /home/ directory.

# Purpose of these scripts

I use a lot terminal based applications, so I spend a lot of time in my terminal and these scripts help me a lot with my
workflow. One of the main reason I use TMUX, is that even though I have 3 monitors in my setup, I like the ability of
   having all in one terminal window and be able to organise it and jump into folders and projects quick.

# Scripts


|  Name               | Purpose                                                       |
|--------------------------|--------------------------------------------------------------|
| tmux-keys | Opens pop up menu that allows you to chose nvim or tmux so you can see keymaps. |
| tmux-sipcalc | Pop up where you type a subnet and it uses sipcalc to make subnet calculator |
| tmux-wiki | Fuzzy finds files in vimwiki folder so you can easily search through them and open in nvim |
| tmux-ssh-session | Opens a list of ssh servers in a text file, once you chose one it creates a new session where it ssh to the chosen server |
| tmux-ssh-split | Same as above but it rather than opening a new session it opens in existing session in a split pane |
| tmux-lxexplorer | Goes through the list of ssh servers, once you chose one, it lists folders/subfolders in remote user home directory, once you chose one, it open vim with lexplorer in the remote server and directory you chose |
| tmux-sessionizer-session | This particular one is opens a pop up with fzf where you can search for subfolders within folders set in the script, once you chose one it than lists the files within that folder, if you ctrl+c on that window, it creates a new session in the subfolder you chose, if you chose a file, it opens in a pop up nvim with the file |
| tmux-sessionizer-split | It does the same as the above one, but if you ctrl+c on the file screen, rather than opening the subfolder you chose ina  new session it opens in the exsiting session in a split pane, if you chose a file it does the same as the below and open in a pop up nvim witht he file you chose |
| tmux-docker-net | This one basically creates a docker container in a server I have, with --rm argument so it removes after I am done. This opens dvmfa90/net-tools docker container which I use to run some networking tools. |

# Gifs + Instructions of each script

## tmux-keys:

Inside the folder keys, there are 2 files, one called nvim.txt and another one called tmux.txt.

Each of the text files have some key bindings and explanation I added as sometimes I might forget some of them.

### Usage:

So when I am in my terminal, if I press my tmux prefix + K, a pop up shows up with a menu(Cats the file
options/options_keys.txt) where I have the option to chose Tmux keys or Nvim keys.

No matter what option I chose, this will open tmux-keys script, if I chose tmux it opens in fzf tmux.txt file, if I
chose nvim it opens nvim.txt. This open the files using fzf, which means you can search on it for strings.



https://github.com/dvmfa90/tmux-scripts/assets/51400932/68ac2eed-1456-4f0f-a24b-17b3d11e81be



## tmux-sipcalc:

This requires sipcalc to be installed in your pc.

### Usage:

So when I am in my terminal, if I press my tmux prefix + ALT + c, a pop up shows up asking for subnet.
Once you type in the subnet and press enter, it will then run sipcalc + subnet entered and show the result. You then
need to press q to exit.



https://github.com/dvmfa90/tmux-scripts/assets/51400932/45b9fd43-dd89-41d5-97b9-251ed5277915



## tmux-ssh-session:

This relies on a text file with ssh servers on it. Below an example of the format I have on my ssh text file:

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



https://github.com/dvmfa90/tmux-scripts/assets/51400932/6e5ac1ca-e756-4bc4-ad3d-9921a144b40b



## tmux-ssh-split:

This relies on a text file with ssh servers on it. Below an example of the format I have on my ssh text file:

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



https://github.com/dvmfa90/tmux-scripts/assets/51400932/75fb50d3-6c7f-424e-8b6d-782b20d52868



* TO DO:

   - Upload video showing workflow
   - Upload instruction
