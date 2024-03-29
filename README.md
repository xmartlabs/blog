# Xmartlabs Blog
The purpose of this blog is to showcase some insight into our work and share data and tips related to the projects we tackle.
We will also keep it updated with info and news about Xmartlabs.

## Contents
* [Local setup](#local-setup)
* [Featured posts](#featured-posts)

## Setup
This blog was built using [Jekyll](https://jekyllrb.com), a simple, extendable and static site generator.
To set it up on your machine you have two options:

### Local setup
1. Clone the project into your machine: `git clone git@github.com:xmartlabs/blog.git`
2. Install Ruby 2.6.3 (you can use [rbenv](https://github.com/rbenv/rbenv))
3. Install Jekyll and bundler in this Ruby version by running: `gem install jekyll bundler`
4. Go to the folder for this repository and build the site with `jekyll serve` or `jekyll serve --host=0.0.0.0` (if you want to use it from your phone or other machine)
5. Now browse to http://localhost:4000 or http://YOUR-IP:4000

### Local setup using docker
1. Clone the project into your machine: `git clone git@github.com:xmartlabs/blog.git`
2. Install docker and docker-compose
3. Go to the folder for this repository and build the site with `docker-compose up`


## Test your blogpost

If you want to test your blogpost you have two options to try it out:

### Using the Staging environment
The blog has a staging environment hosted in [blog-staging.xmartlabs.com](https://blog-staging.xmartlabs.com/), which can be used to test the blogposts you’re working on.
That environment is the result of deploying the last commit of the [staging GitHub repository](https://github.com/xmartlabs/blog-staging).
So, if you want to deploy a new staging version you have to add the staging [GitHub repository](https://github.com/xmartlabs/blog-staging) remote url and push the commit that you want to deploy.

```sh
git remote add staging git@github.com:xmartlabs/blog-staging.git # Only the first time
git push staging
```

All pull requests are automatically deployed to the staging environment.
If you want to exclude it, you can add the label 'not-deploy' in your pull request.
If you want to deploy a new version of your pull request, you can add a new commit or add a label, in both cases the deploy trigger will be executed.


**IMPORTANT:**

Newest blogposts will be shown on the featured section.

## Featured posts
Last 3 posts are the featured posts.
You need to set the following custom variables in its [front matter](https://jekyllrb.com/docs/front-matter/):
These may take one of the following values:
    - top position: the image size needs to be around 574x385px
    - 2 blogposts in a secondary level position: the image size needs to be around 706x187px

- `featured_image: /images/my-new-post/featured.png`
Remember to place the image inside the post's folder. A different name and format can be used, just assign the correct path to the variable.

Also make sure your blogpost has `permalink: /:title/` in the blog post's front matter. We're no longer using the date in the blog post url.

> you can check if the variables are properly set up by `printenv | grep MEDIUM`

Next time you build or serve the locally the blog it will be sent to medium as draft story.


## Social Images

Social images can be defined using `social_image` and  `twitter_image` post variables.
- `social_image` dimensions have to be 1200x627 pixels
- `twitter_image` have to respect proportions 2:1, e.g. 1600x800 pixels

If these variables are not defined, `featured_image` is used by defalut.

## What to do if the CSS changes aren't applied when releasing?
Sometimes changes to the CSS aren't applied once the page is released to GitHub Pages, this means the old CSS will be used causing different problems that can't be reproduced locally.

To force GitHub to load the new CSS you can edit [this line at `head.html`](_includes/head.html#L8):
```html
<link rel="stylesheet" href="{{ "/css/main.css" | relative_url }}">
```
So far [adding](https://github.com/xmartlabs/blog/pull/74/commits/99ebef6dd332c80f3e63527cf9c1f8c8c468ef2d) (or removing, [when it was already there](https://github.com/xmartlabs/blog/pull/84/commits/6b1d2086e00e90ef3ed07dd8705e8b89c18ffa60)) an `id` parameter to the `/css/main.css` url has worked.
```html
<link rel="stylesheet" href="{{ "/css/main.css?id=2" | relative_url }}">
```
