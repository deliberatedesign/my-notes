# Rails: Active Record

## Create

```ruby
@new_user = User.new
```

#### Create will create and save a new record into the database
```ruby
user = User.create(name: "David", occupation: "Code Artist")
```

#### Using the new method, an object can be instantiated without being saved
```ruby
user = User.new
user.name = "David"
user.occupation = "Code Artist"
```

#### If a block is provided, both create and new will yield the new object to that block for initialization
```ruby
user = User.new do |u|
  u.name = "David"
  u.occupation = "Code Artist"
end
```

## Read

```ruby
users = User.all
```

```ruby
# return the first user
user = User.first
```

```ruby
# return the first user named David
david = User.find_by(name: 'David')
```

```ruby
users = User.where(:occupation => @occupation.id).ids
```

```ruby
# find all users named David who are Code Artists and sort by created_at in reverse chronological order
users = User.where(name: 'David', occupation: 'Code Artist').order(created_at: :desc)
```


## Update

```ruby
user = User.find_by(name: 'David')
user.name = 'Dave'
user.save
```

```ruby
user = User.find_by(name: 'David')
user.update(name: 'Dave')
```

```ruby
User.update_all "max_login_attempts = 3, must_change_password = 'true'"
```

## Delete

```ruby
user = User.find_by(name: 'David')
user.destroy
```

```ruby
# find and delete all users named David
User.destroy_by(name: 'David')
 
# delete all users
User.destroy_all
```

## Validation

```ruby
class User < ApplicationRecord
  validates :name, presence: true
end
 
user = User.new
user.save  # => false
user.save! # => ActiveRecord::RecordInvalid: Validation failed: Name can't be blank
```

## Other Examples

```ruby
# controller.rb

def mark_all_read(user)
  user.events.update_all("read = true")
  redirect_back(fallback_location: root_path)
end
helper_method :mark_all_read
```

```ruby
# controller.rb

def mark_read(event_id)
  selected_event = Event.where(id: event_id).first
  selected_event.update_attribute(:read, true)
  redirect_back(fallback_location: root_path)
end
helper_method :mark_read
```
