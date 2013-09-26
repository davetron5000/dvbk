require "rubygems"
require 'rake'

desc "Automatically generate site at :4000 for local dev"
task :dev do
  system "jekyll serve --watch"
end # task :dev

desc "Start Sass so that is compiles to css upon file save"
task :sass do
  system "sass --watch _sass:css"
end # task :sass

desc "Start Sass so that is minifies and compiles to nkd/css/i.css upon file save"
task :minify do
  system "sass --watch _sass --style compressed"
end # task :minify

desc "Remove _site from directory before committing"
task :clean do
  system "rm -rf _site"
end # task :clean

desc "Download JS files"
task :js do
  File.open("_includes/_js_includes.html","w") do |file|
    {
      "jQuery" => {
        url: "http://code.jquery.com/jquery-2.0.3.min.js" 
      },
      "simple modal" => {
        url: "https://simplemodal.googlecode.com/files/jquery.simplemodal.1.4.4.min.js"
      },
      "highlight.js" => {
        url: "http://yandex.st/highlightjs/7.3/highlight.min.js",
        init: "hljs.initHighlightingOnLoad();",
      },
    }.each do |library,options|
        puts "Downloading #{library}..."
        url = options.fetch(:url)
        filename = options.fetch(:filename) { url.split(/\//).last }
        `curl '#{url}' > js/vendor/#{filename}`
        file.puts "<script src='js/vendor/#{filename}'></script>"
        if options[:init]
          file.puts "<script>#{options[:init]}</script>"
        end
      end
  end
end
