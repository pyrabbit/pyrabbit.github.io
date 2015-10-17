---
layout: post
title: Controller/Action Specific Javascript with Rails 4
---


I wanted to take the opportunity to share a solution I had for one of my grievences with the existing Rails asset pipeline. For multiple reasons, I absolutely despise how all my JavaScript is compiled into a single file. This isn't a blog post to argue the merits of the existing strategy used by Rails but provide a simple alternative.

However, I do want to touch on at least one reason why I dislike the current strategy and why I decided to implement this. The separation of code is strictly cosmetic and serves no purpose other than organization. Placing JavaScript code in one file conveniently named after one of your controllers can, if not programmatically prevented, be executed on all controllers/applications of your application. Additionally, it can easily mislead naive Rails developers into believing that the JavaScript in one file is executed on only the matching controller.

##My Solution
###Step 1) Remove `require_tree .` from `application.js`

`require_tree .` is a method that pulls all the JavaScript assets into `application.js`. I have decided to reserve `application.js`for requiring any global scripts that I may need.

###Step 2) Modify `application.html.erb` to include our controller/action specific .js files

```
<%= javascript_include_tag "#{controller_name}/#{action_name}" if AppName::Application.assets.find_asset("#{controller_name}/#{action_name}") %>
```

Using some of the methods that come readily available with ActionView, we are able to extract the name of the controller and action we are currently on. In the included example project, when you visit the `static_pages#hello` it will look for a javascript file in `app/assets/javascripts/static_pages/hello.js`. This technique allows us to use some type of convention over configuration with our applications JavaScript.

###Step 3) Add `config.assets.precompile += %w(*/*)` to `config/application.rb` so your assets are precompiled.

I hope this helped someone, if you have a method to improve or have valuabe input on why this wouldn't be a good solution, I would love to hear from you!

P.S. I appologize that the formatting in my post is kind of quirky. I have been meaning to update my design but haven't got around to it yet.

You can find my test code at  https://github.com/pyrabbit/sample-javascript-app.git
