# JavaDoc Publish
A GitHub action that publishes javadocumentation to GitHub pages automatically

## Quickstart 

### action.yml
To import the action into our action.yaml file add the following
```yml
- name: Deploy javadoc to Github Pages
        uses: dev-vince/actions-publish-javadoc@v1.0.1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

```
Also, we need to ensure that our workflow has write permissions to the repository.

```yml
permissions:
  contents: write
```

A full example of what our workflow should like is this
```yml
name: Deploy Javadoc

permissions:
  contents: write
  
on:
  push:
    branches:
      - master
      - main

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy javadoc to Github Pages
        uses: dev-vince/actions-publish-javadoc@v1.0.1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
To specify what java version and distrubution we want to use when compiling javadoc we can add a few inputs in our action.
```yml
- name: Deploy javadoc to Github Pages
    uses: dev-vince/actions-publish-javadoc@v1.0.1
    with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          java-version: "17" # Replace with your java version. Default is 17
          java-distribution: "adopt" # The distributor of the target JDK. See https://github.com/actions/setup-java for more information. Defauly is adopt
```
To specify what type of project we are using (gradle or maven) we need to specify with the following input
```yml
- name: Deploy javadoc to Github Pages
    uses: dev-vince/actions-publish-javadoc@v1.0.1
    with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          project: gradle # The project type. By default maven
```
To specify what branch the action should store your javadoc cotents specify with the following input
```yml
- name: Deploy javadoc to Github Pages
    uses: dev-vince/actions-publish-javadoc@v1.0.1
    with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          branch: "gh-pages" # The branch for the javadoc contents. By default gh-pages
```
All together we should get
```yml
- name: Deploy javadoc to Github Pages
    uses: dev-vince/actions-publish-javadoc@v1.0.1
    with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          java-version: "17" # Replace with your java version. Default is 17
          java-distribution: "adopt" # The distributor of the target JDK. See https://github.com/actions/setup-java for more information. Defauly is adopt
          project: gradle # The project type. By default maven
          branch: "gh-pages" # The branch for the javadoc contents. By default gh-pages
```

## Important!
In order for the page to be active, you must set the github page branch by navigating through Repository Settings > Pages > Build and Deployment > Branch and select the branch used to store the javadoc contents (by default gh-pages) and hit save. Another workflow should start that tests the branch for any errors before publishing to GitHub Pages. 