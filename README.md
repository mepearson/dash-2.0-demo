# Dash App in Docker Container: Demo App
This is a very simple Dash App to provide a demonstration repo for launching dash within a docker container. This repo can be used for standing up new dash applications within the TACC infrastructure syste,.


## Version History
This app is written in Dash 2.0.  For a Dash 1.0 app, please use the Dash 1.0 demo rep [https://github.com/mepearson/dash-demo]

## Dash App File Description
The files to run the dash app are contained within the 'src' folder of the directory. The code has been separated into component files as follows:
* app.py - the file to run the main Dash app. Other files are imported into here for use.
* config_settings.py - file to contain any security or configuration specific Settings
* data_processing.py - file to handle any data processing needs that aren't handled upstream of the application. The demo code merely imports the standard packages without any actual code, though most applications need extensive initial data wrangling and that code should go here. This file may be rendered obsolete in applications pulling from databases that can provide the required data views.
* make_components.py - file to generate custom functions to build reusable dash components from dynamic settings.
* styling.py - file for any styling choices that are provided directly from python and not from a css file located either externally or in the assets folder
* assets folder - folder to hold files such as css, data folders, etc. following standard dash app protocols.

# Development Previews

Development previews are built upon commits to the master branch. If you wish to preview the latest
build, you may use the `docker-compose.yml` file. On your local machine with Docker, run:

```
docker-compose up --force-recreate
```

Then browse to `localhost:8050` in your web browser.

# Automatic Container Build information from parent repository.
This repository was forked from the TACC [dash-container](https://github.com/TACC/dash-container) repo.  

## Configuring your repository for automatic container builds (text from original repo)

### Github Actions workflows

This repository comes with two Github Action workflows that automatically build Docker containers:

- [build-pr](./github/workflows/build-pr) builds commit sha tagged
images upon pull requests
- [build-main](./github/workflows/build-main) builds a commit sha tagged and `:latest` tagged image upon
pushes to main (such as when merging a pull request)

Both require specific Github repo configuration.

### Setting up a Dockerhub token

You will need to create a token for the account that will be used to push your repo.

- On [Dockerhub](https://hub.docker.com) go to your account's [security settings](https://hub.docker.com/settings/security).
- Click the **New Access Token** button and type in a description
- You will see a UUID value - this is your access token. Copy it immediately, as these can only
be read upon creation. You will not see this token again.

### Setting up a Github Actions environment

You will need to create a build environment with secrets to contain Dockerhub settings.

- In your Github repo, click on **Settings**. Then click on **Environments**
- Click on the **New Environment** button and name this environment `docker`. (You can change the
`environment` value in the workflows if you wish to call it something else or keep multiple environments)
- At the bottom of the screen you will see **Environment Secrets**. Click the **Add Secret** button to create secrets.
- Create a secret called `DOCKERHUB_TOKEN` and paste your Dockerhub token here
- Create a secret called `DOCKERHUB_USERNAME` and put the name of the corresponding user here
- Create a secret called `DOCKERHUB_REPO` and put your Docker repository name here. For example, this Github repo
autobuilds images at `jchuahtacc/dash-container`, so that is the value that is used for `DOCKERHUB_REPO`.

### Test it out

Upon pull requests and pushes to main, you will see the workflows perform autobuilds. You can
view the Action results by going to the **Actions** tag of your repo. You can also go to your [Dockerhub](https://hub.docker.com) page and make sure images are properly getting tagged and pushed
