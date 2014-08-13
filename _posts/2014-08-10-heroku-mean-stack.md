---
layout: post
title: Deploying the MEAN stack to Heroku.
summary: Getting an application running in Heroku is dead easy and their docs are great. I ran into a few minor issues with my MEAN application configuration that I'd like to cover here.
---

The MongoHQ and MongoLabs add ons are free but they do require [account verification](https://devcenter.heroku.com/articles/account-verification) which means inputing a credit card.  I used a Visa gift card to get past the validation process.

Below are the commands I used to load my app.

```bash
git clone git://github.com/myrepo/my-app.git
cd my-app
heroku create my-app
heroku addons:add mongohq 
git subtree push --prefix dist heroku master
heroku open
```

# Issue 1 : The Express listen port
This was something even my meager mind anticipated. My server code was simply opening a port with a hard coded value. The solution is simple enough, Heroku will put the PORT number in an environment variable.

```javascript
// -- original
var express = require('express');
var app = express();
app.listen(3030);

// -- updated
var app = express();
var server = require('http').createServer(app)
var port = Number(process.env.PORT || 3030);
server.listen(port);
```

# Issue 2 : Mongo connection URL
I'm using [Mongoose](http://mongoosejs.com/) and my app was simply pointing to a localhost instance of Mongo and was not configurable. I certainly didn't imagine this would work without a change, but the fix is easy. Heroku stuffs the Mongo connect URL into the environment for you. 

```javascript	
var mongoURL = process.env.MONGOHQ_URL || "mongodb://localhost";
mongoose.connect(mongoURL);
```

# Issue 3 : The 'dist' directory server
I'm using a `yeoman` style build that minifies/uglifies JS resources and places the resulting app into a dist directory. To only push the dist folder into into Heroku you can execute the command below rather than the standard push command shown in the Heroku examples. 

```bash
git subtree push --prefix dist heroku master
```

# Disclaimer
The [Heroku quick start](https://devcenter.heroku.com/articles/quickstart) guide is great and most of the information in this post can be found under the [Node](https://devcenter.heroku.com/tags/node) section. I was moving an existing application into Heroku so I of course tried to upload it unchanged to see what would happen. As I searched for answers I found them all in the Heroku docs. I just feel compelled to document the effort because it was so fun.

