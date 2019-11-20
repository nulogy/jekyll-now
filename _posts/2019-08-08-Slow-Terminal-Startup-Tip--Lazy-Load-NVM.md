---
layout: post
title: "Slow Terminal Startup Tip: Lazy Load NVM"
author: evanbrodie
date: 2019-08-08T14:24:07+00:00
---

For a long time, my ZSH shell windows/tabs have had very slow startup times, sometimes taking 5-10 seconds before `.zshrc` fully loads and the input cursor appears. This slows down my daily development cycles.

It turns out that loading NVM was the main culprit. Using [this Medium post](https://medium.com/@dannysmith/little-thing-2-speeding-up-zsh-f1860390f92) and [this gist](https://gist.github.com/fl0w/07ce79bd44788f647deab307c94d6922) as motivation, I have added this snippet to my `.zshrc` file in order to lazy load `nvm`, `npm`, `node`, and `npx` (copied from the gist, credit goes to that author). I have immediately observed major speed improvements in my shell speed load times.

```sh
lazynvm() {
  unset -f nvm node npm npx
  export NVM_DIR=~/.nvm
  [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
  if [ -f "$NVM_DIR/bash_completion" ]; then
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" # This loads nvm bash_completion
  fi
}

nvm() {
  lazynvm 
  nvm $@
}
 
node() {
  lazynvm
  node $@
}
 
npm() {
  lazynvm
  npm $@
}

npx() {
  lazynvm
  npx $@
}
```
