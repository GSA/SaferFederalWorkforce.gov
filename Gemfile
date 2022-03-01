ruby ">= 2.7.4"

source "https://rubygems.org"

gem "jekyll", "~> 3.9"
gem "mini_racer", "0.4.0"  # may not work with newer
gem "sprockets", "~> 3.7"
gem "kramdown-parser-gfm", "~> 1.1.0"

group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.15"
  gem "jekyll-last-modified-at" # used in sitemap
  gem "jekyll-sitemap"
  gem "jekyll-seo-tag"
  gem "jekyll-autoprefixer"
  gem "jekyll-assets", "~> 3.0"
  gem "jekyll-include-cache"
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.0" if Gem.win_platform?

gem "html-proofer", "~> 3.19"
