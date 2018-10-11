### wisepdf
---

https://github.com/igor-alexandrov/wisepdf

```
gem 'wisepdf'
gem 'wkthmlopdf-binary'
bundle install


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
        render :pdf => '',
               :template => '',
               :layout => '',
               :show_as_html => params[].present?,
               :orientation => '',
               :page_size => '',
               :save_to_file => Rails.root.join(),
               :save_only => false,
               :proxy => false,
               :basic_auth => false,
               :username => '',
               :password => '',
               :cover => '',
               
      end
    end
  end
end

pdf = Wisepdf::Writer.new.to_pdf()
pdf = render_to_string :pdf => ""
save_path = Rails.root.join()
File.open() do |file|
  file << pdf
end

render :pdf => '', :header => {}

Wisepdf::Configuration.configure do |c|
end

```

```html
<meta http-equiv="content-type" content="text/html; charset=utf-8" />

<!DOCTYPE html PUBLIC ""
  "">
<html xmlns="" xml:lang="" lang="">
  <head>
  </head>
  <body onload=''>
  </body>
</html>


<%= params[].present? ? image_tag() : wisepdf_image_tag('foo') %>
```
