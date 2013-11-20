---
title: Disable WordPress Feed
author: 悟道
layout: post
permalink: /?p=934
categories:
  - tool
tags:
  - tool
---
<table>
  <tr cellpadding=0><td>
    热度:
  </td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td><td cellpadding=0><img src='http://210.75.224.29/wordpress/wp-content/plugins/statpresscn/images/sun_dark.gif' width=10 height=10 border=0 /></td></tr>
</table>

A really good feature for many websites and already a standard on many blogs is the possibility to subscribe via feed for new posts.

But if you use WordPress for a specific purpose, for example as a CMS, it&#8217;s possible that you really don&#8217;t need that feature because it has no extra value for your users. Maybe because you only have static pages or you just don&#8217;t want to spread your news this way.

For everybody who doesn&#8217;t need the feed functionality in WordPress I show you in a little tutorial how to deactivate all formats of a feed in WordPress.

The easiest way, which I personally don&#8217;t recommend, is to adjust your code in the core files. You can find the responsible code in `wp-settings.php`, in your root of WordPress.

<div class="wp_codebox">
  <table>
    <tr id="p93491">
      <td class="code" id="p934code91">
        <pre class="php" style="font-family:monospace;">    require (ABSPATH . WPINC . '/feed.php');</pre>
      </td>
    </tr>
  </table>
</div>

With this method you have an easy way to deactivate, but you have to do it again when the next update for WordPress is knocking on your door. That can be a torture, especially when the automatic update is coming along with WordPress 2.7 &#8211; [How core update in WordPress 2.7 works][1].

A little bit more time consuming method is to deactivate feeds via hook in your theme or a Plugin. You just have to copy the following lines and copy them into `functions.php` of your theme. If this file doesn&#8217;t exist, just create it and WordPress will recognize it.  
The feed is not deleted, but the user gets an info. In detail, the feed URL will still exist, but if the user put in the URL directly, he doesn&#8217;t get any content but a text, which is been placed in the following code.

<div class="wp_codebox">
  <table>
    <tr id="p93492">
      <td class="code" id="p934code92">
        <pre class="php" style="font-family:monospace;">    /**
    * disable feed
    */
    function fb_disable_feed() {
        wp_die( __('No feed available,please visit our &lt;a href="'. get_bloginfo('url') .'"&gt;homepage&lt;/a&gt;!') );
    }
    add_action('do_feed', 'fb_disable_feed', 1);
    add_action('do_feed_rdf', 'fb_disable_feed', 1);
    add_action('do_feed_rss', 'fb_disable_feed', 1);
    add_action('do_feed_rss2', 'fb_disable_feed', 1);
    add_action('do_feed_atom', 'fb_disable_feed', 1);</pre>
      </td>
    </tr>
  </table>
</div>

That&#8217;s an easy way to disable feeds on your website.  
I do adjustments like this also for my clients in the backend. I only show my clients what they really need to see. Functions, which he doesn&#8217;t need for his use are hidden &#8211; easily possible with my Plugin [Adminimize][2]. More about Adminimize in a future post.

<http://wpengineer.com/287/disable-wordpress-feed/>

&nbsp;

&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-

### Disable RSS in WordPress

WordPress doesn’t come with the ability to turn off RSS. There are no really easy ways to completely switch off or remove your RSS feeds in WordPress for private or semi-private blogs. You could delete the php files themselves in wp-includes, but you’ll have to do this everytime you upgrade. Here is a better way to solve the problem:

Visit “Appearance” and “Editor” in your admin menu. Edit the “Theme Functions” file (functions.php). After the opening

<div class="wp_codebox">
  <table>
    <tr id="p93493">
      <td class="code" id="p934code93">
        <pre class="php" style="font-family:monospace;">remove_action('do_feed_rss2', 'do_feed_rss2', 10, 1);
remove_action('do_feed_rss', 'do_feed_rss', 10, 1);
remove_action('do_feed_rdf', 'do_feed_rdf', 10, 1);
remove_action('do_feed_atom', 'do_feed_atom', 10, 1);</pre>
      </td>
    </tr>
  </table>
</div>

If you change the theme you’re using, you will need to do the same for your new theme. You may also want to remove references to these now non-existent feeds in your themes header file.

<http://www.doeswhat.com/2011/03/03/disable-rss-in-wordpress/>

 [1]: http://wpengineer.com/how-core-update-in-wordpress-27-works/
 [2]: http://wordpress.org/extend/plugins/adminimize/