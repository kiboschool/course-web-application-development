# Cloud Hosts

Deploying means you aren't running your server from your laptop anymore.

If you were a business, you might buy a rack server, put it in a datacenter, and run your application there 24/7. But... setting up rack-mounted servers in datacenters takes time, as well as complication and upfront expense.

Other businesses decide to run their applications on servers they rent from some other company. More and more companies have emerged to _host_ applications. It's now relatively easy configure and run an application on a remote server from the web.

There are a few big name hosts, and a few more niche hosts that offer something in particular to developers, typically ease-of-use.

## Big-name Cloud Hosts

The biggest names in cloud hosting are Amazon AWS, Microsoft Azure, and Google Cloud. These platforms offer a comprehensive suite of tools for running all kinds of applications.

- They are typically cheaper at large scale than smaller providers.
- There are lots of resources and expertise available online for learning those platforms
- The platforms are quite complicated, since they have features to serve hundreds of different needs

There are a number of other large providers, including Oracle, IBM, Alibaba, Tencent Cloud, OVHCloud, Digital Ocean, and Linode. They are all offering roughly comparable services, with some differences in stability, ease of use, price, and available features.

Learning to use any of these platforms takes a good deal of effort, so we're not going to do that in this class. There are lots of online tutorials for configuring applications on those platforms, if you'd like to explore.

## Developer-experience focused hosting platforms

Configuring applications to run well on AWS or Google Cloud is complicated, since those services can support tons of configuration. Another class of host focuses on making the developer experience very easy. They cut down on features and configuration, but make getting started hosting applications very simple.

Typically, they offer features like:
- easy command-line deploys
- connection to github to deploy on push to the `main` branch
- deploy using a _buildpack_ (to auto-configure based on your app code)
- deploy using a docker container (a way to customize the installation and configuration of your server)
- hosted databases

### Static Site hosts

There are a handful of companies that offer hosting for static sites:
- Vercel
- Netlify
- Surge
- Github Pages
- Cloudflare Pages

Vercel, Netlify, and Cloudflare also offer other services for making applications more complete, especially hosting 'serverless' functions that can work like a server.

Since we are running a server, these hosts won't work for our needs.

### Big developer-experience hosting platforms

The older generation of dev-focused hosting platforms includes:
- Heroku
- Firebase

They are still great ways to host applications, but Firebase has gotten more complicated since Google bought it, and Heroku removed their free tier since Salesforce bought it.

### New generation app hosts

The more recent generation of dev-focused server hosting platforms includes:
- Fly.io
- Render
- Railway

Since these platforms offer a free tier and easy deployments of Flask and Express apps, we'll use them for this course.

> Inevitably, there are plenty of platforms that aren't included here. Exclusion does not mean they are bad platforms, just as inclusion does not mean they are good.
