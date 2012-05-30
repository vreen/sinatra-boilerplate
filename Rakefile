require 'rake/testtask'

Rake::TestTask.new do |t|
  t.libs.push("./")
  t.test_files = FileList['tests/*.rb']
  t.verbose = true
end

task :sass do
  scss_files = FileList['sass/*.scss']
  scss_files.each do |file|
    `sass #{file}:public/css/#{file[5..-5]}css`
  end
end

task :default => ["test"]