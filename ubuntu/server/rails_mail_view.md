### visual mail testing

Sending mail is a very big part in rails apps development. You should make sure mail content displayed correctly.
So mail testing is quite important. Everytime I have to send mail to my personal mail box, find errors,
fix them, send mail. The process is repeated agagin and agagin until the mail is perfect. Now I find a gem
called `mail_view` which really help me out from the bored troubles.

1. add the line below to Gemfile

    gem "mail_view", "~> 1.0.3"

2. create a new file named `mail_preview.rb` in `app/mailers` dir, add following lines to the file.

    <pre><code>class MailPreview < MailView
      def new_ep_release
        user = Struct.new(:email, :name).new("tom@gmail.com", "Tom")
        episode = Episode.last
        HappyMailer.new_ep_release(user, episode.id)
      end
    end</code></pre>

3. add the lines below to route.rb

    <pre><code># config/routes.rb
    if Rails.env.development?
      mount MailPreview => 'mail_view'
    end</code></pre>

4. access `http://localhost:3000/mail_view` to check mail list

### Reference

* https://github.com/basecamp/mail_view

* http://actsasblog.ca/2011/10/06/preview-emails-in-browser-without-sending-in-rails3/
