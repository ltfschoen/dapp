# README

---
dApp
---

# Table of Contents
  * [Chapter 0 - Setup Dependencies](#chapter-0)

## Chapter 0 - Setup Dependencies <a id="chapter-0"></a>

* Homebrew
  ```
  brew doctor
  brew update
  ```

* Configure globally ignored files
  ```
  git config --global core.excludesfile ~/.gitignore
  printf "vendor/bundle\n.DS_Store\n" >> ~/.gitignore
  ```

* Configure default path for `bundle`
  ```
  mkdir -p ~/.bundle
  printf -- "---\nBUNDLE_PATH: vendor/bundle" >> ~/.bundle/config
  ```

* Setup RVM and configure to instantiate with shell sessions.
  * https://rvm.io/rvm/install
  * https://rvm.io/rvm/security
    * Add trusted GPG keys
        ```
        # add trusted rvm gpg keys
        echo 409B6B1796C275462A1703113804BB82D39DC0E3:6: | gpg --import-ownertrust # mpapis@gmail.com
        echo 7D2BAF1CF37B13E2069D6956105BD0E739499BDB:6: | gpg --import-ownertrust # piotr.kuczynski@gmail.com
        ```
    * Install. Note: Replace .zshrc with .bash_profile if using that instead.
        ```
        \curl -sSL https://get.rvm.io | bash -s stable
        echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"' >> ~/.zshrc
        source ~/.zshrc
        # don't do this `rvm install ruby-3.3.1` due to error `Error running '__rvm_make -j12'`
        # instead do this:
        rvm reinstall 3.3.1 --with-openssl-dir=`brew --prefix openssl@1.1` --with-opt-dir=`brew --prefix openssl@1.1`
        # use as default for new shells
        rvm use ruby-3.3.1 --default
        ruby -v
        which ruby
        gem pristine --all
        bundle show rails
        rvm gemset create dapp
        ```

    * Set up RVM workflow with Gemsets to create a .ruby-version file and a .ruby-gemset file for the project so RVM will detect the ruby version and gem set automatically
        ```
        rvm --ruby-version use 3.3.1@dapp
        ```

    * Setup .rvmrc
        ```
        echo "rvm --create use ruby-3.3.1; rvm reload;" > .rvmrc
        ```

    * Check Ruby version and location installed
        ```
        ruby -v; which ruby
        ```

* Configure IRB Autocompletion
    ```
    touch ~/.irbrc
    printf "require 'irb/completion'" >> ~/.irbrc
    ```

* Install Ruby on Rails latest stable version from https://github.com/rails/rails/releases
  ```
  gem install rails -v 7.1.3.3
  rails -v
  ```

* Configure Git
  ```
  git config --global color.ui true
  git config --global user.name "YOUR NAME"
  git config --global user.email "YOUR@EMAIL.com"
  ssh-keygen -t ed25519 -C "YOUR@EMAIL.com"
  ```

  * Add newly generated SSH key to your Github account. Copy and paste the output of the following command and paste it https://github.com/settings/ssh.
    ```
    cat ~/.ssh/id_ed25519.pub
    ```
  * Check it worked
    ```
    ssh -T git@github.com
    ```

* Install VS Code and then Cmd+Shift+P and select "Install 'code' command in PATH" to add the code command to your shell so you can open up VS Code from your terminal.

* Configure editor to allow configuring Rails credentials in VS Code
  ```
  echo 'export EDITOR="code --wait"' >> ~/.zshrc
  exec $SHELL
  ```
