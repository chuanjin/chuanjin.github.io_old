title: "JS runtime in Rails"
date: 2015-04-22 21:29:06
tags: Rails
categories: R&D
---

When we develop rails apps, we usually need JavaScript runtime. On Mac OS X and Windows a JavaScript runtime is already installed in the operating system. For Linux, we usually install node.js, because it  uses the Google V8 JavaScript engine, which is super fast.

{% blockquote %}

It's worth noting, that processing JavaScript (without executing it) would not principally require a JavaScript runtime. The reason why the Rails asset pipeline needs a JavaScript runtime is that it does the processing with tools like CoffeeScript and uglifier that themselves are implemented in JavaScript and which thus require a runtime to be used.

{% endblockquote %}

reference: 
http://stackoverflow.com/questions/9673081/why-does-rails-require-javascript-runtime
http://guides.rubyonrails.org/asset_pipeline.html#javascript-compression