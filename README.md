# CrispClient

:small_red_triangle_down: Ruby Client for Crisp API

## Usage

```ruby
cc = CrispClient::Base.new(email: ENV['CRISP_EMAIL'], password: ENV['CRISP_PASSWORD'])
cc.authenticate
#=> {"Authorization"=>"Basic MmjjiyAjSLuMmjjiyAjSLuMmjjiyAjSLuMmjjiyAjSLuMmjjiyAiaiIyMGUyYTdjYzA="}

website_id = cc.find_website_id_by_name(website_name: "Touts")
#=> "8sajk18272-4aab-kjhh-bkjh-8e3chjk5609"

cc.get_people_statistics(website_id: website_id)
#=> {"total"=>3523}

person_id = cc.add_new_people_profile(website_id: website_id, nickname: "Flavio Wuensche", email: "flavio@touts.com.br")
#=> "cd71e876-62e4-17hs-b6c2-570f44b3d83b"
cc.add_new_people_profile(website_id: website_id, nickname: "Flavio Wuensche", email: "flavio@touts.com.br")
#=> RuntimeError: people_exists

cc.remove_people_profile(website_id: website_id, people_id: person_id)
#=> "deleted"
cc.remove_people_profile(website_id: website_id, people_id: person_id)
#=> "people_not_found"

cc.list_people_profiles(website_id: website_id)
#=> will return the first 20 users by default
cc.list_people_profiles(website_id: website_id, page_number: 2, search_filter: "test@email.com")
#=> will return the next 20 users
# Other parameters you can use include: sort_field, sort_order, search_operator, search_filter
# The search_filter parameter is to be used exactly as in the dashboard, as in: "&search_filter="parameter"

cc.update_conversation_metas website_id: website_id, session_id: session_id, 
									meta: { nickname: "test nickname", email: "test@email.com", phone: "9999-9999", 
													address: "rua teste 99t", segments: ["segmento 1", "segmento 2"], 
									data: { teste_data: "data_teste_3", valorArbitrario: "teste arbitrário 3" } }
# Updates the metadata from a specific conversation, given a session_id
# Remember that conversation metadata is not equal to profile metadata. Each conversation has their own parameters.

cc.update_people_profile website_id: website_id, people_id: people_id, 
  								profile_data: { person: { phone: "9999-9999", nickname: "test nickname 2", 
                                                address: "rua teste 99t", website: "http://teste.com"},
                                    segments: ["segmento 4", "segmento 3"], 
                                    company: { name: "Empresa teste" },
                                    geolocation: { city: "Cidade teste" } }
# Updates a user's profile data. This is what you see when you click in a specific profile.

```

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'crisp_client'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install crisp_client

## Development

After checking out the repo, run `bin/setup` to install dependencies. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/crisp_client.

While debugging you might need to reload edited files:

```ruby
load '/Users/fwuensche/www/crisp_client/lib/crisp_client/website_people.rb'
```

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).
