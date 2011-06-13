require 'fileutils'

task :default => 'oocss:regen'

namespace :oocss do

  desc "regenerate the oocss.css file"
  task :regen do
    sh 'rm -f all.min.css'
    sh 'juicer merge all.css'
  end

end

namespace :git do
  def commit_message
    return ENV['m'] if ENV['m']
    raise "Commit message expected. Sample:\n   rake git:commit m='your commit message'"
  end

  desc "regenerate oocss.css & push to the git repository"
  task :release => ['oocss:regen', 'git:add', 'git:commit', 'git:push']

  desc "add all the modifications to the git repository, including deletions"
  task :add do
    sh 'git add .'
    sh 'git ls-files -z -d | xargs -0 --no-run-if-empty git rm'
  end

  desc "Commit with a message"
  task :commit do
    sh "git commit -m #{commit_message.inspect}"
  end

  desc "Push to origin"
  task :push do
    sh "git push origin master"
  end

end
