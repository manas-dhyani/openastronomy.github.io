source "https://rubygems.org"

require 'json'
require 'uri'
require 'open-uri'

versions =
    begin
        JSON.parse(URI.parse('https://pages.github.com/versions.json').open.read)
    rescue SocketError
        { 'github-pages' => 67 }
    end

gem 'github-pages', versions['github-pages']
gem 'html-proofer'