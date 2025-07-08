# Community Map

An interactive, self-service map showcasing members of your GitHub organization.

## Getting Started

The `main` branch of the repository contain all the tooling needed to manage maps.  In your fork, do not modify the `main` branch, and only commit changes in the `gh-pages` branch.
This will allow you to sync updates and fixes submitted upstream in your fork easily.

### Initial setup

1. Fork this repository to your organization;
1. Create a branch `gh-pages`: Branches / new Branch / New branch name: gh-pages, Source: main;
1. Make `gh-pages` the default branch of your fork: Settings / General / Default branch;
1. Adjust your community name, description in `_config.yml`;
1. Collect and setup the required API keys (see bellow);
1. Create an account on geoapify.com, add a project to get an API key, make it a secret on GitHub: Settings / Secrets and variables / Actions / New repository secret.  Name it `GEOAPIFY_KEY`.
1. Make sure your community members are allowed to trigger GitHub actions in your repository so that they can add their location to the map in self-service mode.

### Syncing your fork

1. Synchronize the `main` branch of your fork with the upsteam repository;
1. Merge the `main` branch of your fork into the `gh-pages` branch of your fork.

## API Keys

This project rely on 2 external services for geocoding (turning an address into a latitude and longitude) and for map tiles.  Both provide a generours free tier which should be enough for most uses.

### Geoapify

The free tier allow 3000 geocoding / day, which should be more than enough for almost any projects.

1. On [https://myprojects.geoapify.com/](https://myprojects.geoapify.com/):
   1. Create an account;
   1. Add a new project (e.g. map);
   1. Copy the API key;
1. On your GitHub fork of this project:
   1. Add a repository secret (Settings / Secrets and variables / Actions / New repository secret);
   1. Name it `GEOAPIFY_KEY`;
   1. Paste the API key as its value.

### Thunderforest

Thunderforest provide nice rendering of OpenStreetMap data.  Their free tier offer 150,000 tile requests per month.

**Warning**: as this API key will be exposed, you should use a dedicated user account and not re-use a key from another project.

1. On [https://manage.thunderforest.com/users/sign_in](https://manage.thunderforest.com/users/sign_in):
   1. Create an account;
   1. Copy your API key from the dashboard.
