require 'rubygems'
require 'bundler/setup'

require 'rake'

require 'rspec/core'
require 'rspec/core/rake_task'

require 'grape/activerecord/rake'

namespace :db do
  task :environment do
    require_relative 'config/environment'
  end
end

RSpec::Core::RakeTask.new(:spec) do |spec|
  spec.pattern = FileList['spec/api/*_spec.rb']
end

task :environment do
  ENV['RACK_ENV'] ||= 'development'
  require File.expand_path('../config/environment', __FILE__)
end

task routes: :environment do
  Embryo::API.routes.each do |route|
    method = route.route_method.ljust(10)
    path = route.route_path
    puts "     #{method} #{path}"
  end
end

require 'rubocop/rake_task'
RuboCop::RakeTask.new(:rubocop)

task default: [:rubocop, :spec]
