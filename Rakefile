#!/usr/bin/env ruby

require 'rake/testtask'
require 'fileutils'

# Default task just calls compile
task default: :compile

# Dummy compile task (does nothing)
task :compile do
  puts "Skipping compile task..."
end

# Clean generated HTML files
task :clean do
  FileUtils.rm_r(Dir.glob("./*.html"), force: true)
  puts "Cleaned HTML files"
end

# Run tests
task :test do
  Rake::TestTask.new do |t|
    t.test_files = FileList['test/jenkins_sample_test.rb']
  end
end
