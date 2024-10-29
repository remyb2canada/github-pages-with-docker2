##################################################
# Dockerfile to build a GitHub Pages Jekyll site
# Last Update 2024-10-29
#
#   - Ruby latest (3.3.5, as of writing of this Dockerfile)
#   - Jekyll 3.10.0 (as per GitHub Pages dependencies https://pages.github.com/versions/)
#   - GitHub Pages 232 (as per GitHub Pages dependencies https://pages.github.com/versions/)
#
# Instructions
# 1. Copy and paste the content of this file in a file called Dockerfile
# 2. Open a Terminal (Command Prompt or PowerShell) and navigate where the Dockerfile is located
# 3. Build the Docker image using this command:
#       docker build -t my-jekyll-site .
#
#    Explanation of step 3:
#       - This command instructs Docker to build a new image based on the Dockerfile in the current directory
#       - '-t jekyll-site': Tags the image with the name 'my-jekyll-site'. This makes it easier to reference the image later.
#
# 4. Run the Docker container using this command:
#       docker run -p 4000:4000 -v ${PWD}:/usr/src/app my-jekyll-site 
#
#   Explanation of step 4:
#       - This command starts a new container from the 'my-jekyll-site' image and maps the necessary ports and volumes
#       - '-p 4000:4000':
#               maps a port on the host machine (4000) to a port in the container (4000).
#               This allows to access the Jekyll site running inside the container from the host machine at http://localhost:400
#       - '-v ${PWD}:/usr/src/app':
#               The -v flag mounts a volume from the host machine into the container. 
#               It mounts the current directory (${PWD}) on the host machine to the /usr/src/app directory inside the container. 
#               This allows the container to access and modify the files in your project directory on the host machine
#               If you're on a WINDOWS machine, change '${PWD}' to '%cd%'
#       - 'my-jekyll-site': 
#               This is the name of the Docker image to use for the container (the one built and tagged in the previous step). 
#
# The Jekyll site should be running on the new computer at http://localhost:4000.
##################################################

# Use the official latest Ruby image
FROM ruby:latest

# Set the working directory inside the container
# All subsequent commands will be run in this directory. 
# This is also where the Jekyll site files will be located
WORKDIR /usr/src/app

# Install Jekyll and other dependencies using RubyGems (the package manager for Ruby)
RUN gem install jekyll -v 3.10.0

# Copy all the files from the current directory on the host machine (where the Dockerfile is located)
# into the working directory inside the container (/usr/src/app). 
# This includes the Jekyll site files and any other necessary files
COPY . .

# Tell Docker that the container will listen on port 4000 at runtime (the default port that Jekyll uses to serve the site)
EXPOSE 4000

# Specify the default command to run when the container starts:
# Run 'jekyll-serve' with the following options:
# '--watch': Automatically regenerate the site when files change.
# '--force_polling': Force Jekyll to use polling to watch for changes (useful in environments where file system events are not supported).
# '--host 0.0.0.0': Make the Jekyll server accessible from outside the container.
CMD ["jekyll", "serve", "--watch", "--force_polling", "--host", "0.0.0.0"]
