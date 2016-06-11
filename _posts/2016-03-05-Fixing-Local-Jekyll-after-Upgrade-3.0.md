---
layout: post
title: Fixing Local Jekyll after Upgrade to 3.0
tags: [Article]
---

![jekyll-logo]({{ site.baseurl }}/images/jekyll-logo.png "jekyll-logo")

### Github Deprecating Redcarpet and Pygments

You Can see that in my repo commit:

-  [fix Markdown](https://github.com/nghenglim/nghenglim.github.io/commit/ccb334ecfeb2de31d295c687f9f21d7d0a9022ac)
-  [fix Highliger](https://github.com/nghenglim/nghenglim.github.io/commit/0ff9af854b7b9975bf243892664b1ddf62745a97)

And to have same jekyll version with Github Page my local has updated to Jekyll 3.0 with `gem update jekyll` too

### Upgrading to Jekyll 3.0 break local
Image of Fixed Local Jekyll:

![image breaked jekyll]({{ site.baseurl }}/images/2016030500.png "image breaked jekyll")

### All the Effort I Tried but Failed
- `conda install Pygments`
- `gem uninstall jekyll; gem install jekyll`

### Image of Fixed Local Jekyll
![image fixed jekyll]({{ site.baseurl }}/images/2016030501.png "image fixed jekyll")

### Solutions
After all the above failed, I think it might be due to markdown has changed, so I go to see the document of [kramdown](http://kramdown.gettalong.org/syntax.html#language-of-code-blocks).

Then I found out:

- \`\`\` using this as code block markdown is not supported in kramdown
- ~~~ this is the new supported code block markdown
