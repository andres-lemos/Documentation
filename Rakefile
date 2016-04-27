namespace :build do
  desc 'prepare build'
  task :prebuild do
    Dir.mkdir 'book/images' unless Dir.exists? 'book/images'
    Dir.glob("book/*/images/*").each do |image|
      FileUtils.copy(image, "book/images/" + File.basename(image))
    end
  end

  desc 'Generate HTML output'
  task :html => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor book/WaRP7-Software-Guide.adoc`
    puts " -- HTML output at book/WaRP7-Software-Guide.html"
  end

  desc 'Generate EPub output'
  task :epub => :prebuild do
    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 book/WaRP7-Software-Guide.adoc`
    puts " -- Epub output at book/WaRP7-Software-Guide.epub"
  end

  desc 'Generate Mobi (kf8) output'
  task :mobi => :prebuild do
    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -a ebook-format=kf8 book/WaRP7-Software-Guide.adoc`
    puts " -- Mobi output at book/WaRP7-Software-Guide.mobi"
  end

  desc 'Generate PDF output'
  task :pdf => :prebuild do
    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf -a pdf-style=book \
                                 -a pdf-stylesdir=theme/pdf \
                                 book/WaRP7-Software-Guide.adoc`
    puts " -- PDF  output at book/WaRP7-Software-Guide.pdf"
  end

  desc 'Generate PDF using fopub'
  task :pdf_fopub => :prebuild do
    puts "Converting to PDF (using fopub)..."
    `bundle exec asciidoctor -b docbook -d book -a data-uri! book/WaRP7-Software-Guide.adoc`
    `bundle exec fopub book/WaRP7-Software-Guide.xml \
                       -param page.size a5`
    puts " -- PDF  output at book/WaRP7-Software-Guide.pdf"
  end

end

desc 'Build all default formats'
task :build => [ "build:html", "build:epub", "build:mobi", "build:pdf" ]
