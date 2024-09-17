# Docker Setup

## [What is Docker?](https://github.com/jar285/UFO-JA373/wiki/What-is-Docker%3F#what-is-docker)

## Prerequisites
- Ensure Docker and Docker Compose are installed on your computer. You can download them from the [Docker website](https://www.docker.com/products/docker-desktop/).

- Feel free to visit our [Wiki](https://github.com/jar285/UFO-JA373/wiki) to learn more in-depth key concepts such as the Docker Kernel, containerization, virtualization, and troubleshooting tips.
 
### Creating a Docker Hub Account
- Visit [Docker Hub](https://hub.docker.com/) and sign up for an account.
- Once registered, you can create repositories to store your Docker images.

### Logging into Docker Hub from the Command Line
- **`docker login`**
- Enter your Docker Hub username and password.

# Setting Up a Basic Docker Project

## Step 1: Create a Simple Application
Create a directory for your project and navigate to it in your terminal.

```
mkdir my-docker-app
cd my-docker-app
```
Inside your project directory, create a simple ```app.py``` file with the following content:

```
from http.server import SimpleHTTPRequestHandler, HTTPServer

class MyHandler(SimpleHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.send_header('Content-type', 'text/plain')
        self.end_headers()
        self.wfile.write(b'Hello, Docker World!\n')

port = int(os.getenv('PORT', 3000))
server = HTTPServer(('0.0.0.0', port), MyHandler)
print(f'Server running on http://localhost:{port}')
server.serve_forever()
```


## Step 2: Create a Dockerfile
A Dockerfile is a script that defines the instructions to build a Docker image. Create a file named `Dockerfile` (no file extension) in your project directory and add the following content:

### Example Dockerfile for a Simple Python Application

```Dockerfile
# Use the official Python image from the Docker Hub
FROM python:3.9-slim
# This line specifies the base image for your application, in this case, a lightweight Python image.

# Set the working directory in the container
WORKDIR /usr/src/app
# Sets the working directory inside the Docker container where your application code will reside.

# Copy the requirements file if it exists
COPY requirements.txt ./
# Copies the requirements.txt file from your local machine to the current working directory in the container.

# Install application dependencies
RUN pip install --no-cache-dir -r requirements.txt
# Installs the Python dependencies specified in the requirements.txt file without using the cache to reduce the image size.

# Copy the rest of the application source code to the container
COPY . .
# Copies all the files and folders from your local project directory into the container.

# Expose the port your application will run on
EXPOSE 3000
# Exposes port 3000 so your application can be accessed from outside the container.

# Define the command to run your application
CMD ["python", "app.py"]
# Specifies the command to run your application when the container starts.

```
If your application has dependencies, make sure to list them in a ```requirements.txt``` file and include it in your project directory.

## Step 3: Build the Docker Image
With your Dockerfile in place, you can build a Docker image for your application. In your project directory, run the following command:

**`docker build -t my-docker-app . `**

## Step 4: Run the Docker Container

**`docker run -p 3000:3000 my-docker-app `**

This command maps port 3000 in the container to port 3000 on your host machine, allowing you to access your application in a web browser.

If you want to learn about run options, you can visit [here](https://docs.docker.com/engine/containers/run/)

## Step 5: Access Your Dockerized Application

Open your web browser and navigate to ```http://localhost:3000.``` You should see "Hello, Docker World!" displayed, indicating that your Dockerized application is running successfully.



## Starting the Services

### Docker Commands
- To start all services defined in your Docker Compose file, navigate to the directory containing your `docker-compose.yml` file and run:
  - **`docker-compose up -d`**
  - This command starts the containers in the background.

## Resetting the Testing Environment
- If you need to reset your environment, e.g., to clear test data:
  - **Stop all services and remove volumes**:
    - **`docker-compose down -v`**
  - **Restart the services**:
    - **`docker-compose up -d`**

### Viewing Logs
- To view logs for troubleshooting or monitoring application behavior:
  - **`docker-compose logs -f`**
  - The `-f` flag tails the log output in real-time.

### Shutting Down
- To stop and remove all running containers:
  - **`docker-compose down`**

## Docker Images

### Building Docker Images
- To build a Docker image for your application, ensure you have a `Dockerfile` in the same directory as your `docker-compose.yml`. Then run:
  - **`docker-compose build`**

## Pushing Images to Docker Hub

### Tagging Your Docker Image
- Before pushing your image to Docker Hub, tag it with your Docker Hub username and repository:
  - **`docker tag local-image:tagname username/repository:tag`**
  - For example:
    - **`docker tag myapp:latest johndoe/myapp:latest`**

### Pushing the Image
- Push the tagged image to your Docker Hub repository:
  - **`docker push username/repository:tag`**
  - For example:
    - **`docker push johndoe/myapp:latest`**

## Additional Tips
- Ensure that your `docker-compose.yml` and `Dockerfile` are correctly set up according to your project’s needs.
- Use `.env` files to manage environment variables securely.

