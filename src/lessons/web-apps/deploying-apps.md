# Deploying apps

As we have seen in the previous lessons, creating web applications with Flask allows us to develop powerful and dynamic software accessible through a web browser. However, up to this point, we've been running our Flask applications on our local machines. This is excellent for development and testing, but what if you want to share your app with the world? That's where deploying to the cloud comes in.

## Why Deploy to the Cloud?

Deploying your Flask application to the cloud means making it accessible to anyone with an internet connection. Instead of running the app on your local machine, it runs on a server in a data center, ready to serve your app to anyone who requests it.

## Getting Started with Render

Render is a cloud provider that offers a platform to deploy web applications quickly and easily. They provide a simple and intuitive interface for deploying a variety of web applications, including Flask apps.

To get started with deploying a Flask app to Render, you'll need to follow a few steps:

1. **Create a Render Account:** If you don't have one already, you will need to create a Render account. You can do this by visiting [their website](https://render.com/) and following the sign-up process.

2. **Prepare Your Flask Application:** You can use [this repo](https://github.com/render-examples/flask-hello-world) as base, or just follow the instructions in [this page](https://render.com/docs/deploy-flask)

3. **Push Your Code to a Git Repository:** Render uses Git repositories to deploy code. If you haven't already, create a repository on GitHub, GitLab, or Bitbucket, and push your Flask app code to it.

4. **Connect Your Git Repository to Render:** Once your Git repository is ready, you can connect it to Render by following the prompts in the Render dashboard.

5. **Configure and Deploy Your Application:** After connecting your repository, you'll need to configure a few settings (like the build and run commands) and then deploy your application.

6. **Access Your Deployed App:** Once your app is deployed, you'll receive a unique URL to access it. Share this URL with others, and they can use your app from anywhere with an internet connection!