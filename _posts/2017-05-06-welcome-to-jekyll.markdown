---
layout: post
title:  "Welcome to Jekyll!"
date:   2017-05-06 11:03:10 -0300
categories: jekyll update
---
You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

If you don't want to publish right away, you can work with drafts. Drafts are posts without date, hence they dont have date in the post filename, nor in the head and are located in the `_drafts` directory. To be able to see drafts you should run `jekyll serve --drafts`.

To avoid "jekill serving" after every update use `jekyll serve -w` to watch and serve new changes, so for local editing you'd likely run `jekyll serve --drafts -w` :)

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

{% highlight java %}
// Dummy class
class Dummy{
  private var;
}
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
