RUBY := $(shell command -v ruby 2>/dev/null)
HOMEBREW := $(shell command -v brew 2>/dev/null)
BUNDLER := $(shell command -v bundle 2>/dev/null)

default: setup

setup: \
	pre_setup \
	check_for_ruby \
	check_for_homebrew \
	install_bundler \
	install_gems \
	install_ios_dependencies

setup_circle: \
	install_gems \
	install_ios_dependencies

pre_setup:
	$(info ------------------------------)
	$(info iOS project setup ...)
	$(info ------------------------------)

check_for_ruby:
	$(info )
	$(info Checking for Ruby ...)

ifeq ($(RUBY),)
	$(error Ruby is not installed)
endif

check_for_homebrew:
	$(info )
	$(info Checking for Homebrew ...)

ifeq ($(HOMEBREW),)
	$(error Homebrew is not installed)
endif

install_bundler:
	$(info )$(info Checking and install bundler ...)

ifeq ($(BUNDLER),)
	gem install bundler -v '~> 2.0'
else
	gem update bundler '~> 2.0'
endif

install_gems:
	$(info )$(info Install Ruby Gems ...)

	bundle install --without=documentation

install_ios_dependencies:
	$(info Install iOS dependencies ...)
	bundle exec fastlane carthage_ci

	bundle exec pod install --repo-update

update:
	$(info Updating iOS dependencies ...)
	bundle exec fastlane run_rome_update

test:
	bundle exec fastlane test_iphone_pro
