# travis-reactjs-example
Travis Continous Integration with React JS


# Setting up Continuous Integration Builds

First, make sure your react project is pushed into the GitHub and you have an account in TravisCI.
Travis CI also supports build and deploy for open source project. Read here.
The very first step in integrating Travis CI is to create a file named .travis.ymlwhich will contain the essential information about the environment and configurations for the build to run. For simplicity, we will just include the programming environment and the version. In our simple project, it is NodeJS version 8.0 which has LTS recently provided by NodeJS The final contents of the file .travis.yml will be as follows:

```
language: node_js
node_js:
  - "stable"
cache:
  directories:
  - node_modules
script:
  - npm test
  - npm run build

```

We will add this file in our project root folder like this and push it to our github repository.

In order to make this build file working, we need to link up our project to Travis. For that, we can go to our logged in account in Travis

<img src="https://github.com/abdullasulaiman/travis-reactjs-example/blob/master/images/AddRepo.png" alt="Add Repository"/>

And then click the + icon near to the My Repositories which will open a new window.

<img src="https://github.com/abdullasulaiman/travis-reactjs-example/blob/master/images/EnableTravis.png" alt="Enable Travis"/>

Then toggle the settings to enable the project. It will start the build process.

# Setting up auto deployment to GitHub Pages

In order to deploy to the github pages, we need to provide access_token to our build file. To obtain a new access_token we can go to.

https://github.com/settings/tokens/new


<img src="https://github.com/abdullasulaiman/travis-reactjs-example/blob/master/images/github_token.png" alt="Github Token"/>

About permission, we need repo level access.
Copy the value of this token. This is a private token that gives access to your GitHub repos.
Now we can go to our project build screen. Then navigate to the settings page and add the environment variables and paste the copied token as its value. Here I have named my variable as github_token.

<img src="https://github.com/abdullasulaiman/travis-reactjs-example/blob/master/images/github_token_env.png" alt="Adding Github Token to Environment variable"/>

To make our deployment work we need to add deployment script in our .travis.yml. Now, let's add it.

```
  language: node_js
node_js:
  - "stable"
cache:
  directories:
  - node_modules
script:
  - npm test
  - npm run build

deploy:
  provider: pages
  skip_cleanup: true
  github_token: $github_token
  local_dir: build
  on:
    branch: master
```

Here, $github_token will read the access token value from our environment variables that we set previously.

We need to let our app know which URL that it should look for. We can set the URL in our app package.json. In my case, it goes like

```
{
"name": "travis-reactjs-example",
"version": "0.1.0",
"private": true,
"homepage": "https://abdullasulaiman.github.io/travis-reactjs-example/",
"dependencies": {
    ........
}, 
....
}
```

It could vary on others but the format is like this.

https://<usename>.github.io/<repository_name>/
  
Now, we can commit and push our changes to our repo in Github. It will automatically trigger the build. After successful completion of our build, it will deploy our project into the gh-pages. Thus resulting our app running in the URL which in my case is



