---
title: Wordpress Configuration
type: docs
---

### When to use Wordpress multisite
https://fr.wordpress.org/support/article/before-you-create-a-network/
https://learn.wordpress.org/lesson/setting-up-a-wordpress-multisite-network/

A multisite network is a good solution where you have a number of sites that are similar in nature, but that need to be kept separate from each other.


### Wordpress multisite installation
Add this to `wp-config.php`
`define( 'WP_ALLOW_MULTISITE', true );`

**tutorial :** https://fr.wordpress.org/support/article/create-a-network/


**N.B :**
Please make sure the Apache `mod_rewrite` module is installed as it will be used at the end of this installation.
If `mod_rewrite` is disabled, ask your administrator to enable that module, or look at the [Apache documentation](https://httpd.apache.org/docs/mod/mod_rewrite.html) or [elsewhere](https://www.google.com/search?q=apache+mod_rewrite) for help setting it up



### Wordpress Security

**WordPress actions** allow you to execute custom code at certain points in the WordPress request-response lifecycle

_add_action()_ function to register a plugin's custom action
*do_action()* is when registered actions are executerd (Line 700 of wp-settings.php in WordPress core)


*plugin.php* : functions used by plugins, *do_action* for example


```
__( 'Quote from Hello Dolly song, by Jerry Herman:' )
// translation of the string Quote from...
```

#### User input Security
```js
';echo '<script>alert("message successfully sent")</script>';
```

Tried this script on my Wordpress user input (while connected with admin privileges) and it resulted in an XSS injection. The comment has been stored in the Database and did not get sanitized. 

Wordress does not filter malicious payloads by default. 


### Wordpress Plugin Development
```js
// _e equivalent to echo
// sample-text-domain is a translation to the active language within wordpress
<p><?php _e( 'Done!', 'sample-text-domain' ); ?></p>

```
