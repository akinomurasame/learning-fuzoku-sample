require 'rake'
require 'yaml'

def load_yaml(file)
  raise "Can't open #{yamlfile}." if file.nil? || !File.exist?(file)
  return YAML.load_file(file)
end

config = load_yaml('config.yml')
bookname = config["bookname"] if bookname.nil?

desc 'create all books (.epub, .pdf, .mobi)'
task all: [:epub, :pdf, :mobi]

desc 'create .epub'
task :epub do
  sh 'bundle exec review-epubmaker config.yml'
end

desc 'create .pdf'
task :pdf do
  sh 'rm -rf *pdf'
  sh 'bundle exec review-pdfmaker config.yml'
end

desc 'create .mobi'
task :mobi do
  sh 'rm -f *.mobi'
  sh "kindlegen #{bookname}.epub || true"
end

desc 'send to kindle'
task :send_to_kindle do
  sh "bundle exec kindlemail -f #{bookname}.mobi"
end

desc 'convert ./src/*.md to ./*.re'
task :md2review do
  Dir.glob('./src/*.md') do |md|
    re = File.basename(md).sub(/\.md$/, '.re')
    sh "bundle exec md2review #{md} > ./#{re}"
  end
end

desc 'clean working files'
task :clean do
  sh "rm -rf #{bookname}-*"
  sh 'rm -f *.epub'
  sh 'rm -f *.pdf'
  sh 'rm -f *.mobi'
end

task default: :all
