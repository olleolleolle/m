M.RB
----

`m` stands for metal, a better test/unit test runner that can run tests by line number.

    ________________________________________________________________________________
    _________________________/\\\\____________/\\\\_________________________________
    _________________________\/\\\\\\________/\\\\\\________________________________
    __________________________\/\\\//\\\____/\\\//\\\_______________________________
    ___________________________\/\\\\///\\\/\\\/_\/\\\______________________________
    ____________________________\/\\\__\///\\\/___\/\\\_____________________________
    _____________________________\/\\\____\///_____\/\\\____________________________
    ______________________________\/\\\_____________\/\\\___________________________
    _______________________________\/\\\_____________\/\\\__________________________
    ________________________________\///______________\///__________________________
    ________________________________________________________________________________


  - [![Gem Version](https://badge.fury.io/rb/m.png)](https://rubygems.org/gems/m)
  - [![Code Climate](https://codeclimate.com/github/qrush/m.png)](https://codeclimate.com/github/qrush/m)
  - [![Build Status](https://travis-ci.org/qrush/m.png)](https://travis-ci.org/qrush/m)
  - [![Dependency Status](https://gemnasium.com/qrush/m.png)](https://gemnasium.com/qrush/m)
  - [![Coverage Status](https://coveralls.io/repos/qrush/m/badge.png?branch=master)](https://coveralls.io/r/qrush/m)


INSTALL
=======

Install via:


    $ gem install m


If you’re using Bundler, you’ll need to include it in your Gemfile. Toss it into the test group:

``` ruby
group :test do
  gem 'm', '~> 1.5.0'
end
```

Developing a RubyGem? Add m as a development dependency.


``` ruby
Gem::Specification.new do |gem|
  # ...
  gem.add_development_dependency "m", "~> 1.5.0"
end
```

m works on Ruby 2.0+ only.


USAGE
=====

Basically, I was sick of using the -n flag to grab one test to run. Instead, I prefer how RSpec’s test runner allows tests to be run by line number.

Given this file:


    $ cat -n test/example_test.rb
     1  require 'test/unit'
     2
     3  class ExampleTest < Test::Unit::TestCase
     4    def test_apple
     5      assert_equal 1, 1
     6    end
     7
     8    def test_banana
     9      assert_equal 1, 1
    10    end
    11  end


You can run a test by line number, using format m TEST_FILE:LINE_NUMBER_OF_TEST:


    $ m test/example_test.rb:4
    Run options: -n /test_apple/

    # Running tests:

    .

    Finished tests in 0.000525s, 1904.7619 tests/s, 1904.7619 assertions/s.

    1 tests, 1 assertions, 0 failures, 0 errors, 0 skips


Hit the wrong line number? No problem, m helps you out:


    $ m test/example_test.rb:2
    No tests found on line 2. Valid tests to run:

     test_apple: m test/examples/test_unit_example_test.rb:4
    test_banana: m test/examples/test_unit_example_test.rb:8


Want to run the whole test? Just leave off the line number.


    $ m test/example_test.rb
    Run options:

    # Running tests:

    ..

    Finished tests in 0.001293s, 1546.7904 tests/s, 3093.5808 assertions/s.

    1 tests, 2 assertions, 0 failures, 0 errors, 0 skips

If you want to run all the tests in a directory as well as its subdirectories, use the `-r` flag:

    $ m -r test/models
    "Searching provided directory for tests recursively"
    Run options:

    ..

    Finished in 3.459902s, 45.0880 runs/s, 87.5747 assertions/s.

    156 tests, 303 assertions, 0 failures, 0 errors, 13 skips


SUPPORT
=======

`m` works with a few Ruby test frameworks:

  - Test::Unit
  - ActiveSupport::TestCase
  - MiniTest::Unit::TestCase


CONTRIBUTING
============

You can run all the tests with:

    bundle exec rake tests

You can also run tests selectively. For minitest 4 run:

    appraisal minitest4 rake test

and the ones for minitest 5 with:

    appraisal minitest5 rake test TEST=test/minitest_5_test.rb

In the case of minitest 5, we have to specify the test to run, because running
the whole suite will fail due to incompatibilities with ruby (at least until
2.1.1).


LICENSE
=======

This gem is MIT licensed, please see LICENSE for more information.
