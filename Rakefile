# frozen_string_literal: true
# rubocop:disable all

#require 'bundler/gem_tasks'
#require 'rspec/core/rake_task'

sheep_dir = ENV['SHEEP_DIR']
cur = Dir.pwd

desc 'Making Yardoc to the SHEEP_DOC_DIR directory.'
task 'doc' do
  sh "rm -rf  docs"
  sh 'mkdir -p copy'
  sh "cp #{sheep_dir}/*.md copy/"
  sh "cp #{sheep_dir}/manual/*.md copy/"
  sh "mv copy/README.md README.md"
  sh "#{ENV['RBENV_COM']} bundle exec yardoc -m markdown --plugin sorbet --no-cache -o #{cur}/docs #{sheep_dir}/{lib,app}/**/*.rb - copy/*.md"
end

desc 'Push document repository'
task 'push' do
  sh "git add -A && git commit --amend --no-edit && git push origin main -f"
end

desc 'Init document repository'
task 'init' do
  sh "rm -rf docs && git add -A && git commit --amend --no-edit && git push origin main -f"
end

desc 'change ruby version by rbenv. Specify SHEEP_RV environment parameter for ruby version'
task 'change-version' do
  if !ENV['SHEEP_RV']
    puts 'specify ruby version like 3.0.0 to SHEEP_RV env'
    exit 1
  else
    sh "rbenv local #{ENV['SHEEP_RV']}"
    sh "bundle update"
  end
end
