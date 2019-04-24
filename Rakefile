require 'rake'
require 'yaml'

SOURCE = "."
CONFIG = {
  'posts' => File.join(SOURCE, "_posts"),
  'post_ext' => "md",
  'code' => File.join(SOURCE, "_code"),
  'code_ext' => "md",
  'linux' => File.join(SOURCE, "_linux"),
  'linux_ext' => "md",
  'wiki' => File.join(SOURCE, "_wiki"),
  'wiki_ext' => "md",
  'ai' => File.join(SOURCE, "_ai"),
  'ai_ext' => "md",
}

# Usage: rake post title="A Title"
desc "Begin a new post in #{CONFIG['posts']}"
task :post do
  abort("rake aborted: '#{CONFIG['posts']}' directory not found.") unless FileTest.directory?(CONFIG['posts'])
  title = ENV["title"] || "new-post"
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join(CONFIG['posts'], "#{Time.now.strftime('%Y-%m-%d')}-#{slug}.#{CONFIG['post_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "category: "
    post.puts "tags: []"
    post.puts "---"
  end
end # task :post

task :wiki do
  abort("rake aborted: '#{CONFIG['wiki']}' directory not found.") unless FileTest.directory?(CONFIG['wiki'])
  title = ENV["title"] || "new-wiki"
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join(CONFIG['wiki'], "#{Time.now.strftime('%Y-%m-%d')}-#{slug}.#{CONFIG['wiki_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new wiki: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: wiki"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "category: "
    post.puts "tags: []"
    post.puts "---"
  end
end # task :post

task :linux do
  abort("rake aborted: '#{CONFIG['linux']}' directory not found.") unless FileTest.directory?(CONFIG['linux'])
  title = ENV["title"] || "new-post"
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join(CONFIG['linux'], "#{Time.now.strftime('%Y-%m-%d')}-#{slug}.#{CONFIG['linux_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new linux: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: wiki"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "category: "
    post.puts "tags: []"
    post.puts "---"
  end
end # task :post


task :ai do
  abort("rake aborted: '#{CONFIG['ai']}' directory not found.") unless FileTest.directory?(CONFIG['ai'])
  title = ENV["title"] || "new-post"
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join(CONFIG['ai'], "#{Time.now.strftime('%Y-%m-%d')}-#{slug}.#{CONFIG['ai_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new ai: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: wiki"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "category: "
    post.puts "tags: []"
    post.puts "---"
  end
end # task :post


task :page do
  abort("rake aborted: '#{CONFIG['page']}' directory not found.") unless FileTest.directory?(CONFIG['page'])
  title = ENV["title"] || "new-post"
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join(CONFIG['page'], "#{Time.now.strftime('%Y-%m-%d')}-#{slug}.#{CONFIG['page_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new page: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: page"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "category: "
    post.puts "tags: []"
    post.puts "---"
  end
end # task :post



task :code do
  abort("rake aborted: '#{CONFIG['code']}' directory not found.") unless FileTest.directory?(CONFIG['code'])
  title = ENV["title"] || "new-post"
  slug = title.downcase.strip.gsub(' ', '-').gsub(/[^\w-]/, '')
  filename = File.join(CONFIG['code'], "#{slug}.#{CONFIG['code_ext']}")
  if File.exist?(filename)
    abort("rake aborted!") if ask("#{filename} already exists. Do you want to overwrite?", ['y', 'n']) == 'n'
  end

  puts "Creating new code: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/-/,' ')}\""
    post.puts "category: "
    post.puts "tags: []"
    post.puts "---"
  end
end # task :post