---
layout: post
title: Setting Up A New Macbook- Updated 2025
---
![](/assets/images/terminal.png)

## Motivation
I have been writing code with MacOS in one form or another for almost 15 years at this point. I've tried almost every 'productivity' tool or setup out there over that time, and I've dialed in what I use during my day-to-day workflow to a point I'm quite happy with. Time spent learning and implementing tools to minimize friction across workflows is generally well spent- if you are even 10% more efficient at something, that compounds drastically over time, especially if you are doing that thing 100x per day. Every tool, decision, workflow here is a means to that end.

Hope anyone reading this can pick up at least one new thing that'll reduce that friction for you too. I'm going to generally go over this in order from most to least impactful on my daily work.

### TLDR:
- I highly recommend learning vim if you write code.
    - play this game for a bit: [vim adventures](https://vim-adventures.com)
    - install the [vim](#vim) plugin in the editor of your choice
- Use a [clipboard history manager](#clipboard-history-manager) like the one in [alfred](https://www.alfredapp.com/help/features/clipboard/)
- I highly recommend [alfred](#alfred) in general.



### Why MacOS?
Not much to say here- I've tried linux and windows separately, and I'll always prefer Mac for a few reasons:
- **Unix shell**: Incredibly nice to have a shell environment in unix. Most thing I need to do will involve the shell in some way, and in my opinion having a unix shell allows me to do much of the same things I would do on a linux. That compatibility helps any time you need to hop on linux for any reason
- **Sensible defaults**: Most things just work. While something like ubuntu might offer more customization, for me personally, I find that the abundance of customization options just adds too much decision fatigue. I'll take the reduction of overhead over greater customization, at least for now.

## Vim
I have been using vim motions to edit text since 2016, and have used neovim as my main editor on and off since then. I've been asked on a few occasions to 'sell' people on vim. My typicall response is just to blindly trust me, start using it, and you will see for yourself how indespensible it will become after that initial learning curve.  First off, I can't overstate enough how impactful vim for everything I write. If I could only keep one thing on this list, it would be vim without any question. I would go as far as to say that any person writing code for a living needs to pick this up, you will take it with you the rest of your life. Here's a few quick reasons.

**Editing speed**:
Not having to take your fingers off the keyboard for doing most things ends up saving a ton of time. Most of the time, writing text or code isn't just about how fast you can type, it's about changing things, duplicating things, navigation, and much more. This is where vim motions in particular let you reach a flow state where you can minimize the time from thought -> action to about as low as it can go.

Here's a quick example of some really common patterns that just make sense in vim. Say you have some object, and you want to make another one and change some parameters. So, you have something like this:
```python
async def main():
    es_search = WorkOrderSearch(environment="test")
    es_search.connect()
    semantic_evaluator = SemanticEvaluator(es_search, "0.7 threshold semantic search")
```
and you want to add this line:
```python
mpnet_evaluator = SemanticEvaluator(es_search, "all-mpnet-base-v2 evaluator")
```
To do this in vim, I would do these keystrokes:

**`jjj..`** -> navigate to the line with my semantic evaluator

**`yyp`** -> copy the current line, paste it directly under the current line

**`ct_`** -> change the currently selected word up until the _, enter insert mode, write mpnet

**`A (esc) bb ci"`** -> move to end of the line, move back two words, change the inside of the parentheses and enter insert mode

This entire process takes a few seconds and requires no additional thought, it's just muscle memory.

**CLI editing**:
You can hop into any remote server at any time and be fully competent. Vim or vi(the CLI), is installed by default nearly everywhere.

**Fun**:
It's fun to use. It's fun to find new, creative ways of doing things. I'd relate it to climbing a bit in this way- you can pick up new movement patterns over time, think initially about how to solve certain common problems, but they quickly become muscle memory and you never have to think about that again. There's also no skill ceiling.

### Vim motions
Important to distinguish vim from vim motions. Vim refers to the cli editor, while the vim motions refers to the navigation language used to move around and edit text. Vim motions have native support on almost every editor out there, like VSCode, Cursor, Jetbrains, even leetcode.com. Even some notes apps like [obsidian](#obsidian) have native vim motions support. Vim motions can be taken with you wherever you go.

### Vi, Vim and Neovim
`vi` is the original editor which is installed by default on most linux and mac machines. `vim` is also usually installed by default, but it came later("vi iMproved"). It's incredibly useful to be competent in the cli editor for a variety of reasons:
- I've had to use `vi` on several occasions on certain remote machines that I need to make quick edits on
- Sometimes you have to work on remote servers, and you need to edit files. Super easy to do so with stock `vim`, even without customizations.
- **Quick edits**: If I need to just change one quick thing in a file, maybe a config file like `~/.zshrc`, I don't want to boot up vscode or cursor to make that edit. Way easier just to use iTerm and quickly make that edit.

#### Neovim
![](/assets/images/lazyvim.png)

I went through an extended period ~5 years ago where I spent a ton of time customizing a `.vimrc` to do exactly what I wanted. It was a lot of fun and all, but I found that the customization ended up getting in the way of actually getting things done. So a new change is that I just install [stock lazyvim](https://www.lazyvim.org), which is a neovim distribution. Again, this seemed to have the best sensible defaults of any vim setups I found, and I love that I don't really have to touch `.vimrc` to get it functional.

Also, I have `alias vim='nvim'` in my `~/.zshrc` to always boot lazyvim if I need to edit something.

#### Some customization
- I map `C-u` and `C-d` to be `C-u zz` and `C-d zz` to center the page upon scroll

### Why I don't main Nvim
Very similar reason as to why I go with MacOS over linux- I have learned to seriously value sensible defaults over customization. For me personally, when I am given the option of endless customization, I will often end up endlessly customizing(at the expense of getting work done). Maybe this will change in the future, but for now I stick to [cursor](#cursor) (previously vscode)


## Cursor
![](/assets/images/cursor.png)

Obviously AI code editors are generally in their infancy, but for now I've found Cursor to be pretty great for my daily needs. Since it's just a VSCode fork, I genuinely don't really see a reason to use VSCode anymore(please enlighten me if there is). There's a lot more to it than just something that can get claude to write code for you. Here's why:

**CMD+K**:
One of the best features of Cursor in my opinion is CMD+K. I love to be able to highlight a small piece of text while I'm editing or writing something, and either:
- ask a quick question about it(`option+enter`)
- ask for a quick fix

In particular, this is great if I don't know the syntax for something, and I don't want to go to google or wait for a lengthy chat response from claude. Or, if I just have a question about how a block of code works or should behave.

**CMD+L: Chat interface**:
As we all know, LLMs are only as good as the context you give it, and something like Cursor is the best way to 'be your own RAG', in a sense. Tagging specific files, sections of code, or directories is super easy. This is probably the most useful way to interact with LLMs in a coding context in my opinion.

**Tab Complete**:
Really, really great at just anticipating certain things that you are about to do. Obviously it can get this wrong a lot of the time, but when it's right it saves a ton of time. Because of this I have `cmd+ctrl+t` and `cmd+ctrl+y` as my keybinds to toggle cursor command tab, so I can turn it off if it's getting in the way.

**Agent Mode**:
I use this super sparingly because it can often get things wrong, especially on complex code bases. However, where I think this shines is in simple tasks, writing boilerplate, or spinning up demos. In particular, this can help go from 0 to demo very fast- that being said, I wouldn't rely on it to choose the tech stack and set that up.


#### Cursor settings:
Vim extension, obviously.

Map visual line navigation. `j` and `k` will move up and down by visual lines, instead of real lines. More intuitive vertical nav with vim motions.
`keybindings.json`:
```json
    {
        "key": "k",
        "command": "cursorUp",
        "when": "textInputFocus && vim.mode == 'Normal'",
        "args": {
            "by": "wrappedLine",
            "value": 1
        }
    },
    {
        "key": "j",
        "command": "cursorDown",
        "when": "textInputFocus && vim.mode == 'Normal'",
        "args": {
            "by": "wrappedLine",
            "value": 1
        }
    }
```

#### Keybinds I use
Would love to learn more about cool things you can do with vscode, but here's what I find very useful right now. A lot of these are especially useful when working just from a single laptop screen, as I like to be able to quickly and efficiently manage my screen real estate.

- `ctrl+backtick`: open terminal
- `cmd+1/cmd+2`: focus open panes
- `cmd+b`: toggle left side bar
- `cmd+alt+b`: toggle right side bar
- `cmd + r + m`: toggle focus current pane completely


## Alfred

One of the best apps out there. I use it every day(accourding to the stats, around 8 times per day):
![](/assets/images/alfred_stats.png)
Here are some of the things I use it for:

### File nav
`open + file` or `find + file` will search the disk for files, and either reveal them in finder or open them. This is probably what I use alfred for most, super easy and intuitive way of quickly getting to specific files or folders.

### App launcher
I use this to open any app with command+space. Because this is so quick and simple, I make the bottom icons hidden by default for more screen real estate:
```bash
$ defaults write com.apple.dock autohide -bool true
```

### Snippets
I use alfred to manage snippets for commonly typed things. For instance, typing /em will auto expand out my email, and I can use `cmd+shift+x` to browse these snippets

### Clipboard History Manager
Incredibly useful. I have `cmd+shift+c` mapped to clipboard history, where I can search through everything that I have copy pasted. Once you get used to using this, it fundamentally changes the way that you interact with your computer. Searchable and nice UI, looks like this:
![](/assets/images/clipboard.png)

### App Switching
I previously used an alfred workflow to switch to my commonly used apps(browser, code editor, LLM, and terminal). This worked, but I've since switched to using [karabiner elements](#karabiner-elements) for this task to get slightly better latency.

### Workflows
I use custom workflows sometimes as a way to launch or perform various automations. I've written many mini scripts over the years and alfred workflows is a great way to launch them. 

For example, when I was studying spanish I wrote a script that would automatically search google images, get the first stock photo, and copy the output to my clipboard, so that I could put that image in an Anki deck.

![](/assets/images/rug_gif.gif)

## Obsidian
![](/assets/images/obsidian_plus.png)

Simple enough to get started with, rich enough in features to be a forever daily driver, native vim motions support, everything stored as markdown files. It's like it was made for me.
(I never use that graph view by the way but it looks cool!)

### Why Obsidian

**Vim mode**

Native vim mode support. Since this is where I write and edit text, this makes a big difference for a notes app

**Speed**

Obsidian feels snappy to me in a way that Notion did not. Low boot time, and I can just get writing much faster. Key commands, search, in-file search, all work to minimize the friction I have getting around the app, and that adds up for me personally compared to Notion or Apple Notes

**Markdown**

I personally love markdown as a standard way of typing and formatting text. I don't want to have to fiddle with nav bar items just to set a header. This is also great with syntax highlighting with code blocks being supported, if I want to include some code in a note.

**Ease of Use/Sensible Defaults**

To me, Obsidian is the final form of a 'just works' note taking app for me. All I want in a note taking app is to be able to write things down, and quickly find those things later when I need them. I can do that quickly:
- `cmd+n` -> new file, name it, start typing, maybe link it do some other things
- `cmd+o` -> fuzzy search all my notes, immediately open the right one
- `cmd+shift+f` -> fuzzy search the contents of all my notes

**Linking between notes**

Really inuitive way of organizing and structuring relationships between notes. Typing `[[` will open a pop up to fuzzy seach over all your files to then link to it. Empty links are great too, new notes can be created this way.

**Daily notes**

I have `cmd+shift+d` mapped to open my daily note. Titled with the days date. I use these to jot down things that I'm working on that day, general thoughts, todos, anything really.

**Excalidraw**

Personally love diagramming with the Excalidraw plugin for things like architecture diagrams or otherwise.

### Some customization I have
I mapped `cmd+shift+p` to render the current markdown file with `xelatex` and `pandoc` and export as a pdf. Was somewhat confusing to get this set up but generally quite useful now that I have it.

### Other Apps I've tried
I have historically used a few different options for note taking apps.

- **Notion**: probably my second favorite after Obsidian. Loved using notion for several years. Really great table support, which I think is a disadvantage of Obsidian. Can't describe particularly why, but the usage of Notion just felt slightly bloated for me, Obsidian just felt like less friction to quickly write stuff down.
- **Apple notes**: I love using stock apple apps when I can; for instance, I use apple reminders as my main task management app. Still use this for some thigs, but Obsidian wins because of vim motions, and just a bit more maturity as a dedicated note taking app.
- **Vimwiki**: Would never consider this these days. Was great when I wanted vim motions note app, but too much friction to use.

## iTerm2
![](/assets/images/iterm.png)

Tried and true terminal emulator. I try to keep my terminal setup as minimal as possible, and only add to my `.zshrc` as needed. I installed nerdfonts and tokyo night theme though.

### Shell config
Every dev needs to interact with the shell, so it's at least worth investing some time to make it nice to use. 

#### FZF
I install fzf CLI tool [here](https://github.com/junegunn/fzf). It's used for a lot of other things I frequently use(like lazyvim). However, I also love it's default terminal settings:
`CTRL+R`: fzf through command history
`CTRL+T`: fzf files

#### Powerlevel10k
This is what I use to get my shell looking a bit nicer visually. Set it and forget it situation, I don't mess around with the options too much. I installed it [here](https://github.com/romkatv/powerlevel10k) with [zinit](https://github.com/zdharma-continuum/zinit), as well as these plugins:

```bash
zinit ice depth=1; zinit light romkatv/powerlevel10k
zinit light zsh-users/zsh-syntax-highlighting
zinit light zsh-users/zsh-completions
zinit light zsh-users/zsh-autosuggestions
zinit light Aloxaf/fzf-tab
```


## Karabiner Elements
![](/assets/images/karabiner.png)

I use karabiner elements to achieve low-level key remapping. This is one of the first things I install on a new machine- simple, but essential.

#### Caps lock -> ESC when tapped, CTRL when held
This is has to be the GOAT of keyboard maps. Especially when using vim, where ESC is essential for mode switching, the ergonomics of not having to move the pinky all the way up to the ESC key is huge. Also, CTRL+key now becomes super fast, and therefore widely useful- both in vim(for example, quick nav with CTRL+U and CTRL+D).

#### Right command + hjkl to arrow keys
This was a default karabiner option, but I actually use this more than you would think. This makes the ergonomics of any arrow key based navigation much, much better.

#### CTRL+Numbers to Apps
This is my attempt at mimicking i3-style workspace navigation. I previously tampered with [yabai](https://github.com/koekeishiya/yabai) and [aerospace](https://github.com/nikitabobko/AeroSpace) to do this, but tiling wasn't really that useful to me, and in the case of aerospace I found the workspaces to be a bit buggy. This is a great option to be able to context switch every time, consistently, without having to think about it.

Also, this is way better than any other option I've found because Karabiner is extremely low-latency.

##### Setting Up
Karabiner elements handles complex modifications with json. First, we need to get the bundle identifier of the app:
```bash
$ osascript -e 'id of app "Safari"'
# outputs com.apple.Safari
```
Then, we create a new complex modification in karabiner, and add this to the list of manipulators, with the bundle ID and keybind:

```json
    "manipulators": [
        {
            "conditions": [],
            "from": {
                "key_code": "3",
                "modifiers": { "mandatory": ["control"] }
            },
            "to": [{ "shell_command": "open -b com.anthropic.claudefordesktop" }],
            "type": "basic"
        }
    ]
}
```

##### Maps currently:
CTRL+1 -> Safari

CTRL+2 -> Cursor

CTRL+3 -> Claude

CTRL+4 -> iTerm2

CTRL+5 -> Obsidian

CTRL+6 -> Music

## Contexts
I try to move away from command+tab switching in favor of keybinds, but of course looking through open applications is still incredibly necessary if you're working with stuff that's not one of your most used apps. Contexts is the best app I've found to replace default command tab functionality.

#### Better default command-tab
Command tab now gives all open windows, not just applications. Incredibly useful.

#### Command-tab within application
CMD+` now lets you cycle through windows for the current application. Great when combined with [app keybinds](#ctrlnumbers-to-apps).

#### Fuzzy find open applications
Mapped to ctrl-space by default. I don't use this much but it's cool

## Rectangle
Also incredibly essential when for managing windows is the ability to quickly manage the display of multiple windows. I use these maps with Rectangle, and use these 100s of times per day:

`CMD+Shift+H`: current window fills left side of the screen
`CMD+Shift+L`: current window fills right side of the screen
`CMD+Shift+Enter`: maximize current window

I can send a window to another display with `CMD+Shift+HHHHHHH`, which is an interesting side effect. Could map is separately but this works well enough for me.

## Claude

I want a desktop app that I can use to maintain LLM conversations when needed, and right now Claude desktop does the trick for me. However, 3.7 has been annoying me recently. So might need to switch this to something else.