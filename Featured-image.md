## For Customization

### Get First Image
```
function catch_that_image() {
  global $post, $posts;
  $first_img = '';
  ob_start();
  ob_end_clean();
  $output = preg_match_all('/<img.+src=[\'"]([^\'"]+)[\'"].*>/i', $post->post_content, $matches);
  $first_img = $matches [1] [0];

  if(empty($first_img)){ //Defines a default image
    $first_img = "/images/default.jpg";
  }
  return $first_img;
}
```
### Set Post Thumbnail HTML
```
function filter_post_thumbnail_html( $html, $post_ID, $post_thumbnail_id, $size, $attr ) {

    $image = get_field( 'fl_image' );

    if ( ! empty( $image ) && (empty( $post_thumbnail_id ) || $post_thumbnail_id === -1) ) :

        $html = sprintf( '<img width="%s" height="auto" src="%s" class="attachment-post-thumbnail size-post-thumbnail wp-post-image" >', "100%", esc_url( $image)  );

    endif;

    return $html;
}

add_filter( 'post_thumbnail_html', 'filter_post_thumbnail_html', 20, 5 );
```
