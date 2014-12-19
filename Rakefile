require 'bundler/setup'
require 'rake'
require 'yaml'
require 'epub_validator'

config = YAML.load_file('config.yml')
bookname = config["bookname"]
bookname = "example" if bookname.nil?
epub_file = bookname+'.epub'
mobi_file = bookname+'.mobi'

def source_exist(source, error_message= nil)
  return true if File.exist?(source)

  puts error_message if error_message
  fail "#{source} does not exist."
  false
end


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
  sh "kindlegen #{epub_file} || true"
end

desc 'validation .epub'
task :epub_validation do
  next unless source_exist(epub_file, 'Cant execute :epub_validation')
  epub = EpubValidator.check(epub_file)
  puts "checking #{epub_file}..."

  if epub.valid?
    puts "OK, #{epub_file} is valid!"
  else
    epub.messages.each do |m|
      puts m
    end
    fail "#{epub_file} is invalid :-("
  end
end

desc 'send to kindle'
task :send_to_kindle do
  sh "bundle exec kindlemail -f #{mobi_file}"
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
