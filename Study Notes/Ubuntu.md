Restart nginx:

> sudo systemctl restart nginx

Kill process running on port:

> sudo kill -9 \$(sudo lsof -t -i:3000)
