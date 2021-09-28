In this first example, we’re going to create a basic WordPress shortcode that inserts the Day Of The Indie avatar image below.

### Creating the Shortcode

The first step is to create the shortcode function. Inside the `custom-shortcodes.php` file, add the following block of code:
```
    function dotiavatar_function() {
         return '<img src="http://dayoftheindie.com/wp-content/uploads/avatar-simple.png" 
        alt="doti-avatar" width="96" height="96" class="left-align" />';
    }
```
In the code example above, the `dotiavatar_function` function returns a pre-determined image named `avatar-simple.png`.

The next step is to register the shortcode with WordPress using the built-in function `add_shortcode`. Still inside `custom-shortcodes.php`, add the following line of code:

    add_shortcode('dotiavatar', 'dotiavatar_function');

When you register a shortcode using the `add_shortcode` function, you pass in the shortcode tag (`$tag`) and the corresponding function (`$func`)/hook that will execute whenever the shortcut is used.

In this case, the shortcut tag is `dotiavatar` and the hook is `dotiavatar_function`.

**Note**: When naming tags, use lowercase letters only, and do not use hyphens; underscores are acceptable.

### Using the Shortcode

Now that you have the shortcode created and registered, it’s time to try it out! Whenever you want the DOTI avatar to appear inside the post content, you can use the shortcode instead:

    [dotiavatar]

### SHORTCODES WITH PARAMETERS (ATTRIBUTES)

In the previous example, there wasn’t much room to change things up. Let’s say, instead of pushing a single image, we’d like to be able to set which image to use using a parameter. You can do that by adding some attributes (`$atts`).

Once again, inside `custom-shortcodes.php`, add another function, like so:
```
    function dotirating_function( $atts = array() ) {

        // set up default parameters
        extract(shortcode_atts(array(
         'rating' => '5'
        ), $atts));

        return "<img src=\"http://dayoftheindie.com/wp-content/uploads/$rating-star.png\" 
        alt=\"doti-rating\" width=\"130\" height=\"188\" class=\"left-align\" />";
    }
```
The function above accepts a single parameter: `rating`. If a `rating` value is not passed, it uses a default string value of `5`. It does this by unwrapping the array of attributes using the built-in [`shortcode_atts`](https://codex.wordpress.org/Function_Reference/shortcode_atts) function, and combining the default values with values that may have been passed into the function.

Don’t forget to register the shortcode:

    add_shortcode('dotirating', 'dotirating_function');

With the shortcode function created, and the hook added, the shortcode is now ready to be used inside your post content:

    [dotirating rating=3]

Alternatively, you can omit the `rating`, and just go with the default value:

    [dotirating]

And that’s it! You now know how to create self-closing WordPress shortcodes. But there is another kind you can create.
