---
layout: post
title:      "Makefile 004: Rails Project--Lessons Learned"
date:       2020-02-17 14:29:30 +0000
permalink:  makefile_004_rails_project--lessons_learned
---


While doing my Rails project for Flatiron School, I learned a lot (not giving up being on the top of the list!). I'd like to share a few problems I had and how I overcame them.

## Overview

My app is called "I Remember When". It allows users to make entries of events in recent history and to write their own memories of them. It has three models: User, Event, and Memory.

## Lesson 1: Manipulating Dates

I wanted to allow a user to specify the date an Event happened by selecting from Day, Month, and Year dropdowns. Then, I wanted to combine these 3 values into a single datetime value in the events table so events can be chronologically sorted. Finally, the date of each event should be displayed in views in a user-friendly format.

In a form_with set to `model: @event` we have 3 dropdowns from 1 date_select.

*app/views/events/_form.html.erb):*

```ruby
  <%= f.label :date %>:
  <%= f.date_select("date", start_year: 1900, end_year: Date.today.year, order: [:day, :month, :year], prompt: { day: 'Select Day', month: 'Select Month', year: 'Select Year'}) %>
```

Selecting "13", "June", and "1945" produces these params:

```
  "event"=>{"name"=>"Sample Event", "date(3i)"=>"13", "date(2i)"=>"6", "date(1i)"=>"1945", "country"=>"Barbados", "description"=>"Sample description."}
```

We can include these in event_params with this method in events_controller.rb:

```ruby
  def event_params
    params.require(:event).permit(:name, :'date(3i)', :'date(2i)', :'date(1i)', :country, :description)
  end
```

As you can see, each of the date params is wrapped in quotes. Otherwise we get: `syntax error, unexpected '(', expecting ')'` when '(' is encountered.

We can check to make sure a day, month, and year have all been selected by writing a class method on Event:

```ruby
    def self.date_present?(event_params)
      %w[1 2 3].map { |element| event_params["date(#{element}i)"] }.to_a.none? { |element| element == '' }
    end
```

Here, we access each of the date values in the event_params hash by iterating over the elements of an array of the numbers 1-3 to construct the keys for those values through string interpolation, convert the results into an array, then check if any of the elements of this array are empty strings. (This guards against having an argument error if we try to pass invalid arguments to Date.new later.)

We can convert the date string values in event_params to integers with another class method on Event:

```ruby
    def self.convert_date(event_params)
      %w[1 2 3].map { |element| event_params["date(#{element}i)"].to_i }
    end
```

In action:

```ruby
  Event.convert_date(event_params)
  => [1945, 6, 13]
```

Then, we bring it all together in #create in events_controller:

```ruby
    date = Date.new(*Event.convert_date(event_params)) if Event.date_present?(event_params)
    @event = Event.new(name: event_params[:name], country: event_params[:country], description: event_params[:description], user_id: current_user.id, date: date)
```

In action:

```ruby
  date = Date.new(*Event.convert_date(event_params))
=> Wed, 13 Jun 1945
```

The combined date will be validated in Event.rb:

```ruby
  validates :date, presence: true
```

To nicely format the date in views, we can make a view helper using Ruby's #strftime method:

*application_helper.rb:*

```ruby
  def format_date(date)
    date.strftime('%B %e, %Y')
  end
```

Yields:

`June 13, 1945`

## Lesson 2: Guard Clauses

The handy Rubocop gem taught me how to use a guard clause instead of an 'if' conditional. I originally had this method in registrations_controller.rb:

```ruby
  def check_admin_key
    if params[:admin_key] != ""
      if params[:admin_key] == ENV["ADMIN_KEY"]
        @user.admin = true
        @user.save
        flash[:notice] = "Admin account established!"
      else
        flash[:alert] = "Admin key not recognized. Please update account to have admin status."
      end
    end
  end
```

As you can see, there's an if...end nested in an if...end. (Sometimes, this kind of nesting can get pretty deep.) To make the code a bit shorter and easier to read, we can replace the outer if conditional with a `return unless` guard clause:

```ruby
  def check_admin_key
    return unless params[:admin_key] != ''

    if params[:admin_key] == ENV['ADMIN_KEY']
      @user.admin = true
      @user.save
      flash[:notice] = 'Admin account established!'
    else
      flash[:alert] = 'Admin key not recognized. Please update account to have admin status.'
    end
  end
```

This way, if the user has not entered anything in the admin_key field, none of the rest of the method will be executed.

## Lesson 3: link_to Styled as a Button

I wanted to have buttons placed horizontally in a view. To do so, and take advantage of Rails helper methods at the same time, I learned how to use link_to styled as a button. (We might be tempted to use button_to for this, but be warned, this arranges the buttons vertically.) For instance, in my Memory show view I have:

```ruby
  <p><%= link_to 'Edit', edit_memory_path(@memory), class: "btn btn-outline-dark btn-sm" %> <%= link_to 'Delete', memory_path(@memory), method: :delete, class: "btn btn-outline-dark btn-sm" %><p>
```

Here I use path helpers and specify a method (necessary for delete.) I make the links look like buttons by specifying some Bootstrap styles.

## Conclusion

These are just a few of many things I learned putting together my first solo Rails app. The experience has given me a taste of possibilities Rails opens up, with more being created as the framework continues to develop.

