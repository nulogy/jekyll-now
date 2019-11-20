---
layout: post
title: "Lazy-load NVM to speed up zsh initialization "
author: jiyou
date: 2019-02-19T17:05:37+00:00
---

**UPDATE**
Once appending `--no-use`,  ensure to `source $NVM_DIR/.nvm.sh` when actually needed. For example, `yarn install` will complain ` node: No such file or directory` 


I was curious as to why the zsh initialization was so slow. After some benchmarking .zshrc, I learned that oh-my-zsh and NVM were the main source of slow-down. For oh-my-zsh, I'm trying to see if I can avoid loading plugins that I rarely use to cut some time. However for nvm, simply passing `--no-use the following will make a big difference.

`[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" --no-use`

Benchmarking with bash's buil-in `time` command...

Before `--no-use`:

```
❯ for i in $(seq 1 5); do /usr/bin/time zsh -i -c exit; done
        1.43 real         0.65 user         0.62 sys
        2.42 real         0.66 user         0.61 sys
        1.42 real         0.65 user         0.61 sys
        1.42 real         0.65 user         0.61 sys
        2.43 real         0.66 user         0.62 sys
```

After `--no-use`:

```
❯ for i in $(seq 1 5); do /usr/bin/time zsh -i -c exit; done
        0.48 real         0.26 user         0.17 sys
        0.46 real         0.25 user         0.16 sys
        0.46 real         0.25 user         0.16 sys
        0.46 real         0.26 user         0.16 sys
        0.49 real         0.27 user         0.17 sys
```

Sources:

https://github.com/creationix/nvm/issues/539
https://github.com/michaelmoussa/dotfiles/commit/8d67223aad5885ffc17e540b00e00478dd3c44d2
https://blog.jonlu.ca/posts/speeding-up-zsh
