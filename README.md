Project Overview:
Goal: Deploy a basic web application using Docker containers.


Set Up Your Development Environment
After installing Docker verify the installaion:

    docker --version
    docker-compose --version

Create a Simple Web Application
1) Choose a Web Application:
For simplicity, let's use a basic Node.js web server.

2) Create a Project Directory:
Open a terminal and create a new directory for your project:

    mkdir docker-web-app
     cd docker-web-app

3) Create a Node.js Server:

Inside your project directory, create a file named server.js:

          const http = require('http');
          const port = 3000;
          
          const server = http.createServer((req, res) => {
            res.statusCode = 200;
            res.setHeader('Content-Type', 'text/plain');
            res.end('Hello, Docker!\n');
          });
          
          server.listen(port, () => {
            console.log(`Server running at http://localhost:${port}/`);
          });

4) Create a Dockerfile:
In the same directory, create a file named Dockerfile (no file extension) with the following content:

          # Use an official Node.js runtime as a parent image
          FROM node:14-alpine
          
          # Set the working directory in the container
          WORKDIR /app
          
          # Copy package.json and package-lock.json to the working directory
          COPY package*.json ./
          
          # Install dependencies
          RUN npm install
          
          # Copy the rest of the application code to the working directory
          COPY . .
          
          # Expose the port the app runs on
          EXPOSE 3000
          
          # Command to run the application
          CMD ["node", "server.js"]


5) Build and Run Your Docker Container

Build the Docker Image
In your terminal, run the following command from your project directory (where Dockerfile is located):

        docker build -t my-node-app .

This command builds a Docker image named my-node-app using the Dockerfile in the current directory (.).


6) Run the Docker Container:
After building the image, start a container based on this image:
 
          docker run -p 3000:3000 my-node-app

This command runs a new container named my-node-app and maps port 3000 of the container to port 3000 on your host machine.


7) Access Your Web Application:
Open your web browser and navigate to http://localhost:3000/. You should see Hello, Docker! displayed, indicating that your Node.js server is running inside a Docker container.




