---
title: Session Configuration
---

Configuring Sessions
========================

Bolt supports nearly all methods of storing user session data, including plain
files, Memcached, and Redis. By default, it will adapt to the settings in 
your `php.ini` file, but you can also configure how you'd like your sessions 
to be set up in your `app/config/config.yml` file.


<p class="note"><strong>Note:</strong> The config file is in the YAML format,
  which means that the indentation is important. Make sure you leave leading
  spaces intact.</p>
    
  - **Files** - The default for most PHP installations is to store session data in
  files on the disc. Because PHP's native C code accesses filesystem with different 
  permissions than Bolt, if your php.ini is using the default (files) handler, Bolt 
  will store your user session data in a `cache/.sessions` folder. Of course, you can
  overwrite this value by setting the folder in your `app/config/config.yml` file.
  
  ```yaml
  sessions:
    save_path: "/your/sessions/folder"
  ```
  
  - **Memcached** - Memcached is a "free & open source, high-performance, distributed 
  memory object caching system". It can help you store your session data across many
  servers. You can configure one or more Memcached server connections in your `php.ini` 
  file or overwrite those values in `app/config/config.yml`.
  
  - **Redis**  - "Redis is an open source (BSD licensed), in-memory data structure store, 
  used as database, cache and message broker." It can also help you to store your session
  data a cross multiple servers. You can configure one or more Redis server connections in
  your `php.ini` file or overwrite them in `app/config/yml`.
  

Memcached or Redis connections can be configured in your `app/config/config.yml` file a 
few ways.

```yaml
sessions:
  save_handler: memcached # or redis
  
  # Can be defined as comma-separated connection strings:
  save_path: 127.0.0.1:1234?weight=0,127.0.0.2:5678?weight=1
  # OR an array of connections:
  connections:
    - 127.0.0.2:1234?weight=0
    - host: 127.0.0.2
      port: 5678
      weight: 1
```

In addition to the configuration values mentioned above, you can also change a number of
settings in `app/config/config.yml` to configure how cookies are stored and validated
in your users' browsers. Here are some of those settings and their defaults.

```
sessions:
  name: bolt_session_

  # The length of time a user stays 'logged in'. 0 means the session should end when 
  # the browser is closed.
  cookie_lifetime: 0
  
  # Set the session cookie to a specific domain. Leave blank, unless you know what
  # you're doing. When set incorrectly, you might not be able to log on at all.
  # If you'd like it to be valid for all subdomains of 'www.example.org', set this
  # to '.example.org'.
  cookie_domain: 

  # Only nly send cookies over secure connections. Set this to true if your site
  # will be served over HTTPS.
  cookie_secure: false
```
