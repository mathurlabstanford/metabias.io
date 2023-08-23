- [Website Configuration](#website-configuration)
  - [Global settings](#global-settings)
  - [Adding a new page](#adding-a-new-page)
  - [Adding new page for a Shiny app](#adding-new-page-for-a-shiny-app)
  - [Website deployment](#website-deployment)
  - [Custom domains](#custom-domains)
  - [Editing the outer UI of the website](#editing-the-outer-ui-of-the-website)
- [Local development with jekyll](#local-development-with-jekyll)

Based on the [Minimal Mistakes Jekyll theme](https://mmistakes.github.io/minimal-mistakes/)
under an MIT license.

## Website Configuration

### Global settings

See full [config](https://mmistakes.github.io/minimal-mistakes/docs/configuration/).
The following are the most important places where you need to make changes
(see comments in these files also): 

- edit `_config.yml` to update site metadata
  - most important settings (site title, name, url) are highlighted at the top, 
  - you can add Google Analytics tracking ID
- edit `_data/navigation.yml` to add more tabs to the top navigation: title and url (relative to site url)
- edit `assets/css/main.scss` to change customized colors and fonts.

```yaml
# main links in _data/navigation.yml
main:
  - title: "Publication bias"
    url: /pubbias/
  - title: "p-hacking"
    url: /phacking/
```

### Adding a new page

Open the `site.Rproj` file in RStudio IDE.
Open Rmd files you'd like to edit. Click render.
Jekyll will ignore Rmd, and will deploy html based on the md files.

Adding a new page under `metabias.io/path/dir/`:

1. create folder `path/dir`
2. add `index.Rmd` into the folder (see below for what goes into the header)
3. Edit Rmd then render the md

This is the part that goes into the Rmd header of the file `path/dir/index.Rmd`:

```yaml
---
title: Add your title here
layout: archive
output:
  md_document:
    variant: gfm
    preserve_yaml: true
---
```

Keeping the `layout` and `output` is important, so that it will show up as expected after Jekyll renders the pages.

Note: if images are included as part of the Rmd, those will be placed
relative to the `index.Rmd` file and need to be added to git.

See [this](https://rstudio.com/wp-content/uploads/2016/03/rmarkdown-cheatsheet-2.0.pdf) cheat sheet for markdown formatting.

### Adding new page for a Shiny app

Here is how you can add a page for Shiny apps that are already deployed (see the [metabias-apps repo](https://github.com/mathurlabstanford/metabias-apps) for information on how to structure and deploy them).

Create new folder in the root, e.g. `my-app` and add an `my-app/index.md` file
with the following content: change the app url

```yaml
---
layout: app
app_url: https://qsu-stanford.shinyapps.io/my-app/
---
```

This will indicate to the Jekyll template to use the `app` layout (which puts the iframe around the app URL). The `app_url` is the link that will show up in the iframe.

If the website is served over https, the iframe needs to be https as well.

### Website deployment

GitHub pages use Jekyll, so no additional steps are required.
Commit changes and it is done. Make sure you go to the Settings tab
of the repo and set GitHub pages deployment from the root folder of
the master/main branch.

### Custom domains

Set up a www subdomain (e.g. `www.new-domain.com`) following [this](https://docs.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site) guide.

1. Go to the Settings tab of the repo, scroll down to the GitHub Pages section
2. Add `www.new-domain.com` to the Custom Domain field and click Save
3. Go to your DNS settings on your provider's page (see [here](https://support.google.com/domains/answer/9211383?hl=en))
  - In the first field, enter `www` or the required subdomain
  - In the dropdown menu, select CNAME
  - In the TTL field, enter 1H
  - In the data field, enter `mathurlabstanford.github.io`
  - Click Add

### Editing the outer UI of the website

To edit the outer framework exclusive of the Shiny app iframe itself (e.g., the Resources tab), just edit and knit the relevant .Rmd file, commit as normal (with no special message), and push. Remember you need to knit the .Rmd file or else the changes will not be reflected in the .md file, which is what the website ultimately uses.

- Changing font sizes: Edit per comments in `assests/css/main.scss`.
- Changing width of text on page (i.e., change whitespace on either side of text column): Edit per comments in `_sass/minimal_mistakes/_archive.scss`.

Note: We are using the "archive" layout (`_sass/minimal_mistakes/_archive.scss`), so if you want to change a parameter that is normally in `_page.scss`, you should change it in `_archive.scss` instead.

## Local development with jekyll

### One-time steps to set up jekyll locally

Install jekyll (one time setup inside the directory): skip steps as appropriate, e.g. if you have Ruby installed etc (`ruby -v` should return Ruby version).
See more about Ruby and Jekyll installation [here](https://jekyllrb.com/docs/installation/).

This will install jekyll to `evalue_website/vendor`. Important: To avoid errors in `bundle install`, the entire file path to ruby (which will be in `evalue_website/vendor`) needs to not have spaces in the directory names. Change them to underscores before the installation.

```bash
# Install Command Line Tools
xcode-select --install

# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Ruby
brew install ruby

# Add the brew ruby path to your shell configuration:
PATH="`ruby -e 'puts Gem.user_dir'`/bin:$PATH"

# Install Jekyll
gem install --user-install bundler jekyll

# Install gems (dependencies) for the template
bundle install
```

When you edit your files and want to check locally how the site looks, first make sure you are in the top-level directory `evalue_website` (where the jekyll files live) and then use this:

```bash
bundle exec jekyll serve
```

This will build the site that you can check at `http://127.0.0.1:4000` in
your browser. When you change the source it render the changes
but you have to click refresh in the browser to see the changes.
Stop the server with Ctrl+C in the command line.
