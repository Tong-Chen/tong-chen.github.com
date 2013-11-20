---
title: bashrc bash_profile profile
author: 悟道
layout: post
permalink: /?p=2768
categories:
  - bash
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

`~/.bash_profile` is only sourced by bash when started in interactive login mode. That is typically only when you login at the console (Ctrl+Alt+F1..F6), or connecting via ssh.

When you log in graphically, `~/.profile` will be specifically sourced by the script that launches gnome-session (or whichever desktop environment you&#8217;re using). So `~/.bash_profile` is not sourced at all when you log in graphically.

When you open a terminal, the terminal starts bash in (non-login) interactive mode, which means it will source `~/.bashrc`.

The right place for you to put these environment variables is in `~/.profile`, and the effect should be apparent next time you log in.

Sourcing `~/.bash_profile` from `~/.bashrc` is the wrong solution. It&#8217;s supposed to be the other way around; `~/.bash_profile` should source `~/.bashrc`.

&nbsp;

<div>
  <p>
    Traditionally, when you log into a Unix system, the system would start one program for you. That program is a shell, i.e., a program designed to start other programs. It&#8217;s a command line shell: you start another program by typing its name. The default shell, a Bourne shell, reads commands from <code>~/.profile</code> when it is invoked as the login shell.
  </p>
  
  <p>
    Bash is a Bourne-like shell. It reads commands from <code>~/.bash_profile</code> when it is invoked as the login shell, and if that file doesn&#8217;t exist, it tries reading <code>~/.profile</code> instead.
  </p>
  
  <p>
    You can invoke a shell directly at any time, for example by launching a terminal emulator inside a GUI environment. If the shell is not a login shell, it doesn&#8217;t read <code>~/.profile</code>. When you start bash as an interactive shell (i.e., not to run a script), it reads <code>~/.bashrc</code> (except when invoked as a login shell, then it only reads <code>~/.bash_profile</code> or <code>~/.profile</code>.
  </p>
  
  <p>
    Therefore:
  </p>
  
  <ul>
    <li>
      <code>~/.profile</code> is the place to put stuff that applies to your whole session, such as programs that you want to start when you log in (but not graphical programs, they go into a different file), and environment variable definitions.
    </li>
    <li>
      <code>~/.bashrc</code> is the place to put stuff that applies only to bash itself, such as alias and function definitions, shell options, and prompt settings. (You could also put key bindings there, but for bash they normally go into <code>~/.inputrc</code>.)
    </li>
    <li>
      <code>~/.bash_profile</code> can be used instead of <code>~/.profile</code>, but you also need to include <code>~/.bashrc</code> if the shell is interactive. I recommend the following contents in <code>~/.bash_profile</code>: <pre><code>if [ -r ~/.profile ]; then . ~/.profile; fi
case "$-" in *i*) if [ -r ~/.bashrc ]; then . ~/.bashrc; fi;; esac
</code></pre>
    </li>
  </ul>
  
  <p>
    On modern unices, there&#8217;s an added complication related to <code>~/.profile</code>. If you log in in a graphical environment (that is, if the program where you type your password is running in graphics mode), you don&#8217;t automatically get a login shell that reads <code>~/.profile</code>. Depending on the graphical login program, on the window manager or desktop environment you run afterwards, and on how your distribution configured these programs, your <code>~/.profile</code> may or may not be read. If it&#8217;s not, there&#8217;s usually another place where you can define environment variables and programs to launch when you log in, but there is unfortunately no standard location.
  </p>
  
  <p>
    Note that you may see here and there recommendations to either put environment variable definitions in <code>~/.bashrc</code> or always launch login shells in terminals. Both are bad ideas. The most common problem with either of these ideas is that your environment variables will only be set in programs launched via the terminal, not in programs started directly with an icon or menu or keyboard shortcut.
  </p>
  
  <p>
    &nbsp;
  </p>
  
  <p>
    http://superuser.com/questions/183870/difference-between-bashrc-and-bash-profile
  </p>
  
  <p>
    http://askubuntu.com/questions/121073/why-bash-profile-is-not-getting-sourced-when-opening-a-terminal
  </p>
</div>