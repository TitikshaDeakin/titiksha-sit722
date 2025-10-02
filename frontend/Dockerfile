# Serve static files with Nginx
FROM nginx:1.25-alpine

# Remove the default site
RUN rm -rf /usr/share/nginx/html/*

# Copy your Nginx config (uses your repo's nginx.conf)
# If your file is named differently, adjust the path.
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy static assets
COPY index.html /usr/share/nginx/html/index.html
COPY main.js    /usr/share/nginx/html/main.js

# Optional: static asset permissions
RUN chown -R nginx:nginx /usr/share/nginx/html

EXPOSE 80

# Healthcheck (optional)
HEALTHCHECK --interval=30s --timeout=3s --retries=3 CMD wget -qO- http://127.0.0.1/ || exit 1

# Nginx is the default entrypoint/cmd in the base image
