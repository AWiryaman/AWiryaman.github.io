---
layout: post
title: Creating the blog
---

## The Start

This summer, some of my friends and I decided that we should start blogs to accompany our personal websites. We decided to turn it into a little competition.

I had little experience with making a website so this project required a lot of Googling and resources.

The basis of my blog is [Jekyll hosted on GitHub pages](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/).

With little HTML or CSS experience, I knew that I would not be able to create a full website without some sort of template to go off of. I chose [hyde](https://github.com/poole/hyde), which is a two-column theme with a simple sidebar.

To customize the theme I looked towards a couple other blogs which used hyde or similar themes
- [Jonathon Bechtel's blog](http://jonathonbechtel.com/2015/11/16/building-my-first-blog-ever-using-jekyll-and-github-pages/)
- [Kyle Stratis's blog](http://kylestratis.com/2015/05/05/blog-setup-pt2/)


## Jekyll and GitHub pages

I began with a GitHub account and followed the instructions [here](https://pages.github.com/).
Key GitHub commands:

```
~ $ git add --all
~ $ git commit -m "Commit message"
~ $ git push -u origin master
```

This will push your local code into GitHub

The next step was setting up Jekyll, which is a simple, easy to use static site generator. Jekyll's [documentation](https://jekyllrb.com/docs/installation/) was really solid and I ran into no issues getting it up and running.

The essentials contained within the quick-start guide are:

```
~ $ gem install jekyll
~ $ jekyll new myblog*
~ $ cd myblog
~/myblog $ bundle install
~/myblog $ bundle exec jekyll serve
# => Now browse to http://localhost:4000
```

\*myblog would be the GitHub repo


## Hyde

[Hyde](https://github.com/poole/hyde) can be downloaded, cloned or manually copy and pasted in to your project.

The first file to be edited is `_config.yml`:
- `markdown: redcarpet` needs to be changed to `markdown: kramdown`

- `highlighter: pygments` needs to be changed to `highlighter: rouge`

- `relative_permalinks: true` needs to be removed

- all the other information below `# Setup` can be personalized


To look at the website so far you can always browse to the project and `bundle exec jekyll serve` and view it at http://localhost:4000

I'm not exactly sure why but to get this to work I had to remove the following lines from `_config.yml`

```
github:
	repo: yourrepo
```

and replace it with
`repository: yourrepo`

I also have a Gemfile with the following code inside

```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

Gemfiles seem pretty typical in Jekyll projects but is not actually in the existing hyde project.

## Font Customization

I chose to change the font on hyde. I took font suggestions from [Typewolf](https://www.typewolf.com/google-fonts) using Google fonts as it is simple to implement.

After choosing a font you can click on `Google Fonts` underneath which will bring you to the fonts Google Font page. Clicking `Select This Font` at the top of the page will bring up a bar at the bottom which will contain the necessary HTML and CSS code.

Take the HTML code
(ex. `<link href="https://fonts.googleapis.com/css?family=Rubik" rel="stylesheet">`)
and paste that in `_includes/head.html` in the appropriate section under:

`<!-- CSS -->`

Then take the CSS:
(ex. `font-family: 'Rubik', sans-serif;`)
and paste that in `public/css/hyde.css` under:

```css
/* About section */
.sidebar-about h1 {
  color: #fff;
  margin-top: 0;
  font-family: 'Rubik', sans-serif;
  font-size: 2.5rem;
}
```

(I also changed the font-size here from 3.25rem to 2.5rem)
for the sidebar and

```css
/*
 * Global resets
 *
 * Update the foundational and global aspects of the page.
 */

html {
  /* font-family: "PT Sans", Helvetica, Arial, sans-serif;
	font-family: 'Playfair Display', serif;
	font-family: 'Cormorant Garamond', serif;
	font-family: 'Fira Sans', sans-serif; */
	font-family: 'Rubik', sans-serif; /* Changed font */
}
```

for the whole page

## Sidebar

#### Sidebar Theme

Hyde comes with 8 color options for the sidebar. To make my sidebar a little more unique, I took a gradient from http://uigradients.com/.

I chose "Between Night and Day" for my gradient. Appropriate CSS code can be copy and pasted from uigradients.

ex.

```css
background: #2c3e50; /* fallback for old browsers */
background: -webkit-linear-gradient(to left, #2c3e50 , #3498db); /* Chrome 10-25, Safari 5.1-6 */
background: linear-gradient(to left, #2c3e50 , #3498db); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
```

This code can be modified to specify which direction the gradient is going by changing the parameter in `linear-gradient`. For example changing `linear-gradient(to left, #2c3e50 , #3498db)` to `linear-gradient(30deg, #2c3e50 , #3498db)`.

In `public/css/hyde.css` you need to create the custom theme with the following code:

```css
/* Gradient */
/* Added new sidebar theme uigradients.com "Between Night and Day"*/
.theme-gradient .sidebar {
	background: #2c3e50; /* fallback for old browsers */
	background: -webkit-linear-gradient(30deg, #2c3e50 , #3498db); /* Chrome 10-25, Safari 5.1-6 */
	background: linear-gradient(30deg, #2c3e50 , #3498db); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}
.theme-gradient .content a,
.theme-gradient .related-posts li a:hover {
	color: #2c3e50;  /*Same as lefthand gradient from above*/
}
```

To apply the theme change `<body` to `<body class="theme-gradient">` in `_layouts/default.html`

#### Sidebar Width

I decreased the sidebar size in `public/css/hyde.css`:

```css
/*
 * Sidebar
 *
 * Flexible banner for housing site name, intro, and "footer" content. Starts
 * out above content in mobile and later moves to the side with wider viewports.
 */

.sidebar {
  text-align: center;
  padding: 2rem 1rem;
  color: rgba(255,255,255,.5);
  background-color: #202020;
}
@media (min-width: 48em) {
  .sidebar {
    position: fixed;
    top: 0;
    left: 0;
    bottom: 0;
    width: 16rem; /*width adjusted from 18rem*/
    text-align: left;
  }
}
```

#### Added personal image

I decided a picture of myself would be a nice touch and that there was enough free space in the sidebar to add one. I went for a round image as I thought it would look sharp in the rectangular sidebar.

I added this code to the bottom of `public/css/hyde.css`:

```css
/*
 * Image Cropper
 *
 *
 * Creates a rounded image
*/
.image-cropper {
    max-width: 200px; /*can be adjusted*/
    height: auto;
    position: relative;
    overflow: hidden;
}
.rounded {
    display: block;
    margin: 0 auto;
    height: 200px; /*can be adjusted*/
    width: 200px; /*can be adjusted*/
    -webkit-border-radius: 50%;
    -moz-border-radius: 50%;
    -ms-border-radius: 50%;
    -o-border-radius: 50%;
    border-radius: 50%;

    background:url(picture.jpg) center no-repeat;
    	background-size:cover;
}
```

`picture.jpg` is the image to be included and should be added to the `public/css` folder

To add the image to the sidebar, I edited the top of  `_includes/sidebar.html` to:

```html
<div class="sidebar">
  <div class="container sidebar-sticky">
		<div class="image-cropper">
    	<div class="rounded"></div>
		</div>
```

The height and width of the image as well as the length your description and the width of the sidebar can all be adjusted to get everything to fit in the sidebar.

#### Font Awesome

I changed the links at the bottom of the sidebar to be more suited towards me. I got rid of "Download" and "GitHub project"

In their place I added icons linking to various things.
I used [Font Awesome](http://fontawesome.io/get-started/) for the icons. Once you put your email into their site you will be emailed code to enter into `_includes/head.html` under `<!-- Icons -->`. (ex. <script src="https://use.fontawesome.com/someCode.js"></script>)

In `_includes/sidebar.html`, I commented out the links I didn't want and replaced it with the icons I did want:

```html
<!--<a class="sidebar-nav-item" href="https://github.com/AWiryaman">GitHub</a> --> <!--added link to github-->
<!--<a class="sidebar-nav-item" href="https://github.com/AWiryaman/AWiryaman.github.io">Website Repository</a>--> <!--added link to repository-->
<a href="https://github.com/AWiryaman"> <i class="fa fa-github fa-2x" aria-hidden="true"></i></a> <!-- github icon with link to github-->
<a href="mailto:anthonywiryaman@gmail.com">	<i class="fa fa-envelope-square fa-2x" aria-hidden="true"></i></a> <!--email icon with link to send email-->
<a href="https://www.linkedin.com/in/anthonywiryaman"> <i class="fa fa-linkedin-square fa-2x" aria-hidden="true"></i></a> <!--linkedin icon with link-->
<!--<span class="sidebar-nav-item">Currently v{{ site.version }}</span>-->
```


## Favicon

The Favicon is the icon that appears in the browser tab. To customize this you just need to change the `favicon.ico` file. I made a simple icon using [Squarespace's logo creator](https://logo.squarespace.com/). My logo is my initials inside a square using the colors from the gradient theme I chose.

## Custom domain

I got my custom domain through https://www.namecheap.com/ (use https://nc.me/ for a student discount). I purchased a couple domains (wiryaman.com, wiryaman.xyz and wiryaman.me) as the student discount made them relatively cheap. Unfortunately the domain I wanted (anthonyw.xyz) was already taken. Since all the domains were my last name, the obvious choice was to use a subdomain to make it anthony.wiryaman.

#### Making a subdomain
1. To make the subdomain go to the dashboard in namecheap
2. In the lefthand menu click on "Domain List"
3. Select your domain from the list and click "Manage"
4. From the menu at the top select "Advanced DNS"
5. Click "ADD NEW RECORD" under the existing Host Records
6. Choose "CNAME Record"
7. "Host" is the subdomain (ex. anthony)
8. "Target" is the domain (ex. wiryaman.com)
9. You can leave the TTL as automatic

#### Adding the custom domain to the website
In `CNAME` change the url to your custom domain
