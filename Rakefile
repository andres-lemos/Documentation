namespace :build do
  desc 'prepare build'
  task :prebuild do
    Dir.mkdir 'Software_Guide/images' unless Dir.exists? 'Software_Guide/images'
    Dir.glob("Software_Guide/*/images/*").each do |image|
      FileUtils.copy(image, "Software_Guide/images/" + File.basename(image))
    end
  end

  desc 'Generate HTML output'
  task :html => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor Software_Guide/WaRP7-Software-Guide.adoc`
    puts " -- HTML output at Software_Guide/WaRP7-Software-Guide.html"
  end

  desc 'Generate EPub output'
  task :epub => :prebuild do
    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 Software_Guide/WaRP7-Software-Guide.adoc`
    puts " -- Epub output at Software_Guide/WaRP7-Software-Guide.epub"
  end

  desc 'Generate Mobi (kf8) output'
  task :mobi => :prebuild do
    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -a ebook-format=kf8 Software_Guide/WaRP7-Software-Guide.adoc`
    puts " -- Mobi output at Software_Guide/WaRP7-Software-Guide.mobi"
  end

  desc 'Generate PDF output'
  task :pdf => :prebuild do
    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf -a pdf-style=book \
                                 -a pdf-stylesdir=theme/pdf \
                                 Software_Guide/WaRP7-Software-Guide.adoc`
    puts " -- PDF  output at Software_Guide/WaRP7-Software-Guide.pdf"
  end

  desc 'Generate PDF using fopub'
  task :pdf_fopub => :prebuild do
    puts "Converting to PDF (using fopub)..."
    `bundle exec asciidoctor -b docbook -d book -a data-uri! Software_Guide/WaRP7-Software-Guide.adoc`
    `bundle exec fopub Software_Guide/WaRP7-Software-Guide.xml \
                       -param page.size a5`
    puts " -- PDF  output at Software_Guide/WaRP7-Software-Guide.pdf"
  end

end

desc 'Build all default formats'
task :build => [ "build:html", "build:epub", "build:mobi", "build:pdf" ]
