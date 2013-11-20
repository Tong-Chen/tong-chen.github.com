---
title: Some untested linux tricks
author: 悟道
layout: post
permalink: /?p=1299
categories:
  - bash
  - linux
tags:
  - bash
  - linux
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

1.**Per-directory bash history**

<div class="wp_codebox">
  <table>
    <tr id="p1299143">
      <td class="code" id="p1299code143">
        <pre class="bahs" style="font-family:monospace;"># # Replacement for builtin 'cd', which keeps a separate bash-history 
# # for every directory. 
function mycd() {
    history -w # write current history file builtin 
    cd "$@" # do actual cd local 
    HISTDIR="$HOME/.dir_bash_history$PWD" 
    # use nested folders for history 
    if [ ! -d "$HISTDIR" ]; then # create folder if needed 
        mkdir -p "$HISTDIR"
    fi 
    export HISTFILE="$HISTDIR/bash_history.txt" # set new history file   
    history -c # clear memory 
    history -r # read from current histfile 
}</pre>
      </td>
    </tr>
  </table>
</div>