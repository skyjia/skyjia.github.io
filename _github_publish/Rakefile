require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"


# Change your GitHub reponame
GITHUB_REPONAME = "skyjia/skyjia.github.io"


desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "_site"
  })).process
end


desc "Generate and publish blog to gh-pages"
task :publish => [:generate] do
  publish = "_github_publish/"
  cp_r "_site/.", publish
  pwd = Dir.pwd
  Dir.chdir publish

  message = "Site updated at #{Time.now.utc}"
  system "touch .nojekyll"
  system "git add . -A"
  system "git commit -m #{message.inspect}"
  system "git push origin master"

  Dir.chdir pwd
end