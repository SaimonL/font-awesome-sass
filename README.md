# FontAwesome::Sass

[![Gem Version](https://badge.fury.io/rb/font-awesome-sass.svg)](https://badge.fury.io/rb/font-awesome-sass)

'font-awesome-sass' is a Sass-powered version of [FontAwesome](http://fortawesome.github.io/Font-Awesome/) for your Ruby projects and plays nicely with
 Ruby on Rails, Compass, Sprockets, etc.

 Refactored to support more Ruby environments with code and documentation humbly used from the excellent
 [bootstrap-sass](https://github.com/twbs/bootstrap-sass) project by the Bootstrap team

## Breaking Changes

With the update to Font Awesome 5.x there are some breaking changes that will effect your use of this gem. Some of the changes include:

  * Icon name changes
  * New icons
  * The use of an icon style (`solid`, `regular`, or `brands`)

You can find more detailed information on these changes on our [Getting Started](https://fontawesome.com/get-started/web-fonts-with-css) guide, our [How to Use](https://fontawesome.com/how-to-use/web-fonts-with-css) guide, and our [Upgrading from Version 4](https://fontawesome.com/how-to-use/upgrading-from-4) guide.

## Installation

Please see the appropriate guide for your environment of choice:

* [Ruby on Rails](#a-ruby-on-rails).
* [Compass](#b-compass-without-rails) not on Rails.

### a. Ruby on Rails

In your Gemfile include:

```ruby
gem 'font-awesome-sass', '~> 5.9.0'
```

And then execute:

```sh
bundle install
```

Import the FontAwesome styles in your `app/assets/stylesheets/application.css.scss`. The `font-awesome-sprockets` file
includes the sprockets assets helper Sass functions used for finding the proper path to the font file.

```scss
@import "font-awesome-sprockets";
@import "font-awesome";
```

If `app/assets/stylesheets/application.css.scss` does not exist then rename `app/assets/stylesheets/application.css` and add the `@import` statements below the `*= require` statements but outside of the comment block.

#### Rails Helper usage

With Font Awesome 5.x you now need to select what style of icon you want to use. Font Awesome 5.x has 3 styles:

  * solid (`fas`)
  * regular (`far`)
  * brands (`fab`)

In your view:

```ruby
icon('fas', 'flag')
# => <i class="fas fa-flag"></i>
```

```ruby
icon('far', 'address-book', class: 'strong')
# => <i class="far fa-address-book strong"></i>
```

```ruby
icon('fab', 'font-awesome', 'Font Awesome', id: 'my-icon', class: 'strong')
# => <i id="my-icon" class="fab fa-font-awesome strong"></i> Font Awesome
```

Note: the icon helper can take a hash of options that will be passed to the content_tag helper

### b. Compass without Rails

Install the gem

```sh
gem install font-awesome-sass
```

If you have an existing Compass project:

```ruby
# config.rb:
require 'font-awesome-sass'
```

Import the FontAwesome styles

```scss
@import "font-awesome-compass";
@import "font-awesome";
```

## Upgrading from FontAwesome::Sass 4.x

Prepend the style of the icon you want to use (`fas`, `far`, `fab`) class to existing icons:

4.x Syntax

```html
<i class="fa fa-github"></i>
```

5.x Syntax (GitHub icon exists in the Brands style)

```html
<i class="fab fa-github"></i>
```


## Using FontAwesome Pro

Assuming you have purchased fontawesome pro and want to use Rails asset pipeline.

First login to fontawesome and go to the download section. You will see two options in the download seaction, they are "Web" and "Desktop". Click on "Pro for Web" and download it. Unzip it to any tempory folder. 

#### Step 1

* Copy **"./css/all.css"** to you project's stylesheets directory and rename it **"app/assets/stylesheets/fontawesome.css"**
* Copy **"./js/all.js"** to your project's javascripts directory and rename it **"app/assets/javascripts/fontawesome.js"**
* Copy all the fonts from **"webfonts"** folder and place them in **"app/assets/webfonts"** folder (or just copy over the entire folder)

#### Step 2

**Remove** any css settings you have done for this gem such as
* @import 'font-awesome-sprockets';
* @import 'font-awesome';

Edit file **"app/assets/stylesheets/fontawesome.css"**  
Search **"../webfonts/"** and replace with **"/assets/"**

#### Step 3

Add the following to **"config/initializers/assets.rb"**
```ruby
Rails.application.config.assets.paths << Rails.root.join('app', 'assets', 'webfonts')
Rails.application.config.assets.precompile += %w[.svg .eot .woff .woff2 .ttf]
```
In the class Application. And thats it.  
Test it with `icon(:far, 'tachometer-alt-average')` which is a pro icon.

#### Production

In production don't forget to compile the assets using
`bundle exec rails assets:precompile`
