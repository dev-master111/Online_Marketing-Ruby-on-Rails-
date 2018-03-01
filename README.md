[![Build Status](https://travis-ci.org/openfoodfoundation/openfoodnetwork.svg?branch=master)](https://travis-ci.org/openfoodfoundation/openfoodnetwork)
[![Code Climate](https://codeclimate.com/github/openfoodfoundation/openfoodnetwork.png)](https://codeclimate.com/github/openfoodfoundation/openfoodnetwork)
### Dependencies

* Rails 3.2.x
* Ruby 2.1.5
* PostgreSQL database
* PhantomJS (for testing)
* See Gemfile for a list of gems required

### Get it running

For those new to Rails, the following tutorial will help get you up to speed with configuring a Rails environment: http://guides.rubyonrails.org/getting_started.html .

First, check your dependencies: Ensure that you have Ruby 2.1.5 installed:

    ruby --version

Install the project's gem dependencies:

    cd openfoodnetwork
    bundle install

Configure the site:

    cp config/application.yml.example config/application.yml
    edit config/application.yml

Create a PostgreSQL user:

* Login as your system postrgresql priviledged user: `sudo -i -u postgres` (this may vary on your OS). Now your prompt looks like: `[postgres@your_host ~]$`
* Create the `ofn` database superuser and give it the password `f00d`:

```
createuser -s -P ofn
```

Create the development and test databases, using the settings specified in `config/database.yml`, and populate them with a schema and seed data:

    rake db:setup

Load some default data for your environment:

    rake openfoodnetwork:dev:load_sample_data

At long last, your dreams of spinning up a development server can be realised:

    rails server


### Testing

Tests, both unit and integration, are based on RSpec. To run the test suite, first prepare the test database:

    bundle exec rake db:test:prepare

Then the tests can be run with:

    bundle exec rspec spec

The site is configured to use
[Zeus](https://github.com/burke/zeus) to reduce the pre-test
startup time while Rails loads. See the Zeus github page for
usage instructions.
