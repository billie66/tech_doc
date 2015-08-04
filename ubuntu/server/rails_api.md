#### delete all table records of a User model

    User.delete_all

#### timezone

* Automatic time zone conversion is enabled

http://makandracards.com/makandra/646-how-rails-and-mysql-are-handling-time-zones

#### ActiveModel::Dirty

http://craftingruby.com/posts/2014/01/13/callbacks-and-dirty-objects-in-rails.html

### rails migration

* change a column type

    class ChangeProductsPrice < ActiveRecord::Migration
      def up
        change_table :products do |t|
          t.change :price, :string
        end
      end

      def down
        change_table :products do |t|
          t.change :price, :integer
        end
      end
    end

* hidden_field

    <%= form_for order do |f| %>
      <%= f.hidden_field :course_id, value: course.id %>
      <%= f.submit %>
    <% end %>

* to_s

    Loading development environment (Rails 4.1.6)
    irb(main):001:0> Time.now.to_s :number
    => "20150726132302"

