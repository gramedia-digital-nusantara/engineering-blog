Intro to Pelican
================

:date: 2010-12-03 10:20
:category: Review
:authors: Derek J. Curtis

At GDN, we are more-or-less heavily a python shop.

This works-out well for most of our use-cases, as python
has great frameworks and libraries available for Ops, Backend
Development and Quality Assurance.

When we decided to begin with an engineering blog, a static-site
generator seemed to be almost a no-brainer alternative to something
like Wordpress, as it would be simple to maintain and our ops team
shouldn't have to worry much about the server dying.

In that space, Ruby is and has been king for quite a long time with
the extremely popular Jeckly (if you're looking for a similar kind of
project).

Requirements

* Needs to be relatively-easy for engineers to publish content
* Doesn't require any ops time to setup
* R


Common Popular Options
----------------------

Why not Wordpress?
^^^^^^^^^^^^^^^^^^

Wordpress has been around for a number of year (reference) and really does
great for a personal blog.  There are more plugins than one could ever
possibly need, and the process of editing content is extremely simple for
non-technical users.

Although nearly everyone has some familiarity with wordpress (both technical
users and non), if by happenstance you haven't heard of it, it's an
extremely popular blogging engine built on PHP and has a huge community 
and plugin ecosystem built around it.

For an engineering blog, our requirements are a bit different.

As this blog is being written and maintined by software engineers, working
with the content directly in a text editor (like VS Code) is not a concern.

For this project, there are some major downsides to Wordpress.

Mainly, I want to be able to run this blog with an absolute minmum
of operations time required


