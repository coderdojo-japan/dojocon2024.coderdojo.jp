task default: 'test'

# Upsert individual project page by data
desc 'Upsert project page by project data'
task :upsert_project_pages_by_data do
  ruby "tasks/upsert_project_pages_by_data.rb"
end

# HTML Proofer helps to detect broken links.
# https://github.com/gjtorikian/html-proofer
require 'html-proofer'
task test: [:build] do
  options = {
    checks: ['Links', 'Images', 'Scripts', 'OpenGraph', 'Favicon'],
    allow_hash_href:  false,
    disable_external: true,
    enforce_https:    true,

    # NOTE: You can ignore file, URL, and response as follows
    ignore_files: [
      /google(.*)\.html/,
    ],
    ignore_urls: [
      %r{^http://coderdojo-nago.com}, # Use REGEX to skip testing URLs in a domain like this
      %r{^http://www.2469samurai.com},
      %r{^http://food.starfree.jp},
      %r{^http://ichikawa.coderdojo.chiba.jp},
      %r{^http://coderdojo-sennan.net},
    ]
    #ignore_status_ignore: [0, 500, 999],
  }

  HTMLProofer.check_directory('_site', options).run
end

# Enable 'build' to flush cache files via 'clean'
task build: [:clean] do
  system 'bundle exec jekyll build' unless ENV['SKIP_BUILD'] == 'true'
end

task :clean do
  system 'bundle exec jekyll clean' unless ENV['SKIP_BUILD'] == 'true'
end
