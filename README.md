DaData API JS client for Rails Asset Pipeline
=============================================

[JS client for DaData API servise as jQuery plugin] [plugin] by [@gordienko] [author] packaged for Ruby on Rails asset pipeline.

Installation
------------

Add this line to your application's Gemfile:

    gem 'jquery-dadata-rails', github: 'raveman/jquery-dadata-rails'

And then execute:

    $ bundle

Add this line to `app/assets/stylesheets/application.css`:

    *= require jquery.suggestions.min

Add this line to `app/assets/javascripts/application.js`:

    //= require jquery.suggestions.min

Usage
-----

    <input id="address" name="address" type="text" />
    
    <script>
        $("#address").suggestions({
            token: "aec1d68bf398bd3b46d75454985508be3d8185e6",
            type: "ADDRESS",
            count: 5,
            /* Вызывается, когда пользователь выбирает одну из подсказок */
            onSelect: function(suggestion) {
              $('#company_postal_code').val(suggestion.data.postal_code);
              $('#company_okato').val(suggestion.data.okato);
              $('#company_oktmo').val(suggestion.data.oktmo);
                console.log(suggestion);
            }
        });
    </script>

Аdd similar code to your view, for example `app/views/companies/_form.html.haml`:

    = simple_form_for(@company) do |f|
      = f.error_notification
      = f.input :name
      = f.input :address
      = f.input :postal_code
      = f.input :okato, :as => :hidden
      = f.input :oktmo, :as => :hidden

    :javascript
      $("#company_address").suggestions({
          serviceUrl: "https://dadata.ru/api/v2",
          token: "#{ENV['DADATA_API_KEY']}",
          type: "ADDRESS",
          count: 5,
          onSelect: function(suggestion) {
              $('#company_postal_code').val(suggestion.data.postal_code);
              $('#company_okato').val(suggestion.data.okato);
              $('#company_oktmo').val(suggestion.data.oktmo);
          }
      });


See the original [plugin] README and official [examples].

Contributing
------------

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

### Version policy

This gem version number is in form of **X.Y.Z.P**, where **X.Y.Z** is a version of original [plugin] and **P** is a gem-specific patch level.

[plugin]: https://github.com/gordienko/jquery-dadata-rails
[author]: https://github.com/gordienko
