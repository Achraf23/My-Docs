---
title: Wordpress Plugin Development
type: docs
---

### Action hooks vs Filter hooks
-  an action takes the info it receives, does something with it, and returns nothing. I
-  a filter takes the info it receives, modifies it somehow, and returns it.

### Examples of Wordpress filter hooks
- `apply_filters()` **creates** a filter hook.
    
- `add_filter()` **attaches** a function to that hook.
    
- When your code runs and hits `apply_filters()`, WordPress will run all functions added through `add_filter()` and modify the value.


wordpress supports **callbacks** of the form array( 'ClassName', 'methodName' )
```
add_action('admin_init', array( 'Akismet_Admin', 'admin_init' )
```


### What is actually a Wordpress hook
if you find a `do_action('something');` in the core, you can hook in with `add_action('something','my_function');`.

If you find an `apply_filters('something', $value)` in the core, you can filter that $value with `add_filter('something', 'my_function');`.

==> Some hooks are not documented and can still be used to hook into core Wordpress code. This is very convenient !


## InjectGUARD Plugin Development Wordpress
This plugin affects mainly the `edit-commments.php` PHP page in Wordpress administration panel.
The comments are displayed using a `WP_List_Table::display()` method

There are hooks that exist to add a column in the Comments table or edit row attributes but no hooks exist for editing the colors and the core HTML structure of the table

So a solution is to override the `WP_List_Table` class either by creating a new class from scratch or extending the `WP_List_Table` and custominzing it to our needs



### Example usage of an undocumented hook to override WP_list_comment_table Class 

This particular class is used in edit-comments.php

discussion : https://wordpress.stackexchange.com/questions/134961/edit-default-comments-page-in-wp-admin
https://gist.github.com/paulvandermeijs/9209651

```php
// admin_head-edit-comments.php is an action hook that allows us to inject code 
// in the edit-comments.php page before the html is loaded in the admin panel
add_action("admin_head-edit-comments.php", function() {
});
```

To really see how this operates, do the following
```php
// in my-plugin.php main file
add_action("admin_head-edit-comments.php", function() {
	global $prefix;
	echo $prefix . 'admin head called <br>';

});
```

```php
// in edit-comments.php
// When running your plugin, you should the echo below appearing before admin head called
// And if move the echo after the require_once, it will appear after admin head called
echo '____________________before admin header edit-comments.php<br>';

require_once ABSPATH . 'wp-admin/admin-header.php';
?>
```


### Wordpress translation handling 
```
// _e equivalent to echo
// sample-text-domain is a translation in the active language within wordpress
<p><?php _e( 'Done!', 'sample-text-domain' ); ?></p>

```

```
__( 'Quote from Hello Dolly song, by Jerry Herman:' )
// translation of the string Quote from...
```