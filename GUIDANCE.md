# Apache for PHP on Wodby

What this service adds to the Apache service it is based on: it serves a PHP application's static files and passes PHP requests to the linked PHP service.

## How requests are handled

The service sets `APACHE_VHOST_PRESET` to `php`:

- The directory index is `index.php` (`APACHE_DIRECTORY_INDEX`).
- A request for a `.php` file that exists under the document root is passed to the PHP service over FastCGI. A `.php` path with no file is not passed on.
- Everything else is served by Apache as a file. The preset has no front controller rule: routing every path to `index.php` comes from the application's own `.htaccess`, which Apache reads.

## Backend link

The link to a PHP-FPM service sets `APACHE_BACKEND_HOST` and `APACHE_BACKEND_PORT`, the FastCGI target. Apache passes the script as a path on its own disk, so the PHP service must have the code at the same path. Both images are built from the same source for that reason: this service has no repository of its own and is built from the source of the linked PHP service, copied to `/var/www/html`.

## Document root

The `docroot` setting (variable `DOCROOT_SUBDIR`) has no default here: the repository root is served until it is set, for example to `public` or `web`. `APACHE_DOCUMENT_ROOT` is `/var/www/html/` followed by it.

## Variables that matter most

In addition to those of the Apache service: `APACHE_FCGI_PROXY_TIMEOUT` (how long Apache waits for PHP) and `APACHE_FCGI_PROXY_CONN_TIMEOUT`.

## Static files

Static files are served from the built image: a changed asset needs a new build and deployment of this service.

## Check the result

- `httpd -S` prints the virtual host in effect.
- `curl -sI localhost/` from inside the container returns the application's response when the PHP service is reachable.
