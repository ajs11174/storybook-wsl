
## WSL - Storybook Repo

---

This repo is to demonstrate that Storybook does not respond when started from WSL2. If you clone this repo into WSL2 it will not serve any data. If you clone this repo into Windows it will start.

Here's a screenshot of what Chrome responds with when served from WSL2:

![WSL_Chrome_Screenshot](WSL_Chrome_Screenshot.png "Title")

I can confirm that hitting the server with a curl from either WSL or Windows returns the index page. However, the browser does not receive any data (Tested with Chrome and Edge.)

---

### Steps Used to Generate this Project

### Set up an nx workspace

```bash
nx create-nx-workspace@latest --preset=ts
```

Change the apps and libs folders to `/apps` and `/libs` in `nx.json`

### Set up a React library
```bash
npm i @nrwl/react@latest
nx g @nrwl/react:library ui --style=none --unitTestRunner=jest --bundler=none
nx g @nrwl/react:component input --project=ui --export=true --style=none
```
Remove the auto generated `ui` component

### Set up Storybook and Generate Stories
```bash
npm i -D @nrwl/storybook
nx g @nrwl/storybook:configuration ui --uiFramework=@storybook/react --tsConfiguration=true --configureCypress=true
nx g @nrwl/react:stories ui
```

### Run the Storybook server
```bash
export NODE_OPTIONS=--openssl-legacy-provider
nx run ui:storybook
```