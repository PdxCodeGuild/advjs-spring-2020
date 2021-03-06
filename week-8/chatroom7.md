# Chat Room - Phase 7

In this phase of the project, you will deploy your project so it is publicly accessible on the web!

**Note: since this assignment is more about deployment, and less about the chat app specifically, you can deploy another project if you want to.** Perhaps you have a side-project or a project from the Python course that you want to deploy.

There exists a spectrum of services available to deploy an app. On one end of the spectrum, we have a more bare-bones approach, where we use what is essentially just a linux distro that we can ssh into and do whatever we want with. On the other end of the spectrum, we have services that seek to automate much of the work that goes into setting up common deployment tasks, providing a deployment platform that is theoretically easier to use.

The terms you might hear to describe these services are generally "Platfrom as a Service" (PaaS) and "Infrastructure as a Service" (IaaS). Where PaaS generally describes the more opinionated pre-configured options, and IaaS generally describes the more bare-bones virtual private server (VPS) offerings.

Both options have their pros and cons. This debate is similar to the minimalist vs opinionated framework discussion we had earlier in the course.

For this assignment, I wanted to give you the choice to pick what style suits you best.

## Requirements

Deploy the project using one of the following options. I only chose options that I have experience with.

* [Upcloud](https://upcloud.com/)
  * IaaS
  * cheapest long term option
  * simplest VPS option
* [Heroku](https://www.heroku.com/)
  * PaaS
  * simplest and easiest option overall
  * [more expensive than other options](https://www.heroku.com/pricing) overall
  * Although free tier doesn't expire like some of the other options, your app will "fall asleep" and will be slow to "wake up"
* Amazon Web Services (AWS)
  * spans the IaaS -> PaaS spectrum more than Upcloud with its various offerings
  * all the services and the complex UI can feel overwhelming
  * offers a pretty good [1 year free trial](https://aws.amazon.com/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc)
* Google Cloud Platform (GCP)
  * Google's version of AWS, spans the IaaS -> PaaS spectrum
  * UI is nicer and feels less overwhelming than AWS imo
  * also has a [good free trial/tier](https://cloud.google.com/free/)
  * not used as much as AWS in industry though 
  * [Google Compute Engine](https://cloud.google.com/compute/) is more on the IaaS side
  * [Google App Engine](https://cloud.google.com/appengine/) is more on the PaaS side

### Other things to consider

* what platform has more employment opportunites
* what platform will teach you the most useful skills
* Cost. Free trials, free tier, cost once free period ends, etc.

As you may have imagined, the more bare-bones options will be cheaper, and will probably teach you more general skills. The more opinionated options will be easier to set up and may teach you more specific (easier to market) skills.

### My Advice

Choose Upcloud if you want the cheapest long-term option and/or like the idea of a more minimalist approach.

Choose Heroku if you want the easiest option.

Choose AWS if you want to gain experience with the AWS ecosystem because you think it is the most marketable skill for the types of jobs you want.

Choose GCP for similar reasons to AWS.

## Technical details to consider

* You will probably not want to run the create-react-app in watch/dev mode. Look at [CRA's deployment docs](https://create-react-app.dev/docs/deployment/)
  * You will need to make sure you are serving the static files
  * [This tutorial](https://daveceddia.com/deploy-react-express-app-heroku/) walks through how to set that up with Heroku
* Make sure to setup MongoDB. You could consider using a separate service for this. 
  * Heroku will require a separate service, as it is not a VPS so you cannot simply run `mongod` like you would in a VPS. 
  * [Atlas](https://www.mongodb.com/cloud/atlas) might be the best option
  * For VPS, see [mongodb's installation docs](https://docs.mongodb.com/manual/administration/install-on-linux/)
* For best security practices, your source code should not contain any private keys or "secrets". Especially if your source code is public on github. Put your secrets (for example, the secret when encoding the JWT) into environment variables.
  * this goes for API keys, credentials, etc. as well
  * For more, see [The Twelve-Factor App - Config](https://12factor.net/config)
  * With Heroku, see [Configuration and Config Vars docs](https://devcenter.heroku.com/articles/config-vars)
* You may want to grab the port from an environment var as well. Heroku will supply the port through the "PORT" env var, so it won't let you pick a port arbitrarily.
* if you are going with a bare-bones VPS, you should look into using an enterprise-ready web server such as [Nginx](https://nginx.org/) or [Caddy](https://caddyserver.com/)
  * you can use these to set up a [reverse proxy](https://en.wikipedia.org/wiki/Reverse_proxy) to proxy requests to your node apps
  * you can also use Nginx/Caddy to serve static files, set up load-balancing, and more
  * for setting up Caddy, I found [this tutorial](https://www.digitalocean.com/community/tutorials/how-to-host-a-website-with-caddy-on-centos-7) useful, though you may want to look for a tutorial that matches your linux distro (although many of the steps should be similar)
    * Update: Caddy 2 is not backword compatible with Caddy 1, see the [Caddy 2 docs](https://caddyserver.com/docs/v2-upgrade).

## More Advice

* Start with something simple like a "Hello World" app
  * this will greatly simplify the deployment process since there won't be any complex build steps, environment variables to setup, or a database
* After that, try deploying something more complex like the chat app (something that has a database at least)
* Please share docs with each other! I'm sure you all will find awesome tutorials and useful docs pages

## Extra Credit

Pick from the following:

* set up a domain name
* set up TLS (https)
* set up [continous deployment](https://en.wikipedia.org/wiki/Continuous_deployment)
  * basically this means to automate the deployment process so when new changes in the code repository are committed, the project will automatically deploy with the new changes
  * lots of tutorials for this sort of thing online. If you find a good one share it with the class!
* try out one of the other deployment platforms
* learn about docker and deploy the project as a container
* set up a firewall if you set up a VPS
* set up some type of monitoring
  * for VPS, check out [PM2](https://pm2.keymetrics.io/)

