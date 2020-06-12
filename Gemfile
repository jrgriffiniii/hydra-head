source "https://rubygems.org"

gem 'rspec-its'

# Specify gem dependencies in hydra-head.gemspec
gemspec

# BEGIN ENGINE_CART BLOCK
file = File.expand_path('Gemfile', ENV['ENGINE_CART_DESTINATION'] || ENV['RAILS_ROOT'] || File.expand_path('.internal_test_app', File.dirname(__FILE__)))
if File.exist?(file)
  begin
    eval_gemfile file
  rescue Bundler::GemfileError => e
    Bundler.ui.warn '[EngineCart] Skipping Rails application dependencies:'
    Bundler.ui.warn e.message
  end
else
  Bundler.ui.warn "[EngineCart] Unable to find test application dependencies in #{file}, using placeholder dependencies"

  if ENV['RAILS_VERSION']
    if ENV['RAILS_VERSION'] == 'edge'
      gem 'rails', github: 'rails/rails'
      ENV['ENGINE_CART_RAILS_OPTIONS'] = '--edge --skip-turbolinks'
    else
      gem 'rails', ENV['RAILS_VERSION']
    end

    case ENV['RAILS_VERSION']
    when /^6\.0/
      gem 'active-fedora', git: 'https://github.com/jrgriffiniii/active_fedora.git', branch: 'faraday-dependency'
      gem 'activesupport', '~> 6.0'
      # gem 'faraday', '~> 0.11'
      gem 'faraday', '0.9.0'

    when /^5.[12]/
      gem 'rails-controller-testing'
      gem 'sass-rails', '~> 5.0'

    when /^4.2/
      gem 'responders', '~> 2.0'
      gem 'sass-rails', '>= 5.0'
      gem 'coffee-rails', '~> 4.1.0'

    when /^4.[01]/
      gem 'sass-rails', '< 5.0'
    end
  else
    gem 'rails-controller-testing'
  end
end
# END ENGINE_CART BLOCK
