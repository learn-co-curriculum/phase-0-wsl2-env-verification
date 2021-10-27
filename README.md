# Verify and Troubleshoot your WSL2 Environment Setup

## Action Item

1. Open your "Ubuntu" application
2. Type the following:

```console
$ curl -so- https://raw.githubusercontent.com/learn-co-curriculum/flatiron-manual-setup-validator/master/wsl-phase-0-manual-setup-validator.sh | bash 2> /dev/null
```

## Check Your Work

<iframe width="560" height="315" src="https://www.youtube.com/embed/LOAbYZmRc9I" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

If all checks pass, you have completed your environment setup and are ready to
move on!

It may be that you are set up correctly, but the validator script can't tell. If
there is some sort of error, revisit the instructions for the item that is not
passing. If you can run the commands listed in the **Check Your Work** section
of that item, you should be all set and can disregard the validator.

### Fixing NVM and RVM Issues for WSL2

If you are having trouble getting RVM, Ruby, NVM, or Node to work, you may have
an issue with your `.bashrc` file. To fix, we need to run two commands.

The first command makes a backup of your current `.bashrc` file:

```console
$ mv ~/.bashrc{,.bak}
```

The second command replaces the contents of your `.bashrc` file with a default
file:

```console
$ curl -sSL https://raw.githubusercontent.com/flatiron-school/dotfiles/master/minimal-bashrc > ~/.bashrc
```

Close and reopen your terminal. With a new `.bashrc` file, we can now test out
each tool.

#### Verify RVM is Installed

To confirm that RVM is working, run:

```console
$ rvm
```

If you see a long message ending in
`"For additional documentation please visit https://rvm.io"`, RVM is installed.

> If the command `rvm` is not recognized, do the following in your terminal:
>
> 1. Type `sudo apt-get install software-properties-common` and press `<Enter>`
> 2. Type `sudo -E apt-add-repository -y ppa:rael-gc/rvm` and press `<Enter>`
> 3. Type `sudo apt-get update` and press `<Enter>`
> 4. Type `sudo apt-get install rvm` and press `<Enter>`
> 5. Type `source /etc/profile.d/rvm.sh` and press `<Enter>`
> 6. Close the "Ubuntu" application
> 7. Reopen the "Ubuntu" application
> 8. Type `rvm` and press <Enter>

#### Verify Ruby is Installed

To confirm Ruby is installed, run:

```console
$ rvm list
```

If you see `=* ruby-2.7.4`, Ruby is installed and 2.7.4 set as the default
version and you are all set for Ruby.

> If you do not see `ruby-2.7.4` at all, install it with the following command:
>
> ```console
> $ rvm install ruby-2.7.4 --default
> ```
>
> If `ruby-2.7.4` is listed, but is not preceded by `=*`, make it the default
> version by running:
>
> ```console
> $ rvm use 2.7.4 --default
> ```

#### Verify NVM is installed

To confirm NVM is installed, run:

```console
$ nvm
```

If you see a message ending with `"Note: to remove, delete, or uninstall nvm…"`,
NVM is installed.

> If the `nvm` command is not recognized, install NVM with the following command:
>
> ```console
> $ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
> ```
>
> Close and reopen the "Terminal" application, then run `nvm` again.

#### Verify Node is Installed

To confirm Node is installed, run:

```console
$ nvm list
```

If you see a message starting with "-> v14.13.0" (or any number higher than
this), a version of Node is installed that will work for this course.

> If you don't see this number, install a new version of Node:
>
> ```console
> $ nvm install node
> ```

### Enabling Virtualization In the BIOS

For most Windows machines, enabling WSL and the Virtual Machine Platform should
be enough to get Ubuntu running. Some devices, however, require an additional
step - enabling hardware virtualization in the BIOS.

> **WARNING:** Fiddling with your BIOS settings can **trash your PC**! Be
> careful when making changes. Consult your manufacturer’s help pages or search
> for online advice about your specific make and model.

Accessing your BIOS is typically done by rebooting your computer and hitting a
specific key, usually `DEL`, `F2`, or `F10`, as the system starts. In the BIOS,
look for **Virtualization Technology, VTx** or something similar.
