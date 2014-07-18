---
layout: post
title: Blogging with GitHub Pages, Jekyll and Poole
---

As my first post I have to give props to everyone at GitHub for creating [GitHub Pages](https://pages.github.com/) which makes a hosting a blog or project site ridiculously easy. Especially if you're already a GitHub user. 

I wont bother typing everything you can already find on the [GitHub Pages](https://pages.github.com/) site, but the gist of it is the following

<p class="message">
... create a new (GitHub) repository named username.github.io, where username is your username (or organization name) on GitHub.
</p>

Once you do that the URL `username.github.io` will be accessible with your repository content as the doc-root. It will take a few minutes for the initial creation, but after that it's as simple as committing the content of your site to the new repository.

<p class="message">
One of my first questions was "Can I just create anysiteiwant.github.io"

Nope. It has to exactly match your username.
</p>

Anyway... on to the really interesting stuff. It turns out [GitHub Pages](https://pages.github.com/) supports
[Jekyll](http://jekyllrb.com/) which is 
`...a simple, blog-aware static site generator...` 

There is a wonderful explanation about [Using Jekyll with GitHub Pages](https://help.github.com/articles/using-jekyll-with-pages) on the GitHub site already, so again the gist is the following 

<p class="message">
Every GitHub Page is run through Jekyll when you push content... Because a normal HTML site is also a valid Jekyll site, you don't have to do anything special to keep your standard HTML files unchanged...
</p>

The next thing you'll want is a nice theme for your blog or project site. [JekyllThemes](http://jekyllthemes.org/) has quite a few but I landed on using 
[Poole's](http://getpoole.com/)
Hyde theme. As you'll see, this site is essentially 100% Hyde. I'm trying not to lose focus on my goal of getting my first blog up and running - so I'll tinker with layouts and navigation later <-:

The last thing I will mention is [prose.io](http://prose.io). It is a web-based, Jekyll/Markdown aware editor that links to your GitHub repo. You can basically create your post in `prose.io` and it will push it into GitHub. I have not tried it out yet but it looks interesting. 

Well there you go, my first post (hello world).