require 'rake/testtask'
require 'open-uri'
require 'fileutils'

Rake::TestTask.new do |t|
  t.libs.push("./")
  t.test_files = FileList['tests/*.rb']
  t.verbose = true
end

task :sass do
  puts "Compiling and minifying .scss files in sass/"
  scss_files = FileList['sass/*.scss']
  scss_files.each do |file|
    puts "Processing: #{file}"
    `sass #{file}:public/css/#{file[5..-5]}css --style compressed`
  end
end

namespace :update do
  task :jquery do
    open('jquery.js', 'wb') do |file|
      file << open('http://code.jquery.com/jquery-latest.min.js').read
    end
    FileUtils.mv('./jquery.js', './public/js/jquery.js')
    puts "Downloaded the latest JQuery"
  end

  task :bootstrap do
    
  end
end

task :default => ["test"]
