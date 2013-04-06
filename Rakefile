ENV["BUNDLE_GEMFILE"] ||= File.expand_path("../Gemfile", __FILE__)

require "rubygems"
require "bundler"
Bundler.setup(:default, :test, :development)

require "bundler/gem_tasks"

require "rake/dsl_definition"
require "rake"
require "rspec/core/rake_task"


if defined?(RSpec)
  namespace :spec do
    desc "Run Unit Tests"
    unit_rspec_task = RSpec::Core::RakeTask.new(:unit) do |t|
      t.pattern = "spec/unit/**/*_spec.rb"
      t.rspec_opts = %w(--format progress --color)
    end

    namespace :integration do
      desc "Run AWS Integration Tests"
      integration_rspec_task = RSpec::Core::RakeTask.new(:aws) do |t|
        t.pattern = "spec/integration/aws/**/*_spec.rb"
        t.rspec_opts = %w(--format progress --color)
      end
    end

    desc "Run all Integration Tests"
    task :integration => %w[spec:integration:aws]
  end

  desc "Install dependencies and run tests"
  task :spec => %w(spec:unit spec:integration)
end

task :default => :spec