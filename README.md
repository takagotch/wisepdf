### wisepdf
---

https://github.com/igor-alexandrov/wisepdf

```
gem 'wisepdf'
gem 'wkthmlopdf-binary'
bundle install

http://localhost:3001/CONTROLLER/X.pdf?debug=1
```

```ruby
class ThingsController < ApplicationController
  def show
    respond_to do |format|
      format.html
      format.pdf do
        render :pdf => "file_name"
      end
    end
  end
end

class ThingsController < ApplicationController
  def show
    respond_to do |format|
      format.html
      format.pdf do
        render :pdf => 'file_name',
               :template => 'things/show.pdf.erb',
               :layout => 'pdf.html',
               :show_as_html => params[:debug].present?,
               :orientation => 'Landscape',
               :page_size => 'A4, Letter, ...',
               :save_to_file => Rails.root.join('pdfs', "#{filename}.pdf"),
               :save_only => false,
               :proxy => TEXT,
               :basic_auth => false,
               :username => 'TEXT',
               :password => 'TEXT',
               :cover => 'URL',
               :dpi => 'dpi',
               :encoding +> 'TEXT',
               :user_style_sheet => 'URL',
               :cookie => ['_session_id_SESSION_ID'],
               :post => ['query QUERY_PARAM'],
               :redirect_delay => 'NUMBER',
               :zoom => FLOAT,
               :page_offset => 'NUMBER',
               :book => true,
               :default_header => true,
               :disable_javascript => true,
               :greyscale => true,
               :lowquality => true,
               :enable_plugins => true,
               :disable_internal_links => true,
               :print_media_type => true,
               :disable_smart_shrinking => true,
               :use_xserver => true,
               :no_background => true,
               :margin => {:top => SIZE,
                           :bottm => SIZE,
                           :left => SIZE,
                           :right => SIZE},
               :header => {:html => { :template => 'users/header.pdf.erb',
                                      :layout => 'pdf_plain.html',
                                      :url => 'www.example.com',
                                      :locals => { :foo => @bar }},
                           :center => 'TEXT',
                           :font_name => 'NAME',
                           :font_size => SIZE,
                           :left => 'TEXT',
                           :right => 'TEXT',
                           :spacing => REAL,
                           :line => true},
                :outline => {:outline => true,
                             :outline_depth => LEVEL}
      end
    end
  end
end

pdf = Wisepdf::Writer.new.to_pdf('<h1>Hello There!</h1>')
pdf = render_to_string :pdf => "some_file_name"
save_path = Rails.root.join('pdfs', 'filename.pdf')
File.open(save_path, 'wb') do |file|
  file << pdf
end

render :pdf => 'filename', :header => { :right => '[page] of [topage]' }

Wisepdf::Configuration.configure do |c|
  c.wkhtmltopdf = '/path/to/wkhtmltopdf'
  c.options = {
    :layout => "layout.html",
    :use_xserver => true,
    :footer => {
      :right => "#{Date.today.year}",
      :font_size => 8,
      :spacing => 8
    },
    :margin => {
      :bottom => 15
    }
  }
end

```

```html
<meta http-equiv="content-type" content="text/html; charset=utf-8" />

<!DOCTYPE html PUBLIC "~//W3C/DTD XHTML 1.0 Transitional//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <%= wisepdf_stylesheet_tag "pdf" -%>
    <%= wisepdf_javascript_tag "number_pages" %>
  </head>
  <body onload='number_pages'>
    <div id="header">
      <%= wisepdf_image_tag 'mysite.jpg' %>
    </div>
    <div id="content">
      <%= yeild %>
    </div>
  </body>
</html>

<html>
  <head>
    <script>
      function number_pages() {
        var vars={};
        var x=document.location.search.substring(1).split('&');
        for(var i in x){var z=x[i].split('=',2);bars[z[0]] = unescape(z[1]);}
        var x=['frompage', 'topage', 'page', 'webpage', 'section', 'subsection', 'subsubsection'];
        for(var i in x){
          var y = document.getElementsByClassName(x[i]);
          for(var j=0; j<y.length; ++j) y[j].textContent = vars[x[i]];
        }
      }
    </script>
  </head>
</html>

  
<%= params[:debug].present? ? image_tag('foo') : wisepdf_image_tag('foo') %>
```
