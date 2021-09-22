## Important Codes

### To See formatting

```
add_action('save_post', 'change_title');

function change_title($post_id) {
    $time = get_field('time',$post_id);
    $post_title = 'Topic created at '. $time;

    // unhook this function so it doesn't loop infinitely
    remove_action('save_post', 'change_title');

    // update the post, which calls save_post again
    wp_update_post(array('ID' => $post_id, 'post_title' => $post_title));

    // re-hook this function
    add_action('save_post', 'change_title');
}  
```
### acf/save_post
```
function create_title( $post_id ) {
    // Set variables
    $opposition = get_field( 'opposition', $post_id );
    $match_date_url = get_the_date( 'Y-m-d', $post_id );
    $match_date_title = get_the_date( 'd/m/y', $post_id );

    // Set post title and permalink
    $post_title = $opposition . ' v Team - ' . $match_date_title;
    $post_name = $opposition . ' v Team - ' . $match_date_url;

    // update the post, which calls save_post again
    wp_update_post( array(
        'ID'            => $post_id,
        'post_title'    => $post_title,
        'post_name'     => $post_name,
        )
    );
}

add_action( 'acf/save_post', 'create_title', 20 );
```

```
```

```
```

```
```

```
```

## Final Code
