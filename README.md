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

<img src="https://github.com/abdullasulaiman/travis-reactjs-example/blob/master/Add%20Repo.png" alt="Add Repository"/>

And then click the + icon near to the My Repositories which will open a new window.

<img src="https://github.com/abdullasulaiman/travis-reactjs-example/blob/master/EnableTravis.png" alt="Enable Travis"/>

Then toggle the settings to enable the project. It will start the build process.

# Setting up auto deployment to GitHub Pages

In order to deploy to the github pages, we need to provide access_token to our build file. To obtain a new access_token we can go to.

https://github.com/settings/tokens/new


