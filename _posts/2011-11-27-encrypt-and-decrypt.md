---
title: encrypt and decrypt
author: 悟道
layout: post
permalink: /?p=1306
categories:
  - bash
tags:
  - bash
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

<div class="wp_codebox">
  <table>
    <tr id="p1306144">
      <td class="code" id="p1306code144">
        <pre class="bash" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">################### Begin gpg functions ##################</span>
encrypt <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#123;</span>
<span style="color: #666666; font-style: italic;"># Use ascii armor</span>
gpg <span style="color: #660033;">-ac</span> <span style="color: #660033;">--no-options</span> <span style="color: #ff0000;">"$1"</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
bencrypt <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#123;</span>
<span style="color: #666666; font-style: italic;"># No ascii armor</span>
<span style="color: #666666; font-style: italic;"># Encrypt binary data. jpegs/gifs/vobs/etc.</span>
gpg <span style="color: #660033;">-c</span> <span style="color: #660033;">--no-options</span> <span style="color: #ff0000;">"$1"</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
decrypt <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#123;</span>
gpg <span style="color: #660033;">--no-options</span> <span style="color: #ff0000;">"$1"</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
pe <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#123;</span>
<span style="color: #666666; font-style: italic;"># Passphrase encryption program</span>
<span style="color: #666666; font-style: italic;"># Created by Dave Crouse 01-13-2006</span>
<span style="color: #666666; font-style: italic;"># Reads input from text editor and encrypts to screen.</span>
<span style="color: #c20cb9; font-weight: bold;">clear</span>
<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">"         Passphrase Encryption Program"</span>;
<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">"--------------------------------------------------"</span>; <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">""</span>;
<span style="color: #c20cb9; font-weight: bold;">which</span> <span style="color: #007800;">$EDITOR</span> <span style="color: #000000; font-weight: bold;">&&gt;/</span>dev<span style="color: #000000; font-weight: bold;">/</span>null
 <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #7a0874; font-weight: bold;">&#91;</span> <span style="color: #007800;">$?</span> <span style="color: #000000; font-weight: bold;">!</span>= <span style="color: #ff0000;">"0"</span> <span style="color: #7a0874; font-weight: bold;">&#93;</span>;
     <span style="color: #000000; font-weight: bold;">then</span>
     <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">"It appears that you do not have a text editor set in your
.bashrc file."</span>;
     <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">"What editor would you like to use ? "</span> ;
     <span style="color: #c20cb9; font-weight: bold;">read</span> EDITOR ; <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">""</span>;
 <span style="color: #000000; font-weight: bold;">fi</span>
<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">"Enter the name/comment for this message :"</span>
<span style="color: #c20cb9; font-weight: bold;">read</span> comment
<span style="color: #007800;">$EDITOR</span> passphraseencryption
gpg <span style="color: #660033;">--armor</span> <span style="color: #660033;">--comment</span> <span style="color: #ff0000;">"<span style="color: #007800;">$comment</span>"</span> <span style="color: #660033;">--no-options</span> <span style="color: #660033;">--output</span>
passphraseencryption.gpg <span style="color: #660033;">--symmetric</span> passphraseencryption
<span style="color: #c20cb9; font-weight: bold;">shred</span> <span style="color: #660033;">-u</span> passphraseencryption ; <span style="color: #c20cb9; font-weight: bold;">clear</span>
<span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">"Outputting passphrase encrypted message"</span>; <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">""</span> ; <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">""</span> ;
<span style="color: #c20cb9; font-weight: bold;">cat</span> passphraseencryption.gpg ; <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">""</span> ; <span style="color: #7a0874; font-weight: bold;">echo</span> <span style="color: #ff0000;">""</span> ;
<span style="color: #c20cb9; font-weight: bold;">shred</span> <span style="color: #660033;">-u</span> passphraseencryption.gpg ;
<span style="color: #c20cb9; font-weight: bold;">read</span> <span style="color: #660033;">-p</span> <span style="color: #ff0000;">"Hit enter to exit"</span> temp; <span style="color: #c20cb9; font-weight: bold;">clear</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
keys <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#123;</span>
<span style="color: #666666; font-style: italic;"># Opens up kgpg keymanager</span>
kgpg <span style="color: #660033;">-k</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
encryptfile <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#123;</span>
zenity <span style="color: #660033;">--title</span>=<span style="color: #ff0000;">"zcrypt: Select a file to encrypt"</span> <span style="color: #660033;">--file-selection</span> <span style="color: #000000; font-weight: bold;">&gt;</span> zcrypt
<span style="color: #007800;">encryptthisfile</span>=<span style="color: #000000; font-weight: bold;">`</span><span style="color: #c20cb9; font-weight: bold;">cat</span> zcrypt<span style="color: #000000; font-weight: bold;">`</span>;<span style="color: #c20cb9; font-weight: bold;">rm</span> zcrypt
<span style="color: #666666; font-style: italic;"># Use ascii armor</span>
<span style="color: #666666; font-style: italic;">#  --no-options (for NO gui usage)</span>
gpg <span style="color: #660033;">-acq</span> <span style="color: #660033;">--yes</span> <span style="color: #800000;">${encryptthisfile}</span>
zenity <span style="color: #660033;">--info</span> <span style="color: #660033;">--title</span> <span style="color: #ff0000;">"File Encrypted"</span> <span style="color: #660033;">--text</span> <span style="color: #ff0000;">"<span style="color: #007800;">$encryptthisfile</span> has been
encrypted"</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
decryptfile <span style="color: #7a0874; font-weight: bold;">&#40;</span><span style="color: #7a0874; font-weight: bold;">&#41;</span>
<span style="color: #7a0874; font-weight: bold;">&#123;</span>
zenity <span style="color: #660033;">--title</span>=<span style="color: #ff0000;">"zcrypt: Select a file to decrypt"</span> <span style="color: #660033;">--file-selection</span> <span style="color: #000000; font-weight: bold;">&gt;</span> zcrypt
<span style="color: #007800;">decryptthisfile</span>=<span style="color: #000000; font-weight: bold;">`</span><span style="color: #c20cb9; font-weight: bold;">cat</span> zcrypt<span style="color: #000000; font-weight: bold;">`</span>;<span style="color: #c20cb9; font-weight: bold;">rm</span> zcrypt
<span style="color: #666666; font-style: italic;"># NOTE: This will OVERWRITE existing files with the same name !!!</span>
gpg <span style="color: #660033;">--yes</span> <span style="color: #660033;">-q</span> <span style="color: #800000;">${decryptthisfile}</span>
zenity <span style="color: #660033;">--info</span> <span style="color: #660033;">--title</span> <span style="color: #ff0000;">"File Decrypted"</span> <span style="color: #660033;">--text</span> <span style="color: #ff0000;">"<span style="color: #007800;">$encryptthisfile</span> has been
decrypted"</span>
<span style="color: #7a0874; font-weight: bold;">&#125;</span>
&nbsp;
<span style="color: #666666; font-style: italic;">################### End gpg functions ##################</span></pre>
      </td>
    </tr>
  </table>
</div>

From:<http://www.novell.com/coolsolutions/tools/17142.html>