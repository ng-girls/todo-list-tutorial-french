 # Deploy your App to Github Pages
To deploy our changes to Github pages we will use the angular-cli-ghpages package
https://github.com/angular-buch/angular-cli-ghpages 

* You need to have a Github user
* You need to create a repostiroy for your project.
* You need to commit all the changes you made in the project
* You need to install angular-cli-ghpages

## Creating a Github user
If you already have a Github user you can skip this step.
To Create a Github user go to Github: https://github.com/
Fill the regetration form and make sure to validate your email address.

## Create your App repository
After logging in to Github.
Click on the `Start a project` button, and name the repository `ng-girls-todo` or any other name you like.

## Connecting your repository

Commit all your changes by runing this command in your project directory.
```
git add -A && git commit -m "Your Message"
```

Run the following command to connect your code to your repository.
make sure to replace the {YOUR_USERNAME} and {YOUR_REPO} with your github username and repository name.
```
git remote add origin https://github.com/{YOUR_USERNAME}/{YOUR_REPO}.git
git push -u origin master
```

## Deploying to Github Pages
First install angular-cli-ghpages.

```
npm i -g angular-cli-ghpages
```

Then simply run:

```
ng build --prod --base-href="/[your-repo-name]/"
angular-cli-ghpages
```

Your app will be available at https://[your-GH-username].github.io/[repo-name]

For more information see https://github.com/angular-buch/angular-cli-ghpages.

## Known Issues
On (windows) machines you  probably run into an issue like the following:
```
An error occurred!
 Error: Unspecified error (run without silent option for detail)
    at C:\Users\<myuser>\AppData\Roaming\nvm\v8.9.1\node_modules\angular-cli-ghpages\node_modules\gh-pages\lib\index.js:232:19
    at _rejected (C:\Users\<myuser>\AppData\Roaming\nvm\v8.9.1\node_modules\angular-cli-ghpages\node_modules\q\q.js:844:24)
    ...
```

Try to debug it with ``` angular-cli-ghpages -S ``` . If you get the following error:
```
fatal: could not read Username for \'https://github.com\': No error\n',
```

you can do the following

1. Create a Personal Access Token here: https://github.com/settings/tokens

2. Run the following command and replace your token, organisation (your user), repository, username and email:
```
angular-cli-ghpages --repo=https://<personal-access-token>@github.com/organisation/your-repo.git --name="Displayed Username" --email=mail@example.org
```

