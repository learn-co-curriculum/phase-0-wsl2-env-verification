# Verify and Troubleshoot your WSL2 Environment Setup

## Action Item

1. Open your "Ubuntu" application
2. Type `curl -so- https://raw.githubusercontent.com/learn-co-curriculum/flatiron-manual-setup-validator/master/wsl-phase-0-manual-setup-validator.sh | bash 2> /dev/null`

## Check Your Work

If all checks pass, you have completed your environment setup and are ready to
move on!

It may be that you are setup correctly, but the validator script can't tell.
If there is some sort of error, revisit the instructions for the item that is
not passing. If you can run the commands listed in the **Check Your Work**
section of that item, you should be all set and can disregard the validator.

### Fixing NVM and RVM Issues for WSL2

If you are having trouble getting RVM, Ruby, NVM, or Node to work, you may
have an issue with your `.bashrc` file. To fix, we need to run two commands.

The first command makes a backup of your current `.bashrc` file:

```sh
mv ~/.bashrc{,.bak}
```

The second command replaces the contents of your `.bashrc` file with a default file:

```sh
curl -sSL https://raw.githubusercontent.com/flatiron-school/dotfiles/master/minimal-bashrc > ~/.bashrc
```

Close and reopen your terminal. With a new `.bashrc` file, we can now test out each tool.

#### Verify RVM is Installed

To confirm that RVM is working, run:

```sh
rvm
```

If you see a long message ending in `“For additional documentation please visit https://rvm.io”`, RVM is installed. 

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

```sh
rvm list
```

If you see `=* ruby-2.7.2`, Ruby is installed and 2.7.2 set as the default version and you are all set for Ruby.

> If you do not see `ruby-2.7.2` at all, install it with the following command:
> 
> ```sh
> rvm install ruby-2.7.2
> ```

> If `ruby-2.7.2` is listed, but is not preceded by `=*`, make it the default version by running:
> 
> ```sh
> rvm use 2.7.2 --default
> ```

#### Verify NVM is installed

To confirm NVM is installed, run:

```sh
nvm
```

If you see a message ending with `“Note: to remove, delete, or uninstall nvm…”`, NVM is installed. 

> If the `nvm` command is not recognized, install NVM with the following command:
> 
> ```sh
> curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.36.0/install.sh | bash
> ```
>
> Close and reopen the "Terminal" application, then run `nvm` again.

#### Verify Node is Installed

To confirm Node is installed, run:

```sh
nvm list
```

If you see a message starting with “-> v14.13.0” (or any number higher than this), a version of Node is installed that will work for this course. 

> If you don't see this number, install a new version of Node:
> 
> ```
> nvm install node
> ```

### Enabling Virtualization In the BIOS

For most Windows machines, enabling WSL and the Virtual Machine Platform should be enough to
get Ubuntu running. Some devices, however, require an additional step - enabling hardware
virtualization in the BIOS.

> **WARNING:** Fiddling with your BIOS settings can **trash your PC**! Be careful when making
> changes. Consult your manufacturer’s help pages or search for online advice about your
> specific make and model.

Accessing your BIOS is typically done by rebooting your computer and hitting a specific key,
usually `DEL`, `F2`, or `F10`, as the system starts. In the BIOS, look for **Virtualization
Technology, VTx** or something similar.

<!-- ## Troubleshooting

Below are some options to try for specific issues.

### RVM Is Producing Errors or Warnings

1. Close your terminal, reopen it, and try the `rvm list` command.

2. If you see a warning regarding the `PATH`, try running the following
   first:

   ```sh
   rvm use 2.7.2
   rvm --default use 2.7.2
   ```

   Close and reopen the terminal again, and rerun `rvm list`.

3. If RVM is not found when you run `rvm list`, try reinstalling RVM:

    ```sh
    curl -sSL https://get.rvm.io | bash -s stable --ruby --auto-dotfiles
    ```

    You may get an error regarding keys with further
    commands to try, including the following:

    ```sh
    gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

    or if it fails:

    command curl -sSL https://rvm.io/mpapis.asc | gpg --import -
    command curl -sSL https://rvm.io/pkuczynski.asc | gpg --import -
    ```

   Try each of these, followed by the previous `curl` command to install RVM.

4. If RVM is found but continues to produce errors, try uninstalling with:

   ```sh
   rvm implode
   ```

   This command will remove RVM entirely. Follow the instructions in Step 3 to reinstall RVM.

### `learn whoami` Command Not Found / `learn` Produces `oj.bundle` Error

1. Close your terminal window, reopen it, and try the `learn whoami` command
   again.

2. Run the command `rvm list`. If RVM is not found, follow the steps in the
   previous troubleshooting section on installing RVM. If you see a warning
   regarding `PATH`, try running the following first:

   ```sh
   rvm use 2.7.2
   rvm --default use 2.7.2
   ```

   Then reinstall the Learn gem and test it again with:

   ```sh
   gem install learn-co
   learn whoami
   ```

3. If the `learn` command continues to fail, but RVM is working fine, try
   reinstalling RVM by first using the following command:

   ```sh
   rvm implode
   ```

   Then rerunning the RVM install script:

   ```sh
   curl -sSL https://get.rvm.io | bash -s stable --ruby --auto-dotfiles
   ```

   Once RVM is installed, try reinstalling and testing the `learn-co` gem.

4. If you are still unable to run `learn whoami`, try the following:

   ```sh
   bundle clean --force
   gem install learn-co
   gem install bundler
   ```

   The `bundle clean --force` command will clear out any gems that have already been installed. At the moment,
   you will only need the `learn-co` and `bundler` gems, so this reinstalls
   them.

### `learn` Commands Produce `psych` Gem Errors

This error is typically due to issues in the `~/.learn-config` file. 

1.  Run `code ~/.learn-config`. This file should only have three lines in it, 
    similar to the example below:

    ```sh
    ---
    :learn_directory: "/Users/< username >/Flatiron/code"
    :editor: code
    ```

2.  Check for any typos or extra content. Make sure the `:learn_directory` path
    is valid and has your computer's username after `/Users/`. You can confirm this
    name by running `echo $HOME`. 

3.  Save the `.learn-config` file and try running `learn whoami`.  -->

##
