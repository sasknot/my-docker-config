FROM ruby:2.1

# installs nodejs and npm
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

# creates and changes workdir
RUN mkdir /app
WORKDIR /app

# copies important files
ADD Gemfile /app/Gemfile
ADD Gemfile.lock /app/Gemfile.lock
ADD gems /app/gems

# installs app
RUN bundle install

# copies other files
ADD . /app
