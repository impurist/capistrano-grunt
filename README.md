# capistrano-grunt

capistrano-grunt is a [Capistrano](https://github.com/capistrano/capistrano) extension that will let you run [Grunt](http://gruntjs.com/) tasks during your deploy process.

## Installation

1. Install the Gem

```bash
gem install capistrano-grunt
```

Or if you're using Bundler, add it to your `Gemfile`:

```ruby
gem 'capistrano-grunt', github: 'swalkinshaw/grunt'
```

2. Add to `Capfile` or `config/deploy.rb`:

```ruby
require 'capistrano/grunt'
```

## Usage

Set what Grunt tasks you want run in your `deploy.rb` file:

```ruby
set :grunt_tasks, 'deploy:production'
```

If you don't set `grunt_tasks`, Grunt will run its default task (equivalent to just running `grunt` from the command line).

To run multiple tasks, use an array in the order you want them run:

```ruby
set :grunt_tasks, ['deploy:production', 'cdn']
```

The above would be equivalent of running the following from the command line:

```bash
grunt deploy:production
grunt cdn
```

Then add the task to your `deploy.rb`:

```ruby
after 'deploy:finalize_update', 'grunt'
```

To set `grunt` command line options like the `Gruntfile` path, use the `grunt_options` variable:

```ruby
set :grunt_options, '--gruntfile config/Gruntfile.js'
```

### Tasks

* `grunt`: Runs the Grunt task(s) specified in the `grunt_tasks` variable.

### Dependencies

This extension also adds the `grunt` command as a Capistrano dependency. Meaning when you run cap deploy:check, it will make sure the `grunt` command exists.

### Configuration

* `grunt_tasks`: Grunt tasks to run. Use a string for a single task or an array for multiple ones. Defaults to `default`.
* `grunt_options`: Options for `grunt` command. Defaults to an empty string.
