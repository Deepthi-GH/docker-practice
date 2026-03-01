FROM nginx:alpine

# Create non-root user
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop

# Remove default config (optional)
RUN rm /etc/nginx/conf.d/default.conf

# Copy custom nginx config
COPY nginx.conf /etc/nginx/nginx.conf
COPY static /usr/share/nginx/html/

# Fix permissions
RUN chown -R roboshop:roboshop /var/cache/nginx \
    && chown -R roboshop:roboshop /var/run \
    && chown -R roboshop:roboshop /usr/share/nginx/html

# Switch to non-root user
USER roboshop

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]


# FROM nginx
# RUN rm -rf /usr/share/nginx/html/* 
# RUN rm -rf /etc/nginx/nginx.conf
# RUN rm -rf /etc/nginx/conf.d/default.conf
# COPY nginx.conf /etc/nginx/nginx.conf
# WORKDIR /usr/share/nginx/html 
# COPY static .