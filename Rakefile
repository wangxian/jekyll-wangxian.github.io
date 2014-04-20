task :default => [:server]

desc 'Start jekyll server'
task :server do
  `jekyll serve --watch`
end # task start server

task :post do
  title = get_stdin("Enter a title for your post(eg, first-post): ")
  filename = "_posts/" + Time.now().strftime("%Y-%m-%d-") + title + '.md'
  if File.exists? filename then
    puts "Post already exists: #{filename}"
    return
  end

  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "comments: true"
    post.puts "title: \"#{title.gsub(/-/, ' ')}\""
    post.puts 'category: ""'
    # post.puts 'description: ""'
    post.puts "tags: "
    post.puts "  - "
    post.puts "---"
  end
end # task :post

desc 'reset git repository'
task :reset do
  `rm -rfv .git`
  `git init .`
  `git remote add origin git@github.com:wangxian/wangxian.github.io.git`
  `git add .`
  `git commit -a -m "init"`
  puts "finish..."
  puts "you can push use cli: git push origin master --force"
end

desc 'rake test'
task :test do
  title = get_stdin("Enter a title for your post:")
  puts title
  puts "hello world!"
end

def get_stdin(message)
  print message
  STDIN.gets.chomp
end