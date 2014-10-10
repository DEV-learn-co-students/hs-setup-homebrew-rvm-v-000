---
tags: kids, setup, rvm, homebrew
type: environment setup
language: bash
---

## Environment Set Up - Part 3

###1. Installing RVM
RVM stands for Ruby Version Manager. Ruby, just like software, has newer and older versions. RVM allows you to have multiple versions of ruby installed on your computer that you can easily switch back and forth between. 

```
\curl -L https://get.rvm.io | bash -s stable --ruby=2.1.3
```

This command will install the latest version as ruby, as well as the newest stable version, which here is 2.1.3.

Now, we want to make 2.1.3 our default version. Enter `rvm use 2.1.3 --default`. If you open a new tab and then type `ruby -v`, you should see 2.1.3

If you get any errors installing RVM that are related to XCode or GCC, it means you'll need to uninstall XCode and start this guide all over from step 2.

If you have issues with Homebrew, You can try reinstalling it with this command:
```
\curl -L https://gist.github.com/mxcl/1173223/raw/a833ba44e7be8428d877e58640720ff43c59dbad/uninstall_homebrew.sh | bash
```

###2. RVM and Sublime Together
To get RVM and Sublime to play nice, we need to do the following:
```
open "$HOME/Library/Application Support/Sublime Text 2/Packages/Ruby/Ruby.sublime-build"
```
Once the file is open, you'll need to paste the below into the file:
```
{
  "env":{
      "PATH":"${HOME}/.rvm/bin:${PATH}"
  },
  "cmd": ["rvm-auto-ruby", "$file"],
  "file_regex": "^(...*?):([0-9]*):?([0-9]*)",
  "selector": "source.ruby"
} 
```

###2. Update your Bash Profile
Make sure you are in your root directory by typing `cd ~` in your terminal. From here you should be able to open up your bash profile with this command `subl .bash_profile`.

Scroll down to the very bottom of your bash profile and copy and paste this code after everything else that is already in there:

```
# Final Configurations and Plugins
# =====================
  # Git Bash Completion
  # Will activate bash git completion if installed
  # via homebrew
  if [ -f `brew --prefix`/etc/bash_completion ]; then
    . `brew --prefix`/etc/bash_completion
  fi

  # RVM
  # Mandatory loading of RVM into the shell
  # This must be the last line of your bash_profile always
  [[ -s "/Users/$USER/.rvm/scripts/rvm" ]] && source "/Users/$USER/.rvm/scripts/rvm"  # This loads RVM into a shell session.
```
