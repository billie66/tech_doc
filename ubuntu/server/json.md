### apply .html.erb partial to .json.erb template

    <% self.formats = ["html"] %>
    disclaimer = {
      "html":"<%= sanitize escape_javascript(render :partial => 'projects/disclaimer',
                  :content_type => 'text/html'),
                  :locals => {:localVariable => @localVariable}
              %>"
    }

* http://stackoverflow.com/questions/5401696/json-erb-template-cannot-find-other-html-partial
