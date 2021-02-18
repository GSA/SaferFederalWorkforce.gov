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

This repository contains the following examples and functionality:

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
