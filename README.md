## Introduction

I hope you've heard about the WordPress rest API. WordPress rest API provides some endpoints which you can use to fetch data from your WordPress site.

Imagine that you are planning to create a mobile app for your WordPress blog. The job of the mobile app is to display your latest blog posts. But the problem is that when you make http request to receive recent posts, you will find many fields in the rest API response. You don't need all of these fields for your app and sometimes you will need some extra fields which are not returned by default in API response.

So, what can you do in such a situation? Yeah, don't be panic. it's really easy extending WordPress rest API as your need. The purpose of this tutorial is to show you how to extend WordPress rest API. I will divide this tutorial into several parts, this will help you to move forward step by step.

## Create A Plugin

Before we get started. First, I am going to create a basic plugin where I can save all of my codes. This is the best way to extend WordPress functionality or add unique features to your WordPress site.

To create a plugin create folder called "rest-api-tutorial" where we will save all of our plugin files. Inside that folder create a file "rest-api-tutorial.php" with the following code.

```php
/**
 * Plugin Name: Rest Api Tutorial
 * Description: How to extent WP RSET api from your custom plugin.
 * Version: 1.0.0
 * Author: upnrunn
 * Author URI: https://upnrunn.com/
 * License: GPL2+
 *
 * @package Rest_Api_Tutorial
 */

if ( ! defined( 'ABSPATH' ) ) {
	exit; // Exit if accessed directly.
}

// Define constants.
define( 'REST_API_TUTORIAL_PLUGIN_VERSION', '1.0.0' );
define( 'REST_API_TUTORIAL_PLUGIN_DIR', untrailingslashit( plugin_dir_path( __FILE__ ) ) );

// Include the main class.
require plugin_dir_path( __FILE__ ) . 'includes/class-rest-api-tutorial.php';

// Main instance of plugin.
function rest_tutorial() {
    return Rest_Api_Tutorial::get_instance();
}

// Global for backwards compatibility.
$GLOBALS['rest_tutorial'] = rest_tutorial();
```

Now create another file called "class-rest-api-tutorial.php" in the includes/ folder using the following code. This is our main plugin class.

```php
<?php
/**
* Main class.
*
* @package Rest_Api_Tutorial
*/

class Rest_Api_Tutorial {

    /**
     * Returns the instance.
     */
    public static function get_instance() {

        static $instance = null;

        if ( is_null( $instance ) ) {
            $instance = new self();
        }

        return $instance;
    }

    /**
     * Constructor method.
     */
    private function __construct() {
        $this->includes();
    }

    // Includes
    public function includes() {
    }
}
```

Finally our plugin is ready. In the next part, I will explain how to modify WordPress rest API response.