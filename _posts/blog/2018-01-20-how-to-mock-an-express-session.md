---
layout: post
title: How to mock an Express session?
excerpt: "Mock session object in Nodejs unit test-cases."
modified: 2018-01-20T15:15:25+05:00
categories: blog
tags: [expressjs,nodejs,mocha,cookies,cookie-session,crypto,javascript]
author: waleed_ashraf
image:
  feature: cover_arch.jpg
  credit: thomashawk
  creditlink: http://thomashawk.com/
comments: true
share: true
---

[sinon](http://sinonjs.org/) is used to mock methods with unit tests frameworks (like [mocha](https://mochajs.org/)). It is one of the most popular packages used for JavaScript testing. But is there a way to mock session objects in tests for [Express](https://expressjs.com/)?

I’m working on a project where I upload images to s3 in bulk (albums) and then apply some processing like resizing/compression/editing on them.

It’s an [Express](https://expressjs.com/) app with middleware for authorization, authentication, setting context and is working fine. Recently, however I started adding test cases for different routes using [mocha](https://mochajs.org/). I’m using [cookie-session](https://www.npmjs.com/package/cookie-session) for session handling in app. Which means [cookie-session](https://www.npmjs.com/package/cookie-session) is responsible for encrypting/setting/decrypting all session related data.

I have two routes, one is to upload the photo to s3 (create) and the second one (submit) to apply further processing on uploaded images. For one route, I needed to mock `req.session` object. I needed to set its value before calling the other route. First route (create) set `req.session` value and redirect to second one (submit).

### 1) api/image/create

```
exports.create = function(req, res) {
    // upload image to s3
    // and add entries in database
    var photos = PhotosTable.create(req.files.names);
    req.session.count = photos.length; // set count in req.session
    res.redirect('api/image/submit');
}
```
### 2) api/image/submit (need to add test case for this one)
```
exports.submit = function(req, res) {
    // get count from req.session
    if (req.session.count && req.session.count > 0) {
        // perform further tasks
        res.sendStatus(200); 
    } else {
        res.sendStatus(400); 
    }
}
```
### I just want to test second route (api/image/submit).
The issue is that api/image/submit route checks for `req.session.count` and than perform further tasks. If the count is not set, it sends 400 in response. With mocha you can only check response from one route, you can’t wait for the result from redirect call.

One easy solution to fix this issue is to send a req-param from the test case, and check it in method if that param is present, then skip checking for `req.session.count`.
However, this solution isn’t the best because:
- It can’t be reused as it’s not a generic solution.
- Adding if/else for extra parameter in controller logic will require more checks to verify that controller logic is not effected.

I could also easily get rid of the second route and add all logic in one. But should I? As far as I know, 

> one should never change implementation for the sake of test cases.

This problem seems so common but I couldn’t find any solution on the internet (or at least StackOverflow). My first guess was that there would be some npm-package to handle this kind of situation. As mocha, cookie-session are the most used modules with [Express](https://expressjs.com/).

Alas! There isn’t any.

### I’m using cookie-session with Express to maintain sessions:
[cookie-session](https://www.npmjs.com/package/cookie-session) maintains the session by keeping signed cookies. It uses [cookies](https://www.npmjs.com/package/cookies) with [Keygrip](https://www.npmjs.com/package/keygrip) and [crypto](https://www.npmjs.com/package/crypto) to set and validate session keys.
It requires a name and a key for setting session cookies. 
name is used as cookie name. 
key is used to sign cookie value using Keygrip.
So, somehow I should set `req.session.count` value in the test case, before calling the route.
```
// name = “my-session” -> base64 value of required object (cookie)
// name.sig = “my-session.sig” -> signed value of cookie using Keygrip

let cookie = Buffer.from(JSON.stringify({“count”:2}))
            .toString(‘base64’);
             
let kg = Keygrip([‘testKey’]); // same key as I’m using in my app
let hash = kg.sign(‘my-session=’ + cookie);

await request(app).get(‘api/image/submit’)
                  .set(“Accept”, “text/html”)
                  .set(‘cookie’, [‘my-session=’ + cookie + ‘; ‘ +
                  ‘my-session.sig=’ + hash + ‘;’])
                  .expect(200);
```
That’s it. By setting this cookie in request, I was able to set `req.session.count` to my desired value. Hah!! xD
```
exports.submit = function(req, res) { 
    if(req.session.count && req.session.count > 0) { // true 
    // ..... perform some tasks
    res.sendStatus(200); 
    }
}
```
This is just one use case for mocking session in [Express](https://expressjs.com/). Most of the time unit tests require customized values for assertion but it can be used wherever you need to set `req.session` with any specific value.
I have also created package at npm, 

**mock-session**: [https://www.npmjs.com/package/mock-session](https://www.npmjs.com/package/mock-session)