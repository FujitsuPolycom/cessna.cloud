---
title: The Blog is Up!
subtitle: Welcome to my blog and first official post.
category: Tech
date: 2021-10-24 01:15:45
tags: 
  - CI/CD 
  - Cloud 
  - AWS
  - Devops
  - homelab
---

### What Even Is This
Welcome to my blog and first official post. The plan is to document my adventures in all things technology and backpacking. Yep, that's right, my yin and yang of hobbies. 

Currently my technology interests lie in all things cloud, linux, infrastructure as code, and automation. My day job doesn't present many oppurtunities for experimentation with the latest and greatest of the technologies listed above so what you'll find here will be a whole lot of home lab dabblings. 

In the backpacking category I see myself mostly posting trip reports. I have roughly a backlog of trips to document as well as many future adventures.

### The Technical Deets

This is hosted as a static website in an [AWS S3 bucket](https://aws.amazon.com/s3/) with DNS handled by [Route 53](https://aws.amazon.com/route53/), CDN by [CloudFront](https://aws.amazon.com/cloudfront/), and SSL cert provided by [AWS Certificate Manager](https://aws.amazon.com/certificate-manager/). 

Local administration of the blog is done through the [Hexo blog framework](https://hexo.io/) with the blog posts written in markdown with my editor of choice, [VSCode](https://code.visualstudio.com/).

The workflow goes like this:

1. Generate a new post locally with Hexo
``` bash
$ hexo new "The First Post"
```
2. Edit/write the markdown file created for the post in vscode
3. Git commit and push the changes to my Github repo
4. [AWS CodeBuild](https://aws.amazon.com/codebuild/) has a webhook in to GitHub and fires off a build project when changes are POSTed
5. The CodeBuild project runs Hexo in an Ubuntu AMI to generate the static pages for the website and then copies them to the S3 bucket
``` bash
$ hexo generate
$ cd public/ && aws s3 sync . s3://websitebucket/
```

That's the quick and dirty. I'll do an entire write on this soon.

