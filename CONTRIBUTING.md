# Contributing guidelines

We're so glad you're thinking about contributing to a [open source project of the U.S. government](https://code.gov/)! If you're unsure about anything, just ask -- or submit the issue or pull request anyway. The worst that can happen is you'll be politely asked to change something. We love all friendly contributions.

We encourage you to read this project's CONTRIBUTING policy (you are here), its [LICENSE](LICENSE.md), and its [README](README.md).

## Policies

We want to ensure a welcoming environment for all of our projects. Our staff follow the [Code of Conduct](https://18f.gsa.gov/code-of-conduct/) and all contributors should do the same.

We adhere to the [18F Open Source Policy](https://github.com/18f/open-source-policy). If you have any questions about the policy, just [shoot 18F an email](mailto:18f@gsa.gov).

## Public domain

This project is in the public domain within the United States, and copyright and related rights in the work worldwide are waived through the [CC0 1.0 Universal public domain dedication](https://creativecommons.org/publicdomain/zero/1.0/).

All contributions to this project will be released under the CC0 dedication. By submitting a pull request or issue, you are agreeing to comply with this waiver of copyright interest.

## Development with Federalist + U.S. Web Design System + Jekyll

This [Jekyll theme](https://jekyllrb.com/docs/themes/) is developed using the [U.S. Web Design System v 2.0](https://v2.designsystem.digital.gov) and is focused on providing developers a starter kit and reference implementation for Federalist websites.

This code uses the [Jekyll](https://jekyllrb.com) site engine and built with Ruby. If you prefer to use Javascript, check out [federalist-uswds-gatsby](https://github.com/18F/federalist-uswds-gatsby), which uses [Gatsby](https://gatsbyjs.org) site engine.

This project strives to be compliant with requirements set by [21st Century IDEA Act](https://www.meritalk.com/articles/senate-passes-idea-act/). The standards require that a website or digital service:

- is accessible to individuals with disabilities;
- has a consistent appearance;
- does not duplicate any legacy websites (the legislation also requires agencies to ensure that legacy websites are regularly reviewed, removed, and consolidated);
- has a search function;
- uses an industry standard secure connection;
- “is designed around user needs with data-driven analysis influencing management and development decisions, using qualitative and quantitative data to determine user goals, needs, and behaviors, and continually test the website, web-based form, web-based application, or digital service to ensure that user needs are addressed;”
- allows for user customization; and
- is mobile-friendly.

## Key Functionality

This original repository commit contains the following examples and functionality:

✅  Publish blog posts, press releases, announcements, etc. To modify this code, check out `blog/index.html`, which manages how the posts are listed. You should then check out `_layouts/post.html` to see how individual posts are structured.

✅  Publish single one-off pages. Instead of creating lots of folders throughout the root directory, you should put single pages in `_pages` folder and change the `permalink` at the top of each page. Use sub-folders only when you really need to.

✅  Publish data (for example: job listings, links, references), you can use the template `_layouts/data.html`. Just create a file in you `_pages` folder with the following options:

```txt
---
title: Collections Page
layout: data
permalink: /collections
datafile: collections
---
```

The reference to `datafile` referers to the name of the file in `_data/collections.yml` and loops through the values. Feel free to modify this as needed.

✅  There are two different kinds of `pages`, one does not have a side bar navigation, and the other uses `_includes/sidenav.html`. You can enable this option by adding `sidenav: true` to your page front matter.

```txt
---
title: Document with Sidenav
layout: page
sidenav: true
permalink: /document-with-sidenav
---
```

✅ [Search.gov](https://search.gov) integration - Once you have registered and configured Search.gov for your site by following [these instructions](https://federalist.18f.gov/documentation/search/), add your "affiliate" and "access key" to `_config.yml`. Ex.

```yaml
searchgov:

  # You should not change this.
  endpoint: https://search.usa.gov

  # replace this with your search.gov account
  affiliate: federalist-uswds-example

  # replace with your access key
  access_key: xX1gtb2RcnLbIYkHAcB6IaTRr4ZfN-p16ofcyUebeko=

  # this renders the results within the page instead of sending to user to search.gov
  inline: true
```

The logic for using Search.gov can be found in `_includes/searchgov/form.html` and supports displaying the results inline or sending the user to Search.gov the view the results. This setting defaults to "inline" but can be changed by setting

```yaml
searchgov:
  inline: false
```

in `_config.yml`.

✅ [Digital Analytics Program (DAP)](https://digital.gov/services/dap/) integration - Once you have registered your site with DAP add your "agency" and optionally, `subagency` to `_config.yml` and uncomment the appropriate lines. Ex.

```yaml
dap:
  # agency: your-agency

  # Optional
  # subagency: your-subagency
```

✅ [Google Analytics](https://analytics.google.com/analytics/web/) integration - If you have a Google Analytics account to use, add your "ua" to `_config.yml` and uncomment the appropriate lines. Ex.

```yaml
ga:
  # ua: your-ua
```

## How to edit

- Non-developers should focus on editing markdown content in the `_posts` and `_pages` folder

- We try to keep configuration options to a minimum so you can easily change functionality. You should review `_config.yml` to see the options that are available to you. There are a few values on top that you **need** to change. They refer to the agency name and contact information. The rest of `_config.yml` has a range of more advanced options.

- The contents inside `assets/` folder store your Javascript, SCSS/CSS, images, and other media assets are managed by  [jekyll-assets](https://github.com/envygeeks/jekyll-assets).  Assets are combined, compressed, and automatically available in your theme

- If you look at `package.json` you will see that the `npm run federalist` command that will run when running on the Federalist platform.

- Do not edit files in the `_site/` folder. These files are auto-generated, and any change you make in the folder will be overwritten.

- To edit the look and feel of the site, you need to edit files in `_includes/` folder, which render key components, like the menu, side navigation, and logos.

- `index.html` may not require much editing, depending on how you customize `hero.html` and `highlights.html`.

- `_layouts/` may require the least amount of editing of all the files since they are primarily responsible for printing the content.

- `blog/index.html` can be edited, but be careful. It will impact the pagination system for the posts. If you do edit the file, be prepared to edit `_config.yml`.  For example, you may need go change configurations for [jekyll-paginate-v2](https://github.com/sverrirs/jekyll-paginate-v2)

- `search/index.html` is used by search.gov.

## Running the application locally with `node` and `ruby`

```bash
npm install
bundle install
npm start 
    OR
bundle exec jekyll serve
```

To build but not serve the site, run `npm run build` or `bundle exec jekyll build`.

### Running the application locally with Docker

```bash
docker-compose run node npm install
docker-compose build
docker-compose up
```

To build but not serve the site, run:

```bash
docker-compose run ruby bundle exec jekyll build
```

Note that when built by Federalist, `npm run federalist` is used instead of
`npm run build`.  Open your web browser to [localhost:4000](http://localhost:4000/) to view your
site.

## Testing with locally installed `node` and `ruby`

```bash
npm test
    OR
bundle exec htmlproofer _site; npx a11y '_site/**/*.html'
```

### Testing with Docker

```bash
docker-compose run ruby bundle exec htmlproofer _site; npx a11y '_site/**/*.html'
```

## Technologies you should be familiarize yourself with

- [Jekyll](https://jekyllrb.com/docs/) - The primary site engine that builds your code and content.
- [Front Matter](https://jekyllrb.com/docs/frontmatter) - The top of each page/post includes keywords within `--` tags. This is meta data that helps Jekyll build the site, but you can also use it to pass custom variables.
- [U.S. Web Design System v 2.0](https://v2.designsystem.digital.gov)

## One-time local setup for Mac users

This is the "advanced" setup option for developers who want to host the Jekyll site natively in Node instead of Docker containers.  It will require local admin privileges.

### Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Note: you may need to supply your Mac password several times as this runs to verify local Admin actions.

### Git, Node, Npm

```bash
brew install git
brew install node
brew install npm
```

First time setup for Git:

```bash
git config --global user.name "John Doe"
git config --global user.email johndoe@gsa.gov
git config --global pull.rebase true
```

### Chruby and Ruby-Install

```bash
brew install chruby ruby-install
```

### Ruby

```bash
ruby-install ruby 2.6.6
```

After Ruby is installed, add these 2 lines on ~/.bash_profile. If you're using ZSH as your shell, add these to ~/.zshrc.

```txt
source /usr/local/opt/chruby/share/chruby/chruby.sh
source /usr/local/opt/chruby/share/chruby/auto.sh
```

To get to the editor of .zshrc:

1. Right-click on Finder and select “Go to Folder” or `Ctrl+Shift+G` if already open, then type in `~`
2. `Cmd+Shift+.` to show hidden files
3. Double click on `.zshrc`

To use a specific version of Ruby:

```bash
chruby 2.6.6
```

#### Troubleshooting Ruby

You may need to install xcode files before installing Jekyll or Ruby, but probably not

```bash
xcode-select --install
```

If you have a `brew` installed version of Ruby in your path, it may conflict with a `ruby-install` version.

```bash
brew uninstall ruby
```

Also remove references to the `/usr/local/ruby` paths in `.zshrc` file.

### Jekyll

```bash
gem install --user-install bundler jekyll
```

### Local repo setup

To make a local copy of the repository, where you will work until you’re ready to share and merge:

1. Create /Users/(yourusername)/Repos folder + add to Favorites (drag to Favorites)
2. Fork the repo from the GitHub page (skip this step if you are not using the Fork method)
3. Copy Clone information from the GitHub repo
4. We’ll clone from Terminal in VS Code setup, which will auto-set your access token

### Setup Visual Studio Code

1. Install Visual Studio Code from GSA Server Service app
2. Shift+Cmd+P, then >`View: Toggle Integrated Terminal` and then `cd Repos` at the terminal prompt
3. Clone the repo:

  ```bash
  #if forked:
  git clone https://github.com/(username)/SaferFederalWorkforce.gov.git

  # if direct:
  git clone https://github.com/GSA/SaferFederalWorkforce.gov.git

  # enter GitHub credentials if prompted
  ```

### Create first Git feature branch

Some helpful Git commands

- `git status` will show you what branch you are currently on
- `git branch` will show you what branches are available on local copy of repo
- `git branch -r` will show you what branches are available on remote copy of repo

Create new branch from current branch and checkout for editing:

```bash
git checkout -b my-feature-branch
```

You can now edit that branch as needed.  See online help for more information about committing changes in Visual Studio Code and with Git command line.  This blog article is helpful for newbies:
[Making your first GitHub contribution](https://codeburst.io/a-step-by-step-guide-to-making-your-first-github-contribution-5302260a2940).

## References

- [18F Laptop setup](https://engineering.18f.gov/laptop-setup)
- [Federalist](https://federalist.18f.gov)
- [Federalist Jekyll Template](https://github.com/18F/federalist-uswds-jekyll#readme)