require 'rake/testtask'
require 'open-uri'
require 'fileutils'
require 'zip/zipfilesystem'

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
    open('bootstrap.zip', 'wb') do |file|
      file << open('http://twitter.github.com/bootstrap/assets/bootstrap.zip').read
    end

    Zip::ZipFile.open("bootstrap.zip") do |zipfile|
      zipfile.each do |file|
        zipfile.extract(file, "./#{file.name}")
      end
    end

    FileUtils.mv('./bootstrap/css/bootstrap.min.css', './public/css/bootstrap.min.css')
    FileUtils.mv('./bootstrap/img/glyphicons-halflings-white.png', './public/img/glyphicons-halflings-white.png')
    FileUtils.mv('./bootstrap/img/glyphicons-halflings.png', './public/img/glyphicons-halflings.png')
    FileUtils.mv('./bootstrap/js/bootstrap.min.js', './public/js/bootstrap.min.js')
    FileUtils.rm_r('./bootstrap')
    FileUtils.rm('./bootstrap.zip')

    puts "Downloaded the latest Twitter Bootstrap"
  end

  task :all do

  end
end

task :default => ["test"]
