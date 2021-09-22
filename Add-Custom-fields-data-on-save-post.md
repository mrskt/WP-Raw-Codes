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
### Field Value as Tags
```
add_action('save_post','custom_field_add_tags');

function custom_field_add_tags($post_id) {

 $post = get_post($post_id);

 //get values of custom fields and put into array

 $tag1 = get_post_meta($post_id, 'key_1', true);
 $tag2 = get_post_meta($post_id, 'key_2', true);
 $tag3 = get_post_meta($post_id, 'key_3', true);

 $tags_to_add = array($tag1, $tag2, $tag3);

 //now check if tag does not already exist (if no - add tag from custom field)

 $add_tags = array();

 foreach(get_the_terms($post_id, 'post_tag') as $term) {

    if(!in_array($term->slug, $tags_to_add))
        $add_tags[] = $term->slug;
 }

 if(!empty($add_tags))
    wp_add_post_tags($post_id, implode(',', $add_tags));
}
```

```
```

```
```

```
```

## Final Code
