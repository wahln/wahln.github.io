source "https://rubygems.org"
ruby "3.3.11"

gem "jekyll"
gem "jekyll-remote-theme" # we consume al-folio as a remote theme

# Core plugins that directly affect site building (mirrors al-folio v0.14.7)
group :jekyll_plugins do
    gem "jekyll-archives-v2"
    gem "jekyll-email-protect"
    gem "jekyll-feed"
    gem "jekyll-get-json"
    gem "jekyll-imagemagick"
    gem "jekyll-include-cache"
    gem "jekyll-jupyter-notebook"
    gem "jekyll-link-attributes"
    gem "jekyll-minifier"
    gem "jekyll-paginate-v2"
    gem "jekyll-regex-replace"
    gem "jekyll-scholar"
    gem "jekyll-sitemap"
    gem "jekyll-tabs"
    # jekyll-terser intentionally omitted: it breaks on remote_theme assets (it stats JS
    # files at their absolute temp path) and needs a JS runtime. JS ships unminified instead.
    gem "jekyll-toc"
    gem "jekyll-twitter-plugin"
    gem "jemoji"
    gem "classifier-reborn" # used for content categorization during the build
end

# Gems for development or external data fetching (outside :jekyll_plugins)
group :other_plugins do
    gem "css_parser"
    gem "feedjira"
    gem "httparty"
    gem "observer"       # used by jekyll-scholar
    gem "ostruct"        # used by jekyll-twitter-plugin
    gem "unicode_utils"  # used by jekyll-scholar (smallcaps/superscript filters)
    gem "webrick"        # required to serve under Ruby 3.x
end
