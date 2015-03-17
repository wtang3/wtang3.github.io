---
layout: post
htmltitle: Fresh Start
title: Fresh Start ...
description: ""
modified: 
tags: [Jekyll, Google+, AngularJS]
image:
  feature: space-lol.jpg
  credit: fanpop
  creditlink: http://www.fanpop.com/clubs/space/images/34881513/title/space-lols-photo
comments: true
share: true
---

**tl;dr** My experience of building a working blog.

When I was building my blog I wanted to ensure that I had these use cases while being on a budget (I didn't feel the need to spend money).

1. Shall modify the views or appearance of your page when stuff gets boring.
2. Shall display data without the use of a database.
3. Shall be able to update my stuff without modifying the html files.
4. Shall not spend money, because I don't want to spend any.

With that being said, I tried a couple services, 

* <a href="https://cloud.google.com/appengine/?utm_source=google&utm_medium=cpc&utm_campaign=2015-q1-cloud-northam-us-gae-bkws-freetrial-en&gclid=CKaRo8eMqsQCFe7m7Aod0XAABw" target="_blank">Google App Engine</a>
* <a href="https://www.heroku.com/" target="_blank">Heroku</a>

### Google Appengine
What is Google App Engine, for those of you wanting to know if you decide to use this as a service. Google App Engine, aka GAE is a PaaS cloud computing platform and so is any other service you decide to use if you want to host your content on the cloud. The platform has many flavors such as Python, Java, PHP, and GO with the latter two being in beta for now. For my situation at the time my appetite was geared towards PHP, which later became a problem for the particular feature called blade in Laravel.

<img style="display: block; margin-left: auto; margin-right: auto" alt="credit to imagenes google" title="credit to imagenes google" src="http://imagenes.es.sftcdn.net/es/scrn/70000/70210/google-app-engine-3.jpg"/>

Okay back to the story, the cool thing about GAE is that it's free to a certain extent, you are able to host your app through your google account as long as you do not have too many requests, and if you do you're charged a fee with warning of course. Your web app will look like "1-dot-myapp.appspot.com", not a pretty name, but who cares. Moreover since its free this passes my use case numero quatro. Use case 1, since I'm writing the web pages I assume I can modify my stylesheets then push the changes, pass. Displaying my data without the use of a database, well hmm that seems easy why don't I just dump my data into a text file and read it or just have it in the html file. Use case 3, dum dum dum... so how can I do this, easy right just write to the files that I was reading from, well here is the down fall you cannot do any writes to the filesystem and neither on majority of the other PaaS vendors. So while I was still figuring out how to solve my last use case, I just worked on the pretty stuff and continued my research.

### Heroku
So I stumbled upon Heroku, which supports Ruby, Node.js, Python, Java, PHP. So the extra languages could come in handy if I decided to create a new project and I was able to get blade working. The url looked like appname.herokuapp.com which I though looked better than 1-dot-may app.appspot.com. Naturally I just moved over to Heroku. During the frontend phases, I realized that the downfall of Heroku is how they handle scaling. When your app is free from requests for more than 2 minutes (I believe that was the timeframe) your application will go in a dormant state, in other words the VM will shutdown and allocate its resources elsewhere. This was a turn off as requesting the site took a bit of time since it was getting ready to spin up the VM in the background. There are work around which you can poll your webpage, but it just didn't feel right for me to do that since they are offering a free service.


<img alt="credit to cdn.tutsplus" title="credit to cdn.tutsplus" src="https://cdn.tutsplus.com/net/uploads/legacy/2145_appfogheroku/Pic2.png"/>

### Google+
How am I going to solve this problem of being able to update my post? At first I was on a website where they had displayed their latest twitter feeds, so I'm thinking hmm this might be a good idea. Why don't I just use twitters api and just display my feeds on my app. This is a good solution, but the limitation of 140 characters did not help. So I decided why not try google+, their limit is 100,000 characters I think that should be enough? So I did some digging around in the <a href="https://developers.google.com/+/api/" target="_blank">google+ api</a>. So voila you can do some gets to this 

http://googleapis.com/plus/v1/people/**[google+ id]**/activities/public?key=[**public key from google**]

And you might get something like this

{% highlight javascript%}
 {
   "kind": "plus#activity",
   "etag": "\"RqKWnRU4WW46-6W3rWhLR9iFZQM/HhXAOsReZ7RsWx2cW4JHkrAplYs\"",
   "title": "fun read on #hacking \n\nhttp://spritesmods.com/?art=hddhack",
   "published": "2015-02-19T02:25:29.291Z",
   "updated": "2015-02-19T02:25:29.291Z",
   "id": "z13fhnw4rszrvzp3f23bvxyq5xveftbfx",
   "url": "https://plus.google.com/+yourid/posts/K1SRScshfcH",
   "actor": {
    "id": "117902654629859382535",
    "displayName": "blah blah",
    "url": "https://plus.google.com/????",
    "image": {
     "url": "https://lh3.googleusercontent.com/-t4xf095UQSQ/AAAAAAAAAAI/AAAAAAAAAH0/6zjdew-hlS0/photo.jpg?sz=50"
    }
   },
  ...
  ..
{% endhighlight %}

So what I did was grab the information I needed by looping through the objects and displayed it on the app. The flavors I used was PHP Laravel, and Angular JS.  This was cool and all, but I like change plus it did not have the blog feel, which brought me to using Jekyll, with the HPSTR theme and github pages.

### Github pages
So what is Jekyll? Jekyll is an open source program, written in Ruby by Tom Preston-Werner, GitHub's co-founder. It is a simple, blog-aware, static site generator for personal, project, or organization sites.
With that being said, you organize your folder structure similar to this

{% highlight text %}
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _data
|   └── members.yml
├── _site
└── index.html

{% endhighlight%}

then you just run jekyll server --watch and it will build your page into _site and serve it at localhost:4000 for testing. Once you are ready to host it on github, you create a new repo and push your project to it. And thats it! ~voila

### In Conclusion

Overall the I believe that if you place some constraints on your projects, it allows you to be creative to think outside the box to get to your goal. Sometimes it might take a while, but eventually you will solve the problem. Don't be afraid to refactor and build from scratch again, because each time you do I feel like you can learn something new. I know I did. Persistence is the key to success.

