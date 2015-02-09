# RenderAsync

See doc in wiki https://github.com/apneadiving/AsyncPartial/wiki

##Prerequisites:

* Rails 3

* jQuery

* `yield :scripts` in your footer

##How to use:

###Basic
In your view:

    <%= async_partial :partial_name %>

This will assume:

* the partial is at the root of the current controller, and it's name is `_partial_name`

### Advanced

In your view:

    <%= async_partial "/shared/my_partial", :controller => "feeds", :action => "retrieve_feeds", :options => { :user_id => 1 } %>

Everything you pass in `options` will be available in the controller's params.

In your `FeedsController`:

    #you must declare your method with (params)
    def retrieve_feeds(params)
      #return a hash with whatever you want
      #All variables you pass there will be available as locals in your partial
      { :feeds => Feed.find_feeds_of_user(params[:user_id]) }
    end

In your partial `/shared/my_partial`:

    <% feeds.each do |feed| %>
       <div> Feed: <%= feed.content %> </div>
    <% end %>

###Notes

When you do `<%= async_partial :partial_name %>`, the existence of the method `partial_name` is automatically checked.

And your hash of locals is retrieved from it if existence confirmed.
