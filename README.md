
<div align="center">

<h1> Hello! Welcome to Poll Me! </h1>

<div align="center">

[![forthebadge](https://forthebadge.com/images/badges/built-with-love.svg)](https://forthebadge.com) 
</div>

![GitHub top language](https://img.shields.io/github/languages/top/KabirSinghBhatia/polly)
![GitHub contributors](https://img.shields.io/github/contributors/KabirSinghBhatia/polly)
![GitHub language count](https://img.shields.io/github/languages/count/KabirSinghBhatia/polly)
![GitHub](https://img.shields.io/github/license/shahrk/polly)
![GitHub last commit](https://img.shields.io/github/last-commit/KabirSinghBhatia/polly)
[![build](https://github.com/KabirSinghBhatia/polly/actions/workflows/build.yml/badge.svg?branch=main)](https://github.com/KabirSinghBhatia/polly/actions/workflows/build.yml)
[![DOI](https://zenodo.org/badge/429940108.svg)](https://zenodo.org/badge/latestdoi/429940108)
[![Docker](https://img.shields.io/badge/Containerized-Docker-blue)](https://docs.docker.com/compose/)
[![Coverage Status](https://img.shields.io/badge/coverage-91%25-brightgreen)](https://coveralls.io/github/KabirSinghBhatia/polly?branch=main)
![lines of code](https://tokei.rs/b1/github/shahrk/polly?color=ff69b4&label=Lines%20of%20Code&style=flat-square)
[![Known Vulnerabilities](https://img.shields.io/badge/vulnerabilities-0-brightgreen)](https://app.snyk.io/org/shahrk/project/4e0a290f-50af-4ab4-9941-c3a7f4d8bea6)
[![CI](https://github.com/KabirSinghBhatia/polly/actions/workflows/workflow.yml/badge.svg)](https://github.com/KabirSinghBhatia/polly/actions/workflows/workflow.yml)   

</div>

<h1> 💎 What is Poll Me about? </h1>

Poll Me is a super tool for getting feedback using online polls to let you check in with your audience or customers at any time. Do you want to get the opinion of many people on a certain matter, but haven't found a device that supports a large number of users yet? Then Poll Me is the right place for you. With Poll Me, you can create instant polls, check on the live user feedbacks and gain access to our vibrant Analytics dashboard to get insight into your poll results. Poll Me enables the creation of robust polls that support the use of a large number of users. Each host can create their own virtual room where they can publish their questions and share them with a large number of people. With pre-built survey templates, different survey types can be created and the results can be viewed by both host and player after answering the question. 

The following technologies were used for the development of this project:  

<p align="left">
  <a href="https://www.reactjs.org" target="_blank">
    <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original.svg" alt="react" width="30" height="30"/>
  </a>
  <a href="https://www.typescriptlang.org/" target="_blank"> 
    <img src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/typescript/typescript.png" alt="ts" width="30" height="30"/>
  </a> 
  <a href="https://www.redis.io" target="_blank"> 
    <img src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/redis/redis.png" alt="redis" width="30" height="30"/>
  </a>
  <a href="https://developer.mozilla.org/en-US/docs/Glossary/HTML" target="_blank"> 
    <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-plain.svg" alt="js" width="30" height="30"/>
  </a>
  <a href="https://aws.amazon.com/" target="_blank"> 
    <img src="https://raw.githubusercontent.com/github/explore/fbceb94436312b6dacde68d122a5b9c7d11f9524/topics/aws/aws.png" alt="aws" width="30" height="30"/>
  </a>
  <a href="https://developer.mozilla.org/en-US/docs/Glossary/CSS" target="_blank"> 
    <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-plain.svg" alt="css" width="30" height="30"/>
  </a>
</p>  


<h1> 📐 Architecture </h1>

<img src="https://github.com/hetthakkar/polly/blob/lorenz_branch/images/Architecture.png" width="600"/>

<h1>Deployment details P1 </h1>

<h2>Backend</h2>

The backend API is deployed on AWS Lambda using the [serverless framework](https://www.serverless.com/). Automated deploys are setup via a Github action that detects pushes to the main branch in the backend directory present in the project root. The action performs the following steps
- Install dependencies using `npm install`
- Generate prisma client(more about Prisma ORM in `./backend/README.md`)
- Push pending migrations to the database `npx prisma push db`
- Deploy the service on AWS Lambda `npx serverless offline`

The above action requires the following environment variables to be set

- `DATABASE_URL` (URL of your postgres database)
- `SERVERLESS_ACCESS_KEY`(Access key for the serverless framework generated from the [serverless dashboard](https://app.serverless.com))
- `JWT_SECRET`(Key used to sign auth tokens using JWT)
- `ALLOWED_ORIGIN`(Origins that are allowed via CORS)

When a service is deployed to AWS via the serverless framework, the following things happen

- Code is zipped and pushed to an S3 bucket
- API gateway service is created(as we use `http` events for our lambda functions)
- An aws lambda function is created/updated for each function defined in the `serverless.yml` file

<h2> Frontend </h2>

Frontend of the application is deployed on [Netlify](https://netlify.com). Netlfiy detects changes to the front end and creates a production optimized build by running the command

    npm run build

The static site assets are then served via Netlify's CDNs. 

Note: There are many other providers that provide static site deployments like Vercel, AWS Amplify, etc that can be swapped for Netlify in this project

<h1> 📊 UML Diagram </h1>

<img src="https://github.com/hetthakkar/polly/blob/lorenz_branch/images/UML%20Diagram.png" width="600"/>

<h1> 🚀 Local development setup </h1>

<h2> Backend </h2>

- Switch to backend directory
 
      cd backend
- Install dependencies
 
      npm i
- Create and populate `.env` file from the `env.example` template
- Generate prisma client
 
      npx prisma generate
- Start local serverless API

      npx prisma db push
- Pushes schema into the local Postgres server

      npx serverless offline      
            
Performing database changes(Refer [prisma docs](https://www.prisma.io/docs/))

- Make your schema changes in the `prisma/schema.prisma`
- To create a migration, use the command

      npx prisma migrate dev --name <migration_name>

<h2> Frontend </h2>

- Switch to frontend directory
 
      cd frontend
- Install dependencies
 
      npm install
- Create and populate `.env` file from the `env.example` template
- Start local serverless API 
 
      npm run start
      
<h1>Deployment details P2 </h1>

By using docker we could deploy the whole system in one single command : 

    “Docker compose up”

The above single command set up the whole environment and downloads the dependencies to make it run seamlessly on any platform.


