# Pre-reqs
- Set up a Github Repository
- Have a Bash terminal with git installed
## Repository
First you need a code repository. Popular options include [github](https://github.com/), [bit-bucket](https://bitbucket.org/), [gitlab](https://bitbucket.org/), and self-hosted options. 
### Github
Navigate to [github](https://github.com/). In the top right corner hit Sign Up and create an account. 
## Bash terminal
Mac and Linux terminals can run git without need of downloading a shell. Windows comes with Powershell and Cmd Terminals, neither will work for this tutorial. If using windows please download a [git bash terminal](https://git-scm.com/install/windows). Downloading the git bash terminal for Linux or Mac is optional, links for downloading can be found on the same link.


## Instructions
1. Ensure you all pre-reqs are installed and ready for use.
2. Familiar self with commands and location of official documentation.
3. Create Repository
4. Push Code 
5. Create a pull request
6. Approve pull request
7. Merge pull request
8. Pull in new code changes.

### Check all pre-reqs are installed and ready for use
Open your git bash terminal and run your first command. `git version`

You should see something like 
```bash
git version 2.52.0
```
Our second command to ensure this tutorial is definatly going to work is `echo $SHELL`. Here we are looking for an executable that ends with the suffix bash. If you are working on a Mac terminal and you see a suffix of zsh, this is also fine. zsh is short for z-shell and has the needed capabilities for this tutorial
```bash
echo $SHELL
<put what comes up when you run the command here. It\'s something that ends in bash.exe>
```
```bash
echo $SHELL
/usr/bin/bash
```
```bash
echo $SHELL
/bin/zsh
```
If you don't see a git version, and a bash/zsh executable/binary then proceed back to Pre-req step 2, and download a git terminal. 

### Create your first repository.
There are multiple ways to create a repository. First let's start with using the user interface provided by github. 
1. Click new repository.
  1. give your repository a name
  2. Leave Settings the same
    - visibility, we leave as public so other classmates can see your repository
    - Add README as off, we can add one of these later if we choose, this is a file that is renderded as html when someone visits your github repository.
    - add .gitignore. Leave this off, we will add one later
    - add license, Leave this off, we do not need a license for this project.
  3. Save and click create new repository
2. Now we have a repository and a set of steps needed to create your new git repository.

### The create a new repository on the command line
First under quick setup, ensure https is selected. The difference between https and ssh instructions are for different ways of authentication. If you use https, you will need your username and password to authenticate. SSH requires creating a Private/Public key pair and uploading the public key to github, the use of git is the same after, but teaching about cipher keys is out of scope for this tutorial.

The commands you see will be similar to the following:
```bash
echo "# git" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/Ditmanson/git.git
git push -u origin main
```

We are missing a step here. First we have to create a directory, or folder, of where we want to place our repository. Since we are going to be using the command line for this, then let's create the repository from the command line. 

First let's navigate to our home directory with `cd $HOME`. `cd` is the change directories command. `$HOME` as a universal environmental variable on all shells that sits at your home location. Next we will create a directory where our repo will live. `mkdir <my-repo>`. The `mkdir` command creates a new folder/directory. Next you will navigate to your repository with `cd` again. `cd <my-repo>`. The commands from above were using relative location commands. If any trouble happened, then follow the following commands to use absolute location paths:
```bash
mkdir -p $HOME/<my-repo-name>
cd $HOME/<my-repo-name>
```

For more information on the above commands type:
`cd --help` `mkdir --help` `env --help`

The echo command is used for printing to standard output on your terminal. For information on `echo` not covered in this tutorial, run the command `echo --help`. Try running the `echo ""# git"` and you'll see the command echo'd on your standard output. Next you'll see the redirection command `>` This means to redirect standard output to a different location. `>>` This means we are going to amend a file if one already exists. When you run `echo " git >> README.md` If you have a README.md file already, then it will append "# git" as the last line. If you don't have a README.md then it will create the file with it as the only line. To verify, after running the echo command run `cat README.md` This will display the contents of your file to standard output. More on the `cat` command is out of context for this tutorial; however, if more information is needed you can run `cat --help`.

Our second command `git init`, scans the current directory and it's child directories and creates all the necessary files for version control and git. After running it you should see output:
```bash
Initialized empty Git repository in /home/evere5t/jade/.git/
```
This directory is hidden, if you look for it on a file explorer, you have to have view hidden files enabled to see them. For us we are going to view them from the terminal. The command we are going to use to view it is `ls`. `ls` command is a list command, this is used to view all the files/directories visible from the location of your present working directory. `ls` command isn't going to show anything other than your README.md file. To see the files created on the previous command you need to enable hidden files. To do this we pass the all files option by running command `ls -a`  Now you'll see something like:
```bash
.  ..  .git  README.md
```
. is your current repo, .. is your parent directory, **.git** is our directory we are interested in. We actually want to see all the files being created so we are going to also pass the recursive flag to have ls list all the files in this directory as well as all it's children. Your final list command is `ls -ar` What all these files do is out of scope for this tutorial. 

Our next command is `git add README.md`. This command will stage our files to be ready for saving to our repo. We will go over this command in more detail later on. As always you can git more information about it with `git add --help`

Before we commit we want to see that we have in fact staged our files. To do this run the command `git status` You should see something like:
```bash
jade master ❯ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   README.md
```

This gives us the command to unstage the file, as well as tells us we have staged a file that is not present in the repository. Now that we have staged our file we can "commit it". Committing is saving the current state of the file into the .git directory as ready to push. The `-m` flag is for message. All new commits must have a message. We use double quotes so our message can contain blank lines. SO go ahead and run `git commit -m "my first commit"`. You'll get a message saying how many files were commited with the amount of ineserts/deletions. After rerun `git status` and we'll see we no longer have any files staged.

The next command is standard practice with git. It is best practice to rename your master branch and you won't be able to continue on your master branch without making modifications in github that are out of scope for this tutorial. So we rename your master branch as main with `git branch -M main`. You should see this change on your terminal. After running it there is no output so to verify nothing went wrong let's use our echo command and we are going to use an environment variable to get the return code from the last command `echo $?` If you get `0` the the command completed without error. Any number means an error occured on your last step. 

The next command is `git remote add origin <your repo https link>` This command is going to save the location of your git repository in your .git files. This will allow you to push code changes to that location. This command has no output either, but instead of using `echo $?` we can verify the location with `git remote -v`. This command is asking git to tell you where you remote branch is. We pass the `-v` flag here for a "verbose output" which is necessary to see your remote location.

Next you are going to run `git push -u origin main` What this is saying is you want to push your commited changes to your origin on the main branch. This will bypass the need for pull requests, which we will go over later. The `-u` flag stands for upstream. This means you want to push your code upstream. For more details, as always, use command `git push -u --help` Since we are authenticating wiht https, you will need to use your username and password you created for your github account.



