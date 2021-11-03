# Tutorial: Deploying a basic Echo app on Jekyo

Demo app [here](https://echo-demo.jekyo.app/)

### Prerequisites

Make sure you have [NodeJS](https://nodejs.org/en/download/), [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) and [git](https://github.com/git-guides/install-git) installed.

If it's your first time using **Jekyo**, you can **install** it by running the following command in your terminal:

`npm install -g jekyo`

### Sign in to Jekyo

You can sign in to Jekyo by running `jekyo user:signin`

```
➜  ~ jekyo user:signin 
Your email?: **************
Your password?: **********
You have successfully signed in!
```
If you don't have a Jekyo account, you can create one in the terminal by running `jekyo user:signup`. 

## 1. Create a basic Echo app

You can start your Echo project by using `jekyo create`

Using the **arrows** on your keyboard, select **echo** and press **enter**.  
```
? Select template
  None Creates only the application
  expressjs A basic app skeleton using [Express](https://expressjs.com/)     
  nuxt-js A boilerplate SSR application using [Nuxt.js](https://nuxtjs.org/) 
❯ echo A basic starter app using [Echo](https://echo.labstack.com/)
```
When prompted, enter the desired name for your Echo app. 

`Application name?: echo-tutorial`

This will create a basic Echo app in the current directory by cloning this [Echo starter app](https://github.com/jekyo/echo-getting-started) repository.

```
Cloning source code... OK
Application created!
```

### Deploy the Echo app on Jekyo

To deploy the app, first navigate to the newly created directory:

`cd echo-tutorial`

Now you can deploy this app to Jekyo by running: 

`jekyo deploy`

After a while, you should see something like this:

```
➜  Fetching source code ... OK
➜  Building application, this might take a while ... OK
➜  Publishing application, this might take a while  ... OK
➜  Deploying application ... OK        
➜  Waiting for application to start ... OK
➜  Visit your app on: https://echo-tutorial.jekyo.app ... OK
```

You can now browse to your Echo app on https://echo-tutorial.jekyo.app (replace 'echo-tutorial' with your app name)

## 2. Deploying an existing Echo app

Navigate to your local Echo app directory

`cd my-echo-app`

### Edit go.mod

At the start of the `go.mod` file, add a line specifying which version of Go your project is using, like this (forward slashes included):

```
// +heroku goVersion go1.17
```
If you don't, the build will use by default an older version of Go and it won't work. 

### Edit main.go

If your main file is named server.go or something else, rename it to `main.go` and edit your `e.Logger` line to look like this:

```
e.Logger.Fatal(e.Start(fmt.Sprintf("%s:%s", os.Getenv("HOST"), os.Getenv("PORT"))))
```

This will specify the necessary `PORT` and `HOST` variables for **Jekyo**.

### Import

Because we are using `fmt` and `os`, we need to import them :

```
import (
	"fmt"
	"net/http"
	"os"

	"github.com/labstack/echo/v4"
)
```

### Commit changes

Initialize a git repository if you haven't already done so by running `git init`. 

```
git add .
git commit -m "your commit message"
```

### Create an empty Jekyo app:

`jekyo create` 

Select 'none' using the **arrows** on your keyboard and press **enter**. This will create an app using your current directory. 

```
? Select template (Use arrow keys)
❯ None Creates an application from your current directory
```

Name your app: 

`Application name?: my-echo-app`

Run `jekyo link` to link your local app to the remote Jekyo app. Select 'my-echo-app' using the **arrows** on your keyboard and press **enter**.

```
? Select application (Use arrow keys)
❯ my-echo-app
```
### Now you can deploy this app to Jekyo by running: 

`jekyo deploy`

After a while, you should see something like this:

```
➜  Fetching source code ... OK
➜  Building application, this might take a while ... OK
➜  Publishing application, this might take a while  ... OK
➜  Deploying application ... OK        
➜  Waiting for application to start ... OK
➜  Visit your app on: https://my-echo-app.jekyo.app ... OK
```

You can now browse to your Echo app on https://my-echo-app.jekyo.app (replace 'my-echo-app' with your app name)

## Pushing local changes to Jekyo 

Add the newly modified file(s) to the git index by using [git add](https://www.atlassian.com/git/tutorials/saving-changes)

`git add filename`

Create a [git commit](https://github.com/git-guides/git-commit)

`git commit -m "your commit message"`

Now, simply deploy your app again:

`jekyo deploy`

You will see your changes on your live app after a short while. 