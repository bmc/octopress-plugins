# Octopress Plugins

This repository contains some plugins for the [Octopress][] blogging engine.

# Image Popup Plugin

Provides a tag that generates a thumbnail of an image which, when clicked,
generates a popup containing the full size image.

See [A Simple Octopress Image Popup Plugin][blog-image-popup] for a discussion,
and demonstration, of this plugin.

## Installation

Add these lines to your blog's `Gemfile`:

    gem `erubis`
    gem `mini_magick`

`mini_magick`, in turn, requires that the Image Magick *mogrify*(1) command
be installed and in your path.

The gem also relies on both jQuery and jQuery UI. Add these lines to your
blog's `sources/_includes/custom/head.html` file:

    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js" type="text/javascript"></script>
    <script src="https://ajax.googleapis.com/ajax/libs/jqueryui/1.8.16/jquery-ui.min.js" type="text/javascript"></script>

Finally, copy `img_popup.rb` and `img_popup.html.erb` to your blog's
`plugins` directory.

## Usage

The plugin implements a [Liquid][] template tag. The tag syntax is
straighforward:

    {% imgpopup /path/to/image percent% [title] %}

The image path is relative to the source directory. The percent argument is the
amount to scale the image down for the clickable preview. The optional title is
put in the title bar of the modal popup. Here’s a real example:

    {% imgpopup /images/bigimage.png 50% My Big Image %}

---

# GitHub Plugin

The GitHub plugin embeds the contents of a *git* commit from a GitHub
repository directly into a blog post. It's similar, in concept, to the
stock Octopress [gist tag][], except that it pulls its content from a GitHub
repo, not from a Gist.

## Installation

Add the following to your blog's `Gemfile`:

    gem 'octokit' # Ruby GitHub API

Then, copy `github.rb` to your blog's `plugins` directory.

## Usage

    {% github user/repo filehash %}

To get a file's hash, run the following in a local copy of the repo:

    $ git hash-object path-to-file

If it's code, you might want to put it inside a codeblock.

Example:

    {% codeblock lang:ruby %}
      {% github bmc/octopress-plugins 4d1efaac98ff3f2c566497ebb6367627e3ab2597 %}
    {% endcodeblock %}

[blog-image-popup]: http://brizzled.clapper.org/blog/2012/02/05/a-simple-octopress-image-popup-plugin/
[Octopress]: http://octopress.org/
[Liquid]: https://github.com/Shopify/liquid
[gist tag]: http://octopress.org/docs/plugins/gist-tag/
