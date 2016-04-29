namespace :build do
  desc 'prepare build'
  task :prebuild do
    Dir.mkdir 'Software_Guide/images' unless Dir.exists? 'Software_Guide/images'
    Dir.glob("Software_Guide/*/images/*").each do |image|
      FileUtils.copy(image, "Software_Guide/images/" + File.basename(image))
    end
    Dir.mkdir 'Hardware_Guide/images' unless Dir.exists? 'Hardware_Guide/images'
    Dir.glob("Hardware_Guide/*/images/*").each do |image|
      FileUtils.copy(image, "Hardware_Guide/images/" + File.basename(image))
    end
  end

  desc 'Generate HTML outputs'
  task :html => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor Software_Guide/WaRP7-Software-Guide.adoc`
    puts " -- HTML output at Software_Guide/WaRP7-Software-Guide.html"
  end
  task :html => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor Hardware_Guide/WaRP7-Hardware-Guide.adoc`
    puts " -- HTML output at Hardware_Guide/WaRP7-Hardware-Guide.html"
  end
  task :html => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor App_Notes/WaRP7-App_Note.adoc`
    puts " -- HTML output at App_Notes/WaRP7-App_Note.html"
  end

  desc 'Generate EPub outputs'
  task :epub => :prebuild do
    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 Software_Guide/WaRP7-Software-Guide.adoc`
    puts " -- Epub output at Software_Guide/WaRP7-Software-Guide.epub"
  end
  task :epub => :prebuild do
    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 Hardware_Guide/WaRP7-Hardware-Guide.adoc`
    puts " -- Epub output at Hardware_Guide/WaRP7-Hardware-Guide.epub"
  end
  task :epub => :prebuild do
    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 App_Notes/WaRP7-App_Note.adoc`
    puts " -- Epub output at App_Notes/WaRP7-App_Note.epub"
  end

  desc 'Generate Mobi (kf8) outputs'
  task :mobi => :prebuild do
    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -a ebook-format=kf8 Software_Guide/WaRP7-Software-Guide.adoc`
    puts " -- Mobi output at Software_Guide/WaRP7-Software-Guide.mobi"
  end
  task :mobi => :prebuild do
    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -a ebook-format=kf8 Hardware_Guide/WaRP7-Hardware-Guide.adoc`
    puts " -- Mobi output at Hardware_Guide/WaRP7-Hardware-Guide.mobi"
  end
  task :mobi => :prebuild do
    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -a ebook-format=kf8 App_Notes/WaRP7-App_Note.adoc`
    puts " -- Mobi output at App_Notes/WaRP7-App_Note.mobi"
  end

  desc 'Generate PDF outputs'
  task :pdf => :prebuild do
    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf -a pdf-style=book \
                                 -a pdf-stylesdir=theme/pdf \
                                 Software_Guide/WaRP7-Software-Guide.adoc`
    puts " -- PDF  output at Software_Guide/WaRP7-Software-Guide.pdf"
  end
  task :pdf => :prebuild do
    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf -a pdf-style=book \
                                 -a pdf-stylesdir=theme/pdf \
                                 Hardware_Guide/WaRP7-Hardware-Guide.adoc`
    puts " -- PDF  output at Hardware_Guide/WaRP7-Hardware-Guide.pdf"
  end
  task :pdf => :prebuild do
    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf -a pdf-style=book \
                                 -a pdf-stylesdir=theme/pdf \
                                 App_Notes/WaRP7-App_Note.adoc`
    puts " -- PDF  output at App_Notes/WaRP7-App_Note.pdf"
  end

  desc 'Generate PDF using fopub'
  task :pdf_fopub => :prebuild do
    puts "Converting to PDF (using fopub)..."
    `bundle exec asciidoctor -b docbook -d book -a data-uri! Software_Guide/WaRP7-Software-Guide.adoc`
    `bundle exec fopub Software_Guide/WaRP7-Software-Guide.xml \
                       -param page.size a5`
    puts " -- PDF  output at Software_Guide/WaRP7-Software-Guide.pdf"
  end
  task :pdf_fopub => :prebuild do
    puts "Converting to PDF (using fopub)..."
    `bundle exec asciidoctor -b docbook -d book -a data-uri! Hardware_Guide/WaRP7-Hardware_Guide.adoc`
    `bundle exec fopub Hardware_Guide/WaRP7-Hardware-Guide.xml \
                       -param page.size a5`
    puts " -- PDF  output at Hardware_Guide/WaRP7-Hardware-Guide.pdf"
  end
  task :pdf_fopub => :prebuild do
    puts "Converting to PDF (using fopub)..."
    `bundle exec asciidoctor -b docbook -d book -a data-uri! App_Notes/WaRP7-App_Note.adoc`
    `bundle exec fopub App_Notes/WaRP7-App_Note.xml \
                       -param page.size a5`
    puts " -- PDF  output at App_Notes/WaRP7-App_Note.pdf"
  end

end

desc 'Build all default formats'
task :build => [ "build:html", "build:epub", "build:mobi", "build:pdf" ]
