# jekyll-template

Template [Jekyll](https://jekyllrb.com) website without styling for use with [GitHub Pages](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll).

Code syntax highlighting is based on the [Poole](https://github.com/poole/poole) theme. Consistency across browsers and compressed HTML are achieved with [normalize.css](https://github.com/necolas/normalize.css) and [jekyll-compress-html](https://github.com/penibelst/jekyll-compress-html).

## Using Jekyll on ARM Macs

I found the instructions [here](https://jekyllrb.com/docs/installation/macos/) didn't work. I used `rbenv` instead:

1. Install Xcode command line tools with `xcode-select --install`
1. Install [Homebrew](https://brew.sh)
1. Install `rbenv` with `brew install rbenv ruby-build`
1. Follow instructions in `rbenv init`
1. Install Ruby and set as the global default with `rbenv install 3.0.0 && rbenv global 3.0.0 && rbenv rehash`
1. Install bundler and Jekyll with `gem install bundler jekyll`
1. Add Ruby to your path with `echo 'export PATH="/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/3.0.0/bin:$PATH"' >> ~/.zshrc`

### Testing your installation

Check your Ruby version:
```bash
% which -a ruby
/Users/USERNAME/.rbenv/shims/ruby  # rbenv Ruby
/usr/bin/ruby  # system Ruby
```
Running `which ruby` should return `/Users/USERNAME/.rbenv/shims/ruby`.

Check your Ruby version:
```
% ruby -v
ruby 3.0.0p0 (2020-12-25 revision 95aff21468) [arm64-darwin21]
```

Create a template website and start a webserver:
```
% jekyll new my-awesome-site
% cd my-awesome-site
% bundle exec jekyll serve
```

### Fixing issues

You may need to run some or all of the commands below to fix installation issues.

*To install `webbrick`*:
```bash
% bundle add webrick
```

*To fix `sassc`/`ffi` issues:*
```bash
% gem uninstall sassc
% gem install sassc -- --disable-march-tune-native
% gem uninstall ffi
% gem install ffi
% gem list | grep ffi
ffi (1.15.5, 1.15.0)  # should be version 1.14.2+
public_suffix (5.0.0, 4.0.7, 4.0.6)
```

*To fix `eventmachine` issues*:
```bash
% gem install eventmachine -v '1.2.7' -- --with-ldflags="-Wl,-undefined,dynamic_lookup"
```

*Update bundler*:
```bash
% bundle update --bundler
% bundle install --redownload
```

### Sources

* https://github.com/github/pages-gem/issues/752
* https://www.earthinversion.com/blogging/how-to-install-jekyll-on-appple-m1-macbook/
* https://www.shouvikbasak.net/website/jekyll-on-macos-apple-m1-solved/
* https://stackoverflow.com/questions/70991441/i-cant-install-eventmachine-gem-on-mac-m1
* https://twitter.com/riffraff/status/1573204825260580864

## License

Released under the [MIT License](LICENSE).
