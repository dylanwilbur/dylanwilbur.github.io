---
layout: post
title: Setting Up A New Macbook
---

# My Essentials For A New Laptop
![](/assets/images/showcase.gif)
__What you're seeing here__:
- Music window(vaporwave artist called 2814 check it out) is "floating": not affected by tiling window manager
- Enter a command `tw` with Alfred to create a new window of iTerm2
- Enter a command `ns` with Alfred to create a new window of Safari
- Open up my vim configuration
- Use Contexts with Command+Tab to switch to the music window
- "Unfloat" the window
- Use a key command to temporarily fullscreen the safari window

I'm going to organize this list in "tier list" format. Stuff I use every day and I think is absolutely essential will be near the top, while more niche things will gather near the bottom.

I'll likely be continuously updating these posts as I use the laptop more and more. I've just been adding stuff as I go along to try and mimic my old laptop, but hopefully cut down on some of the bloat that I don't need.

## Tier One: Absolute Essentials

### iTerm2
##### Used For: Everything
![image-left]({{ site.url }}{{ site.baseurl }}/assets/images/iterm.png){: .align-left} First thing to do on a new mac: install iTerm2. Way better than the default terminal, and I use a terminal for almost everything so this suits my needs perfectly.

__Theming__: I use the [OneDark](https://github.com/nathanbuchar/atom-one-dark-terminal) theme for iterm, but you can find many more [here](https://iterm2colorschemes.com)

__Dropdown Terminal__: In iTerm preferences, create a new profile called Dropdown. Then go to the keys section and select "A hotkey opens....". I have my hotkey as `CMD+CTRL Space` which is super fast to hit because I remapped my Caps Lock key.

### Homebrew
##### Used For: Installing everything
Second thing to do on a new mac: install homebrew. Just paste this into iTerm:
```bash
xcode-select --install
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
If you ever need to install an application, odds are you can do it from the command line with homebrew which is my preferred method. For instance, to install Firefox:
`brew cask install firefox`
The `cask` part is typically used for stuff that isn't a CLI. For CLI stuff, you would just use brew install, like for installing python 3:
`brew install python3`

### Oh My Zsh
Allows me to trick out my terminal window. The github is [here](https://github.com/ohmyzsh/ohmyzsh) and it'll give more info but you can install it by running this on the terminal:
`sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

I personally use the [ Spaceship prompt ](https://github.com/pascaldevink/spaceship-zsh-theme)

### Alfred
##### Used For: Launching Apps and scriptable commands
You can download it with homebrew:
`brew cask install Alfred`

Costs like 15 bucks but it's worth it

### Yabai
##### Used For: Tiling Window Manager
This is highly keyboard based and requires some configuration. If you want a different window manager look up Magnets.
`brew cask install yabai`
Check out my dotfiles for this and skhd [here](https://github.com/dylanwilbur/my-dotfiles).

### Karabiner Elements
##### Used For: Remapping Caps Lock to be more useful

![image-left]({{ site.url }}{{ site.baseurl }}/assets/images/karabiner.png){: .align-left} One of those apps I just completely couldn't live without, and it doesn't even do very much for me. There's a ton of stuff you can do with this, but I only use two complex modifications:
- Change caps_lock to control if pressed with other keys, escape if pressed alone
- Change right_command+hjkl to arrow keys

The first one I use almost every five minutes, and it's one of those things where I feel lost if I don't have it. It's especially useful for vim since the escape key and control keys are used all the time but are in really unnatural spots

**Note**: This one didn't work with a brew cask install because there were some preferences in system preferences that weren't showing up. So it's easier to just download straight off the website.

### Contexts
##### Used For: Command+Tab App switching, Windows style
##### Price: $10

One thing windows does right is their alt+tab app switcher. On MacOS, by default you can only switch between different apps, not specific windows. So if you have, say, 2 iTerm windows open, you're out of luck if you want to command tab to one of them in particular. It was writing this that made me go and redownload this app because the default was so annoying.

Dark Mode, of course.

## CLI's

#### Vim(Neovim)

##### Writing with Vim

Writing with vim is cool, especially spell check.
![](/assets/images/vimwriting.gif)

Note:
- the tiling window manager
- the awesome writing vim theme
- using Ctrl-F while typing to immediately correct the last spell check
- using the alfred command `ns` to create a new safari tab


Check out my dotfiles [here](https://github.com/dylanwilbur/my-dotfiles).


#### Ruby Related Stuff
I used [this](https://jekyllrb.com/docs/installation/macos/) guide on Jekyll's website. You end up with rbenv and ruby installed.
You might need to run
`export GEM_HOME="$HOME/.gem"`
to get some of the commands working with the gems. I added this to my `.zshrc` to make it permanent.




#### Vim Browser Plugin
Hard to stop that keyboard-based stint once you hop on that vim train. Obviously one would think to port vim functionality over to the browser, and it actually tends to work quite well. I've tried qutebrowser, not worth it for me but worth a try. I use safari so unfortunately my beloved [sVim](https://github.com/flippidippi/sVim) broke with the introduction of Mojave. If you use Chrome or Firefox I would recommend using one of their vim extensions, really speeds things up.
