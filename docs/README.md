DocsHub allows you to write your docs in markdown and render them in a clean, simple interface

## Setup

The DocsHub entry point is just a simple html file that looks like this:

<?codeblock external="index.html" lang="html"></codeblock?>

Here you configure the path to your JSON config file by changing `window.docsConfigSrc`. The default is `docs/config.json`.

### Config JSON

Inside the config file we configure some globals - the logo, the brand colour, the project name and version and the menu. A config file would look something like this:

<?codeblock external="config.json" lang="json"></codeblock?>

### Page types

You'll see in the config that each page has a source. The source is in the format `{type}/{file-path}`

There are 5 page types:

1. `page` - markdown or html pages - these pages are treated as content. We have some special syntax for embedding code widgets in your docs which is described below.
2. `dashboard` - a dashboard page is a composable page type made up of different sections configured in a JSON file.
3. `iframe` - iframe that fills up the content area
4. `remotepage` - remote version of page
5. `remotedashboard` - remote version of dashboard
6. `remoteiframe` - remote version of iframe

So if I have a readme page at `docs/README.md` the url would be `page/docs/README.md` - this is case insensitive

For 'remote' sources the file-path would be the full URL path without the protocol - e.g `remotepage/raw.githubusercontent.com/bluegrassdigital/blue-js/master/README.md`

#### page

A page is just html or markdown.

Pages support YML Front matter configuration. Currently the only variable that will be used is `name` which will be used in the header (if not set then the name from the menu is used, and if there is no menu item then there will be no page name)

#### dashboard

A dashboard page is a composable page made up of an array of sections. Each section can have one or more of a `title`, `subtitle`, `downloads`, `pages` and `markdown` section. An example is below:

```json
[
  {
    "title": "Downloads",
    "subtitle": "Version 1.1.0",
    "downloads": [
      {
        "platform": "apple",
        "url": "manifest.plist",
        "text": "Download for iOS"
      },
      {
        "platform": "android",
        "url": "app.apk",
        "text": "Download for Android"
      },
      {
        "platform": "windows",
        "url": "app.msi",
        "text": "Download for Windows"
      },
      {
        "platform": "linux",
        "url": "app.msi",
        "text": "Download for Linux"
      },
      {
        "platform": "file-archive-o",
        "url": "app.msi",
        "text": "Download zip"
      },
      {
        "platform": "cloud-download",
        "url": "app.msi",
        "text": "Download file"
      },
      {
        "platform": "file-pdf-o",
        "url": "app.msi",
        "text": "Download PDF"
      }
    ]
  },
  {
    "subtitle": "Version 1.0.0",
    "downloads": [
      {
        "platform": "apple",
        "url": "manifest.plist",
        "text": "Download for iOS"
      },
      {
        "platform": "android",
        "url": "app.apk",
        "text": "Download for Android (x64)"
      },
      {
        "platform": "android",
        "url": "app.apk",
        "text": "Download for Android (x86)"
      },
      {
        "platform": "windows",
        "url": "app.msi",
        "text": "Download for Windows"
      },
      {
        "platform": "linux",
        "url": "app.msi",
        "text": "Download for Linux"
      }
    ]
  },
  {
    "markdown": "docs/CHANGELOG.md"
  }
]
```
