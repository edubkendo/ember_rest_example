## Ember-Rest Example with Websockets

This modifies the [*Ember-Rest Example*](https://github.com/dgeb/ember_rest_example) as introduced in the blogpost [*Beginning Ember.js on Rails*](http://www.cerebris.com/blog/2012/01/24/beginning-ember-js-on-rails-part-1/). I added some simple websockets as a proof-of-concept. Now when one user adds or updates a contact in one browser, other browsers will automatically update.  Will refine this in the future.
All contents of the original README were left intact beneath my own additions.

Make sure to run bundle to install the gems and setup the database:

```
bundle install
bundle exec rake db:migrate
```

Follow all steps for setting up [*Juggernaut*](https://github.com/maccman/juggernaut). Verify juggernaut is working correctly.

Start your servers in this order: First Redis, then Juggernaut, then Rails. If all three servers are running correctly, you can now open two seperate browsers on your machine and point them to http://localhost:3000/ . Changes or additions made in one browser will be immediately reflected in the other.

Modified the gemfile to include juggernaut.
Ran 'bundle install'

Added the line:

```html
<script src="http://localhost:8080/application.js" type="text/javascript" charset="utf-8"></script>
```

to ## . There is probably a more "rails" way to do this, but for now we just want to get things rolling.  Will look into it later.

Added:

```html
<script type="text/javascript">
    var jug = new Juggernaut;
    jug.subscribe("channel1", function(data){
      App.contactsController.findAll();
    });
</script>
```

to app/views/contacts/index.html.erb

Added:

```ruby
Juggernaut.publish("channel1", @contact)
```

To app/controllers/contacts_controller.rb in both the create and update actions.
My additions end here and the original README begins below.


# Ember REST Example

This is a simple Rails 3.2 app created to demonstrate using Ember.js with a basic RESTful persistence strategy.

The app itself is a single-page Ember.js take on Rails CRUD scaffolding. It is one of several similar examples I'm creating
to try out Ember.js and different persistence strategies.

I extracted the ultra-simple ember-rest.js from this example:
https://github.com/cerebris/ember-rest

## Installation

Assuming Ruby 1.9.2+ with bundler gem installed:

    $ bundle install
    $ bundle exec rake db:migrate
    $ rails s

## Notes

Please help improve this example by filing issues and pull requests!

## License

Copyright 2012 Dan Gebhardt. MIT License (see LICENSE for details).
