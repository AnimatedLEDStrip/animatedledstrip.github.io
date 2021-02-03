---
title: Ruby
parent: Client Libraries
grand_parent: Clients
---

[GitHub Repo](https://github.com/AnimatedLEDStrip/client-ruby){: .btn }

# AnimatedLEDStrip Client Library for Ruby

This library allows a Ruby client to communicate with an AnimatedLEDStrip server.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'animatedledstrip-client'
```

Or install with:

```bash
$ gem install animatedledstrip-client
```

## Creating an `ALSHttpClient`

A new client is created with `ALSHttpClient(ip_address)`.

```ruby
client = ALSHttpClient.new("10.0.0.254")
```

## Communicating with the Server

This library follows the conventions laid out for [AnimatedLEDStrip client libraries](/clients/client-libraries), with the following modifications:

- Function names and class variables are in snake case to follow Ruby style conventions
- `get_supported_animations_hash` is provided as an alias for `get_supported_animations_map`
- `get_sections_hash` is provided as an alias for `get_sections_map`
