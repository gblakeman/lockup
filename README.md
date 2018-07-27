<img src="http://lockupgem.com/github_host/lockup_mark.png" width="100" height="134" alt="Lockup Shield" />

# Lockup

[![Gem Version](https://badge.fury.io/rb/lockup.png)](http://badge.fury.io/rb/lockup)

A simple gem to more elegantly place a staging server or other in-progress rails application behind a basic codeword. It’s easy to implement, share with clients/collaborators, and more beautiful than the typical password-protection sheet.

_“Can I come into your fort?”_

_“…what’s the codeword?”_

(currently used in production with Rails 3.X, Rails 4.X, and Rails 5.X)

[Demos and more information.](http://lockupgem.com)

## Installation

1. Add this line to your application’s Gemfile:

        gem 'lockup'

2. Define a codeword (see Usage below).

3. Mount the engine in your application’s routes file (usually first, for best results):

        mount Lockup::Engine, at: '/lockup'

## Usage

To set a codeword, define LOCKUP_CODEWORD in your environments/your_environment.rb file like so:

    ENV["LOCKUP_CODEWORD"] = 'secret'

If you think you might need a hint:

    ENV["LOCKUP_HINT"] = 'Something that you do not tell everyone.'

If you’re using Rails 4.1 or greater, you can add your Lockup Codeword via Rails Secrets functionality in your secrets.yml file:

    lockup_codeword: 'love'

    lockup_hint: 'Pepé Le Pew'

If you’re using [Figaro](https://github.com/laserlemon/figaro), set your Lockup codeword and hint (optional) in your application.yml file:

    lockup_codeword: 'love'

    lockup_hint: 'Pepé Le Pew'

**Codewords are not case-sensitive, by design. Keep it simple.**

## Advanced Usage

### Use Lockup around a specific controller:

1. Follow the installation instructions above.

2. In your application_controller.rb file, add:

        skip_before_action :check_for_lockup

4. In the controller(s) you would like to restrict:

        before_action :check_for_lockup

### Link it with no typing:

    http://somedomain.com/or_path/?lockup_codeword=love

The visitor is redirected and the cookie is set without them ever seeing the Lockup splash page.

(Lockup also makes a rudimentary attempt based on user agent to **block major search engine bots/crawlers** from following this link and indexing the site, just in case it ever gets out into the wild.)

### Set a custom lifetime for cookie

The cookie set by Lockup defaults to 5 years. If you want to set a shorter amount of time, you can specify a number of weeks:

    ENV["COOKIE_LIFETIME_IN_WEEKS"] = 4

    cookie_lifetime_in_weeks: 4

### Design Customization

If you would like to change the content or design of the lockup page, you can create the directories `app/views/layouts/lockup` and `app/views/lockup/lockup` and populate them with the default content from [here](https://github.com/gblakeman/lockup/tree/master/app/views), and then customize as desired.

## Contribute

Pull requests are quite welcome.

## Project Site

[lockupgem.com](http://lockupgem.com)
