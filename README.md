# Responsive HTML Email Toolset

> Sass based responsive email framework and CSS style inliner with great email client compatibility<br>
> A toolset for frontend developers, which provides a framework independent css style inliner, and a fine-tuned version of the great [Sassy Ink](https://github.com/faustgertz/sassy-ink) fork from [@faustgertz](https://github.com/faustgertz), based on [Foundation for Emails (formerly Ink)](http://foundation.zurb.com/emails.html).

## Features

The project has a `gulpfile.js`, which contains tasks for compiling the css file from an advanced [Sassy Ink](https://github.com/faustgertz/sassy-ink) version, and for moving the css styles inline in the provided html email templates.<br>
The inliner is completely independent from the Ink framework, which means that it works with any html email template.

The compiled html files are optimized to work in every email client, for example it capitalizes the `Margin` and `Float` styles so [they will work on outlook.com](https://www.emailonacid.com/blog/article/email-development/outlook.com-does-support-margins).

## HTML email best practices

To achieve the best possible email client support, you need to know about some surprising pitfalls in some email clients out there. There is a great [CSS Support Guide on Campaign Monitor's website](https://www.campaignmonitor.com/css/).
I stress out that `padding` is not supported on `<p>`, `<div>` and `<a>` tags, and `width` is not supported on `<p>` and `<div>` elements.

If you avoid those pitfalls, then you can achieve pretty great compatibility.

## Changes in Ink compared to the original version

Ink's original documentation at [http://zurb.com/ink/docs.php](http://zurb.com/ink/docs.php) is applicable in most parts.

### Prefer block-grid instead of grid

The main difference is that the grid columns are reduced to only two by default, as they does not play well with Gmail which has no support for media queries, so it shows all the columns in one row even on very small screens.

That's why it is reduced to only two columns, so it is only good for having support to use a left aligned section and a right aligned section in the same row.

In every other use cases it is recommended to use the block-grid syntax instead, which is responsive even on Gmail.

### Removed the buttons

Ink's button styles are not user friendly as they look as a button, but only the text is clickable, not the whole "button", which can confuse the readers.

The recommended way is to use Campaign Monitor's [Bulletproof email buttons](http://buttons.cm/) generator, which generates two different button versions, which works great in every email client.

### Added alignment helper classes

Added the following new helper classes:

- `text-left`: left aligning the text
- `text-right`: right aligning the text
- `centered`: that one is not for text, it is centering the block level elements (for text, you can use Ink's built-in `center` class)

## Customizing Ink with sass

> You can compile the default ink.scss file without doing any modifications.

If you want to customize the sass files, then you need to create a new `_settings.scss` file inside the `scss/ink/` folder, based on `_settings-default.scss`, which is there only for reference. That file contains all the variables that can be customized, just find those you need, uncomment them and change their value.

## Compiling the production ready HTML email

For the best possible compatibility, HTML emails need to utilize inline styles instead of the style header.

This project contains a gulp file with tasks to do that automatically.

### How gulp works

If you are not familiar with Gulp, give it a try, it is fairly easy to setup and can greatly boost your productivity.

1. You need to install node.js, which you can obtain at [https://nodejs.org](https://nodejs.org).<br>
2. Then run `npm install` from the command line in the project's root folder, which will install all the required node modules.<br>
3. After that, you can compile both the sass files and the html templates by running `gulp` from the command line in the project root.

### Available gulp tasks

- `gulp compile-ink`: compiles the default ink styles to `/css/ink.css`
- `gulp compile-custom-ink`: compiles the customized ink styles to `/css/ink-custom.css`, based on the customized `_settings.scss` file, which must be created based on the provided `_settings-default.scss` file
- `gulp inline-styles`: moving the style declarations to inline styles in all the `.html` files in the `templates-src` folder, written into the `templates-dist` folder
- `gulp default`: runs the `compile-ink` and `inline-styles` tasks

## Compatibility

The compiled html template will have the best possible email client compatibility, tested on an Ink based template with [Litmus](https://litmus.com/) on a layout that utilizes the two column grid and three columns of the block-grid.

### Tested with Litmus on the following clients

#### Mobile browsers

- Android 4.4
- Gmail App on Android
- iPad Retina
- iPad Mini
- iPhone 5s iOS 7
- iPhone 5s iOS 8
- iPhone 6
- iPhone 6 Plus
- iPhone 6s
- iPhone 6s Plus

#### Desktop browsers - Mac

- Apple Mail 7
- Apple Mail 8
- Outlook 2011
- Outlook 2016

#### Desktop browsers - Windows

- Lotus Notes 8.5
- Outlook 2000
- Outlook 2002
- Outlook 2003
- Outlook 2007
- Outlook 2010
- Outlook 2013
- Outlook 2013 120 DPI
- Plain Text
- Thunderbird 38

#### Web mail

- AOL Mail (Chrome, Explorer, Firefox)
- Gmail (Chrome, Explorer, Firefox)
- Google Apps (Chrome, Explorer, Firefox)
- Office 365 (Chrome)
- Outlook.com (Chrome, Explorer, Firefox)
- Yahoo! Mail (Explorer, Firefox)

## Credit

* [István Ujj-Mészáros](https://github.com/istvan-ujjmeszaros), the maintainer of this toolset
* [Faust Gertz](https://github.com/faustgertz), who created the Sass version of the Ink framework
* [ZURB](http://www.zurb.com), who created Foundation for Emails (formerly Ink), probably the best freely available responsive email framework
* [René Meye](https://github.com/renemeye)'s [pull request #61](https://github.com/zurb/ink/pull/61) for Ink
