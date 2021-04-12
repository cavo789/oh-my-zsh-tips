# Oh-my-zsh

![Banner](./banner.svg)

## Some advantages over bash {#some-advantages}

### General

* There are plenty of plugins and themes to enhanced the bash experience (see below)
* Spell correct: type a command like  `cd myFolder` (an existing one) but make a typo like `cd myfolder` or `cd myFoder` or anything else. Zsh will detect it and will suggest something like *Did you mean cd myFolder?*. To make this working, run `nano ~/.zshrc` and make sure to enable `ENABLE_CORRECTION` to true (uncomment the line) and write a new line like `export SPROMPT="You've typed %R, did you mean %r? [Yes, No, Abort, Edit] "` to customize the question as you want. *Run `source ~/.zshrc` to read the new configuration file if you've modified it.*
* There is a special utility called `zmv` that will allow mass actions on files or folders like renaming `.tmp` files to `.bak` f.i. `zmv -n '(*).tmp' '${1}.bak'`.
* Special search patterns like:
  * `ls *(.x)` display the list of all executable files in the current folder
  * `ls */*(.x)` display the list of all executable files in a first-level subfolder
  * `ls **/*(.x)` display the list of all executable files, whatever the deep in the structure

### Navigating

* Run `mkdir` and `cd` in only one action: `take test/any/sub/folders` will create the folder and jump in it
* You've a subfolder called `vendor`? No need to type `cd vendor`, `cd` is implicit; just type `vendor` and press <kbd>Enter</kbd> to jump inside
* Inline glob expansion: type f.i. `cat */**/settings.json` **AND PRESS <kdb>TAB</kdb>** (not <kbd>enter</kbd>!), zsh will replace the pattern with all matched filenames. The cat instruction will then be something like `cat settings.json vendor/laravel/tinker/settings.json vendor/vlucas/phpdotenv/settings.json` (and many more perhaps). Before pressing <kbd>Enter</kbd>, you can navigate in the command and suppress a few filenames f.i.
* Prompt completion: type `cd` followed by <kbd>enter</kbd> and you'll get the list of folders; you can select a name by navigating with the <kbd>tab</kbd> key
* Type `cd ven` and press <kbd>tab</kbd>, Zsh will complete the folder name
  
### History

* The *autopushd* command helps you do `popd` after you use cd to go back to your previous directory: type f.i. `cd /usr/local/bin` to go there then type `popd` and you're back in your origin folder.
* Type any command like `mkdir` followed by a space and press the <kbd>UP</kbd> or <kbd>DOWN</kbd> key to loop across the history.
* Type `cd sto` and Zsh will display a command you've already used (like `cd storage/app/public/pictures`); just press the right arrow key and hop, the command will be completed so you just need to press <kbd>enter</kbd> to run it
* Shared history: open more than one Zsh sessions, the history will be shared across all sessions
* <kbd>ALT</kbd>-<kbd>/</kbd> to output the full CLI history
* <kbd>CTRL</kbd>-<kbd>R</kbd> to show the list of commands in the history with navigation feature so we can select a previous command and press <kbd>Enter</kbd> to fire it

## Install zsh and oh-my-zsh

1. First, install zsh like this: `sudo apt install zsh`.
2. Then set zsh as your default shell: `chsh -s /usr/bin/zsh`
3. This done, install oh-my-zsh: `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

### Install plugins

> [https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins)

Note: each time a plugin has to be activated, you'll need to edit the `~/.zshrc` file and add his name to the list of plugins to load.

Edit the file and search for the `plugins=( ... )` array. Add the plugin name to the list. Save the file and the plugin will be loaded the next time you'll create a session.

#### zsh-autosuggestions

> [https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)

This plugin will predict your command based on your history (a command you've already typed in) or, for instance, you're typing `cd` and the plugin will automatically suggest the list of folders in the current directory. You're typing `cat` and you'll get this time a list of file names.

Absolutely essential.

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

#### zsh-syntax-highlighting

> [https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md)

Provide highlighting in the prompt. Practical

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

#### fzf - Command-line fuzzy finder

> [https://github.com/junegunn/fzf](https://github.com/junegunn/fzf)

Usage

* Press <kbd>CTRL</kbd>-<kbd>R</kbd> and get a prompt with your history.
* Get the full list of files under the current folder by typing `fzf` and get a list of files; press enter and the filename is selected.
* Use the `|` (pipe) to filter on a filename, interactively
* and much more, take a look to the video tutorial: [https://www.youtube.com/watch?v=qgG5Jhi_Els](https://www.youtube.com/watch?v=qgG5Jhi_Els)

```bash
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf ; ~/.fzf/install
```

## Install the powerlevel10k theme

> [https://github.com/romkatv/powerlevel10k](https://github.com/romkatv/powerlevel10k)

Installation is made of four steps.

### Get the powerlevel10k theme

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

### Set powerlevel10k as default theme

This done, edit the `~/.zshrc` file and update the `ZSH_THEME` like this:

```ini
ZSH_THEME="powerlevel10k/powerlevel10k"
```

### Install powerlevel10k fonts

Donwload the four fonts from [https://github.com/romkatv/powerlevel10k#manual-font-installation](https://github.com/romkatv/powerlevel10k#manual-font-installation): download one by one and click on the download file. Windows will open it and you'll get a windows with an `Install` button.

This done, open the Windows Terminal settings and open the `settings.json` file. Add the `MesloLGS NF` font in the `defaults` section for `profiles`, like this:

```json
{
  "profiles": {
    "defaults": {
      "fontFace": "MesloLGS NF"
    }
  }
}
```

### Configure powerlevel10k

Once the `~/.zshrc` file has been updated and fonts installed, just create a new Linux session. The `powerlevel10k` configuration script will be started and if everything is going fine, you'll see the correct symbol (if not, fonts were incorrectly installed).

Follow the wizard and make your choice in the different options.

If you want to display the username in the prompt, follow this [guide](https://gitee.com/kongren/powerlevel10k#how-do-i-add-username-andor-hostname-to-prompt).
