# Setting up a new Mac

### Quick start for developers

Homebrew is essential. Other than Google Chrome, it's probably the first app a developer should install on a new Mac. 

You can read about Homebrew at https://brew.sh or  install it with one line:

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

On a Mac, the pre-installed command line tools (such as git, vim, curl, tar, gzip, openssl, php, nslookup, etc) are found in `/usr/bin/`. Homebrew installs additional packages (and their dependencies) in `/usr/local/bin/` where they are sandboxed away from the operating system. 

In general, your Mac includes recent, stable versions of *NIX tools that "just work," so you can use them out of the box. 

Try it:

```
which git
git --version
which php
php --version
```

One popular command line tool, wget, is **not** included on new Macs. Homebrew makes it easy to add wget and countless other *NIX and Gnu tools to your system. To install wget, for example, run `brew install wget`. 

If the version of git included with MacOS is not fancy enough for you, `brew install git` will fetch a newer version. If you change your mind, just `brew remove git` to remove the Homebrew-managed package (the core operating system software will **not** be altered, so the Apple version of git that came with your computer will "just work" again if you uninstall Homebrew.) Developers love Homebrew, because it keeps their system clean and avoids cumbersome $PATH editing when you want to add functionality.

Suppose you need to encrypt or decrypt files with GPG, you could run `brew install gpg`. The versions of sed, awk, zcat etc that ship with the Mac workly slightly differently than what you would find on Ubuntu. If this ever becomes a problem for you, Homebrew can bridge the gap, because you can install [the exact Linux versions](https://serverfault.com/a/597775) of Gnu tools by running `brew install coreutils gnu-sed`. Whatever you need, Homebrew [and Google](http://lmgtfy.com/?q=install+composer+with+homebrew) should have you covered.

`brew list` shows you what packages you have installed. If you want to uninstall every package you've ever installed with Homebrew, [you can do that](https://darryldias.me/12/remove-all-installed-homebrew-packages). 

Now that you know what Homebrew is and what it does, install Drupal tools. You will definitely want Drush and Composer available globally on your system. Run these commands in sequence:

```
brew tap homebrew/dupes
brew tap homebrew/php
brew install php71
brew install mcrypt php71-mcrypt
```

Then run:

```
which php
php --version
```

Next, install Composer:

```
brew install composer
```

Finally, install Drush:

```
brew install drush
drush --version
```

## You can install binaries, too

Most likely, you'll want your familiar Google Chrome browser (perhaps Firefox too) and Vagrant, and VirtualBox. You'll also need a good text editor like Sublime Text or BBEdit. Other editors are [listed on D.O.](https://www.drupal.org/docs/develop/development-tools/development-tools-overview). You can get apps the old-fashioned way (by downloading them from websites) or you can install the latest versions with Homebrew with these commands:

```
brew cask install google-chrome
brew cask install firefox
brew cask install virtualbox
brew cask install vagrant
brew cask install sublime-text
brew cask install bbedit
```
Maybe that was unnecessary, but it's nifty and fast!

## Get your Acquia aliases

Drush aliases make it easy to SSH into your Acquia servers, for example `drush @server.env ssh`.

First generate an SSH key that you can use with Acquia, GitHub, and other services:

```
ssh-keygen -t rsa -C "your.name@acquia.com" -b 4096
cd ~/.ssh
cat id_rsa.pub
```

Log on to [Acquia Cloud](https://cloud.acquia.com) and navigate to your user profile. Edit your profile, then go to your Credentials page to add your public key.

In addition to adding your SSH key to your Acquia profile, you can [download Drush aliases](https://accounts.acquia.com/account/964206/security/drush_aliases/download?site=cloud) that reflect your organization's Teams and permissions. Once you've downloaded your custom file, install your Acquia aliases with this:

```
tar -C $HOME -xf $HOME/Downloads/acquiacloud.tar
```

To see what sites you can access, run `drush site-alias` (or simply `drush sa`). If your organization administrator has changed your access rights, run `drush acquia-update` to refresh your drush aliases.

## Create a folder for your codebases

I like to create a folder where I'll keep sites and codebases:

```
cd $HOME
mkdir Sites
```

If you want to install Drupal VM, you can do that now, with Vagrant. (Please note that while the install process is automated, it takes a long time... 20-25 mins or so depending on your network connection speed.) 

When this process is complete, you'll have the latest version of Drush running locally, in an Ubuntu VM, on your Mac. If you haven't used Drupal VM before, this is a great introduction to Drupal VM.

The Drupal VM maintainer recommends Ansible, so install that first:

```
brew install ansible
```

Navigate to the directory where you'll keep this demo VM:
 
```
cd ~/Sites
git clone https://github.com/geerlingguy/drupal-vm.git
cd drupal-vm
vagrant up
vagrant up
```

When this is all complete you'll have a Drupal VM dashboard, open Chrome and go to http://dashboard.drupalvm.test

_Read more on the [Drupal VM](https://www.drupalvm.com) site._

## Command line protips

- Drag the **title bar** of an open Finder window over the Terminal icon in your Dock. (This takes you directly to that directory on the command line.)
- If you're already on the command line but want to use the Finder, `open .` will open new Finder window showing the contents of the current directory.
- You can show invisible files (like .htaccess) [in the Finder](https://ianlunn.co.uk/articles/quickly-showhide-hidden-files-mac-os-x-mavericks).
- Most popular apps can be invoked from the command line. Check the documentation for each app. In BBEdit, there is an option to "Install Command Line Tools" which allows you to run `bbedit settings.php` from a Terminal prompt.

Mac developer setup guides are dime-a-dozen on the web, but you've just read the best one. Here's [another useful resource](http://sourabhbajaj.com/mac-setup) that I found. Google has [more](https://www.google.com/search?client=safari&rls=en&q=developer+new+mac+setup+github.io&ie=UTF-8&oe=UTF-8).

## Finder protips

See my [Finder protips](Finder_protips.md).