# This repo is now deprecated. Head over to https://github.com/iadvize/public-developers-documentation

# :memo: Documentation

This documentation is the technical documentation for iAdvize API and the Developer platform. This repository is used to store the source of [iAdvize Documentation](https://developers.iadvize.com/documentation). The iAdvize's Documentation is generated from the Documentation.md of this repository.

If you have questions about this documentation you can send an email to developers@iadvize.com.

## How to contribute

You have to create a branch and open a pull request, after that we will review it.

There is two way to do this, directly on github with the preview system on markdown files or in your computer with tools like [MacDown](https://macdown.uranusjr.com/) if you know how to use a git. After that We will review your pull request and decide when to publish it if it's needed.

You have to edit the file Documentation.md in a markdown format, if you don't know how to do this you can use [Mastering Markdown](https://guides.github.com/features/mastering-markdown/) to help you writing markdown.

For GraphQL API, you have to generate static documentation in connectors-app, see [README](https://github.com/iadvize/connectors-app#graphql-doc)
  
## How to test

You can test your branch with the route https://developers.iadvize.com/documentation in production by adding the preview header X-iAdvize-Preview containing the branch name you want to test.

You can check if the rendering is right and if the global documentation with the generating menu is not broken. We will do the same check before publishing it.

## Production

Your changes will be automatically avaible once we've merged it into the master branch.
