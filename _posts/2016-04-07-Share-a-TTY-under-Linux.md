---
layout: post
title: "Share a TTY under Linux"
author: ianpenney
date: 2016-04-07T21:44:55+00:00
---

From: https://www.linux.com/learn/using-screen-remote-interaction

1. Set the screen binary (/usr/bin/screen) setuid root. By default, screen is installed with the setuid bit turned off, as this is a potential security hole.

2. The teacher starts screen in a local xterm, for example via screen -S SessionName. The -S switch gives the session a name, which makes multiple screen sessions easier to manage.

3. The student uses SSH to connect to the teacher's computer.

4. The teacher then has to allow multiuser access in the screen session via the command Ctrl-a :multiuser on (all screen commands start with the screen escape sequence, Ctrl-a).

5. Next the teacher grants permission to the student user to access the screen session with Ctrl-a :acladd student where student is the student login ID.

The student can now connect to the teacher's screen session. 
The syntax to connect to another user's screen session is screen -x username/session.


