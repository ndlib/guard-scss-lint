# coding: utf-8

require 'bundler/gem_tasks'
require 'guard/rake_task'
require 'rspec/core/rake_task'
require 'rubocop/rake_task'

RSpec::Core::RakeTask.new(:spec)
RuboCop::RakeTask.new(:style)
Guard::RakeTask.new(:guard, '--no-interactions')

namespace :ci do
  task :spec do
    ENV['CI'] = 'true'

    ENV['CI_REPORTS'] = 'spec/reports'
    require 'ci/reporter/rake/rspec'
    Rake::Task['ci:setup:rspec'].invoke

    Rake::Task['spec'].invoke
  end
end

desc 'Run RSpec and RuboCop'
task all: [:spec, :style]

task default: :guard
