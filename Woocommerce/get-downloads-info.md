```
// Optional - Get the WC_Product object from the product ID
$product = wc_get_product( $product_id );

$output = []; // Initializing

if ( $product->is_downloadable() ) {
    // Loop through WC_Product_Download objects
    foreach( $product->get_downloads() as $key_download_id => $download ) {

        ## Using WC_Product_Download methods (since WooCommerce 3)

        $download_name = $download->get_name(); // File label name
        $download_link = $download->get_file(); // File Url
        $download_id   = $download->get_id(); // File Id (same as $key_download_id)
        $download_type = $download->get_file_type(); // File type
        $download_ext  = $download->get_file_extension(); // File extension

        ## Using array properties (backward compatibility with previous WooCommerce versions)

        // $download_name = $download['name']; // File label name
        // $download_link = $download['file']; // File Url
        // $download_id   = $download['id']; // File Id (same as $key_download_id)

        $output[$download_id] = '<a href="'.$download_link.'">'.$download_name.'</a>';
    }
    // Output example
    echo implode('<br>', $output);
}
```
