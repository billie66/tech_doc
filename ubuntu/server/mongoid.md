### Manage mongodb with mongoid in rails console

The rails damo app named store, has two models, user and node. The
relationship between the two models is one-to-many, that is, a user has many
nodes, and a node belongs to a user. The node model has two attributes, title
and description respectively, which are all localizable.

    billie@kitty:~/store$ rails c
    Loading development environment (Rails 3.2.13)
    irb(main):001:0> u = User.first
    irb(main):001:0> I18n.locale
    => :en
    irb(main):008:0> node = u.nodes.new
    => #<Node _id: 5163cfa3cd880ba3e1000001, created_at: nil, updated_at: nil,
    title: nil, description: nil, _slugs: [], user_id: "516142f6cd880b6d0b000003">
    irb(main):009:0> node.title="Fruit"
    => "Fruit"
    irb(main):010:0> node.attributes
    => {"_id"=>"5163cfa3cd880ba3e1000001", "_slugs"=>[],
    "user_id"=>"516142f6cd880b6d0b000003", "title"=>{"en"=>"Fruit"}}
    irb(main):011:0> I18n.locale = "zh-CN"
    => "zh-CN"
    irb(main):012:0> node.title="水果"
    => "水果"
    irb(main):013:0> node
    => #<Node _id: 5163cfa3cd880ba3e1000001, created_at: nil, updated_at: nil,
    title: {"en"=>"Fruit", "zh-CN"=>"水果"}, description: nil, _slugs: [], user_id: "516142f6cd880b6d0b000003">
    irb(main):014:0> node.description_translations={"en"=>"everyone love them.", "zh-CN"=>"人人喜爱水果."}
    => {"en"=>"everyone love them.", "zh-CN"=>"人人喜爱水果."}
    irb(main):015:0> node
    => #<Node _id: 5163cfa3cd880ba3e1000001, created_at: nil, updated_at: nil,
    title: {"en"=>"Fruit", "zh-CN"=>"水果"}, description: {"en"=>"everyone
    love them.", "zh-CN"=>"人人喜爱水果."}, _slugs: [], user_id: "516142f6cd880b6d0b000003">
    irb(main):016:0> node.save
    => true
    irb(main):017:0> u.nodes.count
    => 4
    irb(main):018:0> node.update_attribute(:title, "瓜果")
    => true
    irb(main):019:0> I18n.locale
    => :"zh-CN"
    irb(main):020:0> node
    => #<Node _id: 5163cfa3cd880ba3e1000001, created_at: 2013-04-09 08:29:03
    UTC, updated_at: 2013-04-09 08:31:59 UTC, title: {"en"=>"Fruit",
    "zh-CN"=>"瓜果"}, description: {"en"=>"everyone love them.",
    "zh-CN"=>"人人喜爱水果."}, _slugs: ["shui-guo"], user_id: "516142f6cd880b6d0b000003">
    irb(main):020:0> node.delete
    => true
    irb(main):001:0> I18n.locale = :en
    => :en
    irb(main):001:0> u.nodes.first
    irb(main):001:0> u.nodes.second
    ....
    ....
    irb(main):001:0> u.nodes.last
    irb(main):001:0> u.nodes.delete_all(title: "fruit")
    irb(main):001:0> u.nodes.last.update_attributes(title: "fruit", description: "we all love fruit.")

The details, please refer to official documents [mongoid](http://mongoid.org/en/mongoid/docs/documents.html).
    
