# Use an official PHPMyAdmin image
FROM phpmyadmin/phpmyadmin

# Set environment variables
ENV PMA_ARBITRARY 1
ENV PMA_HOST mysql_cakedb
ENV PMA_PORT 3306
ENV MYSQL_USER droot
ENV MYSQL_PASSWORD Pass123
ENV MYSQL_ROOT_PASSWORD RootPass123
ENV UPLOAD_LIMIT 64M

# Expose port 80
EXPOSE 80

# Start PHPMyAdmin
CMD ["apache2-foreground"]


 
