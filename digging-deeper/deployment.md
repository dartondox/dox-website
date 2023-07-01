# Deployment

### To compile dart into machine code

```
$ dox build 
```

### Serve the app

```
$ bin/server
```

### Nginx Configuration <a href="#nginx-reverse-proxy" id="nginx-reverse-proxy"></a>

Running server with Nginx reverse proxy

```nginx
server {
  listen 80;

  server_name <YOUR_APP_DOMAIN.COM>;

  location / {
    proxy_pass http://localhost:<APP_PORT>;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_cache_bypass $http_upgrade;
  }
}
```
