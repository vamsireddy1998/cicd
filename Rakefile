# Rakefile for AWS CodePipeline Demo

task :default => [:build, :test, :package]

task :build do
  puts "======================================"
  puts "Building application"
  puts "======================================"
  
  mkdir_p "build/html"
  
  if Dir["src/*.haml"].any?
    puts "Found HAML files, compiling..."
    Dir["src/*.haml"].each do |haml_file|
      # Generate output filename
      html_file = "build/html/" + File.basename(haml_file, ".haml") + ".html"
      puts "Compiling #{haml_file} -> #{html_file}"
      
      # Correct haml command syntax - using the executable properly
      sh "haml < #{haml_file} > #{html_file}"
    end
  else
    puts "No HAML files found, creating sample HTML"
    File.open("build/html/index.html", "w") do |f|
      f.puts "<!DOCTYPE html>"
      f.puts "<html><head><title>CI/CD Demo</title></head><body>"
      f.puts "<h1>Hello from Jenkins Build!</h1>"
      f.puts "<p>Build Time: #{Time.now}</p></body></html>"
    end
  end
  puts "Build complete!"
end

task :test do
  puts "======================================"
  puts "Running tests"
  puts "======================================"
  
  if File.exist?("build/html/index.html")
    puts "✅ Test passed: HTML file exists"
  else
    puts "❌ Test failed: No HTML files found"
    exit 1
  end
  puts "All tests passed!"
end

task :package do
  puts "======================================"
  puts "Packaging for deployment"
  puts "======================================"
  
  mkdir_p "deploy/build"
  cp_r "build", "deploy/"
  puts "Package created in deploy/ directory"
  puts "Package contents:"
  sh "ls -la deploy/build/html/"
end
