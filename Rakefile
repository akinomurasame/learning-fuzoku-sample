require 'rake'

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
  sh 'kindlegen learning-fuzoku-sample.epub || true'
end

desc 'send to kindle'
task :send_to_kindle do
  sh 'bundle exec kindlemail -f learning-fuzoku-sample.mobi'
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
  sh 'rm -rf learning-fuzoku-sample-*'
  sh 'rm -f *.epub'
  sh 'rm -f *.pdf'
  sh 'rm -f *.mobi'
end

task default: :all
