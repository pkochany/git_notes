Creating new repository from scratch:

1. create new repo on github

2. ```
   $ git remote add origin git@github.com:username/new_repo
   $ git push -u origin master
   ```

------

If you’ve never used git or github before, there are a bunch of things that you need to do.  It’s [very well explained on github](https://help.github.com/articles/set-up-git), but repeated here for completeness.

- Get a [github](https://github.com) account.

- Download and install [git](https://git-scm.com/downloads).

- Set up git with your user name and email.

  - Open a terminal/shell and type:

    ```
    git config --global user.name "Your name here"
    git config --global user.email "your_email@example.com"
    ```

    (Don’t type the `$`; that just indicates that you’re doing this at the command line.)

    I also do:

    ```
    git config --global color.ui true
    git config --global core.editor emacs
    ```

    The first of these will enable colored output in the terminal; the second tells git that you want to use emacs.

- Set up ssh on your computer.  I like [Roger Peng](http://www.biostat.jhsph.edu/~rpeng)’s [guide to setting up password-less logins](http://www.biostat.jhsph.edu/bit/nopassword.html). Also see [github’s guide to generating SSH keys](https://help.github.com/articles/generating-ssh-keys).

  - Look to see if you have files `~/.ssh/id_rsa` and `~/.ssh/id_rsa.pub`.

  - If not, create such public/private keys: Open a terminal/shell and type:

    ```
    ssh-keygen -t rsa -C "your_email@example.com"
    ```

  - Copy your public key (the contents of the newly-created `id_rsa.pub` file) into your clipboard.  **On a Mac**, in the terminal/shell, type:

    ```
    pbcopy < ~/.ssh/id_rsa.pub
    ```

- Paste your ssh public key into your github account settings.

  - Go to your github [Account Settings](https://github.com/settings/profile)

  - Click “[SSH Keys](https://github.com/settings/ssh)” on the left.

  - Click “Add SSH Key” on the right.

  - Add a label (like “My laptop”) and paste the public key into the big text box.

  - In a terminal/shell, type the following to test it:

    ```
    ssh -T git@github.com
    ```

  - If it says something like the following, it worked:

    ```
    Hi username! You've successfully authenticated, but Github does
    not provide shell access.
    ```

- Now make sure git is using correct key for ssh connection to github.

  - In terminal:

    ```
    nvim ~/.shh/config
    ```

  - Paste something like this:

    ```
    Host your.hostname.com
        Hostname github.com
        User git
        IdentityFile ~/.ssh/special_id_rsa
    ```

  - For already existing repositories however, you will additionally need to modify the Git config file `.git/config` inside the project. The url of remote “origin” must be changed to the host defined in `~/.ssh/config`.

    ```
    nvim .git/config
    [remote "origin"]
        url = git@your.hostname.com:username/reponame.git
    ```

------

Git proxy settings:

```
vim ~/.gitconfig
```

```
[http "https://188.252.28.69"]
    proxy = http://username@server:same_port

[http]
    proxy = http://proxy.server:same_port
```

