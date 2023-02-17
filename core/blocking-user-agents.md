```
// Blocking Scrapers
function block_scrapers() {
  $allowed_url = '/'; // Url Here
  $blocked_user_agents = array('Python', 'curl', 'wget', 'httpie', 'scrapy', 'pandas', 'urllib', 'beautifulsoup', 'selenium', 'mechanize'); // Add additional user agents as needed
  $user_agent = $_SERVER['HTTP_USER_AGENT'];
  
  if (in_array($user_agent, $blocked_user_agents) && $_SERVER['REQUEST_URI'] !== $allowed_url) {
    header('HTTP/1.0 403 Forbidden');
    exit();
  }
}
add_action('init', 'block_scrapers');
```
