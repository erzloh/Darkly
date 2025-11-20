# Local File Inclusion

## Description

This challenge demonstrates how improper handling of user-controlled paths in a web application can allow an attacker to read sensitive files from the server. The vulnerability arises when the application dynamically includes files based on user input without validation.

## How to Get the Flag

* The presence of a `page` parameter in the URL suggested that the application might be dynamically loading files.
* By testing with simple path traversal sequences like `../`, it became clear the application was resolving the path directly without validation.
* Incrementally adding more `../` allowed navigation further up the directory structure, eventually leading to access to sensitive files such as `/etc/passwd`.

The payload to get the flag:

```
http://localhost/?page=../../../../../../../etc/passwd
```

## Prevention of Vulnerability

To prevent LFI and path traversal attacks, applications must avoid including or reading files directly from user input. Instead, they should enforce strict allowlists.

Example secure implementation:

```php
<?php
$pages = [
  'home'   => __DIR__ . '/pages/home.php',
  'about'  => __DIR__ . '/pages/about.php',
  'signin' => __DIR__ . '/pages/signin.php',
];

$page_key = $_GET['page'] ?? 'home';
if (!array_key_exists($page_key, $pages)) {
    http_response_code(404);
    include $pages['home'];
    exit;
}
include $pages[$page_key];
```

This solution uses a fixed map of allowed pages rather than allowing arbitrary file paths.
