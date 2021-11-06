---
title: Blog Management with Hexo
date: 2021-11-04 15:16:41
subtitle: Local post creation, deletion, and testing.
category: 
  - Tech
  - Devops
cover_image: /images/3.jpg
tags: 
  - CI/CD 
  - Cloud 
  - AWS
  - Devops
  - homelab
---
### Blog Management

Notes, mostly for my sake, on how to locally generate blog posts using the hexo framework. Post creation, deletion, and local testing is covered here. Commiting to github and the CodeBuild pipeline that follows is for another post.

Quickly: 
``` bash
$ hexo new "Blog Post Title"
$ hexo clean
$ hexo generate
$ hexo server

//Before Git commit/push

$ ctrl+c
$ hexo clean
```

### The Initial Setup: Installing Hexo

I currently have the hexo framework installed on my local Windows machine (soon to be Linux). This required installing the [Node.js runtime environment](https://nodejs.org/en/), including npm, and being sure my workstation had Git (it does). Hexo is then installed with:
``` bash
$ npm install -g hexo-cli
```
To create the website I navigated to my git repository on my local machine and ran the hexo initialize command to generate a working directory for the website:
``` bash
$ hexo init cessna.cloud
$ cd cessna.cloud
$ npm install
```
Folder structure:
```bash
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

Site content lives in the ```source``` folder, mostly markdown files of blog posts. Templates for posts, pages, and drafts live in the ```scaffolds``` folder. Themes live in the... ```themes``` folder. ``_config.yml`` contains overall blog setup paramaters: Title, subtitle, timezone, folder directories, theme selection, etc. Those options won't be detailed here. See: [_config.yml configuration_](https://hexo.io/docs/configuration)

### Content management

Creating a post is simple:

``` bash
$ hexo new <title> 
```

Creating a compeltely new page:

``` bash
$ hexo new page --path about/me "About me"
```
To delete a post:
1. Delete the post in source/_posts
2. Run hexo clean to delete the database (db.json), assets, and public folder

### Generating and testing the blog: 

After creating a post and editing/writing it in vscode, save and then generate the website:
``` bash
$ hexo generate
```
This grabs the markdown posts in the source folder and builds the blog (index.html, etc) in a public and assests folder. 

To create a local running copy of the blog:
``` bash
$ hexo server
```
The local copy can be viewed at: http://localhost:4000


Once it is up to snuff, I shutdown the local server (ctrl+c), run ``` hexo clean ```, commit the changes to my github repository, and from there CodeBuild does its magic and gets the new post up and running in my cessna.cloud s3 bucket. Post on how that is setup coming soon...



