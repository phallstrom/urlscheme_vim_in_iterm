# Vim in iTerm

A small app to open special "viminiterm://" urls in a new iTerm tab in vim.

[Better Errors](https://github.com/charliesome/better_errors) is a RubyGem that provides, well, better errors in Rails applications during development.  One feature it provides is the ability to open the files, at the offending line, in the stacktrace in your editor of choice.  It does this by creating links to specially crafted URLs using custom schemes (ie. "txmt", "subl", "mvim").  I prefer to use standard CLI vim in [iTerm](http://www.iterm2.com/).

To make this work, I've written a small AppleScript based application that registers a URLSchemes of "viminiterm", then activates iTerm, opens a new default session, and starts vim loading the file and line.  Note that the application execs vim in the shell so once you quit vim, that iTerm session will close.  

## Getting Started
1. Download the [ZIP](https://github.com/phallstrom/urlscheme_vim_in_iterm/archive/master.zip) and unzip it.
2. Copy the 'Vim in Iterm' application to your Applications folder.
3. Double click it to open it.  The application needs to be run normally, just once, in order to register the URLScheme with the OS.
5. You can click [here]('viminiterm://open?url=file:///etc/bashrc&line=3') to
   trigger the registration or manually insert the following snippet into the
   browser: `viminiterm://open?url=file:///etc/bashrc&line=3`

## Integrate with Better Errors
Create 'config/initializers/better_errors.rb' with the following contents and restart your Rails application.

```ruby
if defined? BetterErrors
    BetterErrors.editor = proc { |file, line| "viminiterm://open?url=file://#{file}&line=#{line}" }
end
```

## Example

An error is raised in the Rails application. Clicking the filename will open the 'viminiterm://' link.

![image](https://raw.github.com/phallstrom/urlscheme_vim_in_iterm/master/screenshots/better_errors.jpg)

The first time this happens your browser may prompt you to confirm you want to do it. Set your preferences and continue.

![image](https://raw.github.com/phallstrom/urlscheme_vim_in_iterm/master/screenshots/launch_application.jpg)

The application runs, and a new iTerm session is opened, opening vim with that file and line.

![image](https://raw.github.com/phallstrom/urlscheme_vim_in_iterm/master/screenshots/vim_in_iterm.jpg)
