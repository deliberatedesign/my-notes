# Ruby: Convert Strings to Url

#### URI encode

```ruby
require 'uri'

URI::encode("Friedrichtraße 123, Berlin, Germany")
#=> "Friedrichtra%C3%9Fe%20123,%20Berlin,%20Germany"
```

```ruby
require 'uri'
uri_string = URI::encode("http://localhost:3000/stuff?owner=foo bar+type=video game")
```


#### CGI escape 

```ruby
require 'cgi'

CGI.escape('Friedrichtraße 123, Berlin, Germany')
# => "Friedrichtra%C3%9Fe+123%2C+Berlin%2C+Germany"
```

#### Rails routes

```ruby
home_path(:address => 'Friedrichtraße 123, Berlin, Germany')
```
