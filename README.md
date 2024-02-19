### This is the production version of the laravel-nginx-dev with some modification for deployment
# Preparing a dockerized application for production requires a different approach interms of security and user interaction.  The following modification has been made specifically for deployment to production:
* A new Dockerfile has to be created for the nginx server
* Declare a new working directory that is pointing to the configuration file inside of the container: WORKDIR /etc/nginx/conf.d
* Copy the local config file to the working directory: COPY nginx/nginx.conf   .
* Run the mv command that will rename the file to the default nema inside the container: RUN mv nginx.conf default.conf
* Resort back to the default working directory: WORKDIR /var/www/html
* Copy all files from the src directory to the default location within the container: COPY src .
With this approach I have removed all bind mount and anonymous volumes to prevent source files from being over-written of access anonymously
