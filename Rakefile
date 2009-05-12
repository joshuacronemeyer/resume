require 'rubygems'
require 'rake/testtask'
require 'ftools'
require 'yaml'

task :default => :build

task :build => [:clean, :fill_template] do |t|
  `latex  -interaction=batchmode -output-directory=target target/ready_resume.tex`
  `dvipdf target/ready_resume.dvi target/resume.pdf`
end

task :fill_template => :configure do |t|
  content = nil
  File.open('resume.tex') { |f| content = f.readlines }
  template_marker_index = content.index("%FILL_IN_TOP_SECRET_ADDRESS\n")
  content.insert(template_marker_index + 1, "\\address{#{@address}}") unless template_marker_index.nil?
  mkdir('target')
  File.open('target/ready_resume.tex', "w"){ |f| f.puts(content) }
end

task :configure do |t|
  File.open( 'config.yml' ) { |yf| @address = YAML::load( yf )['address'] }
end

task :clean do |t|
  rm_rf("target")
end
