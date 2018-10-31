# Logstash Plugin

This is a plugin for [Logstash](https://github.com/elastic/logstash).

It is fully free and fully open source. The license is Apache 2.0, meaning you are pretty much free to use it however you want in whatever way.

## Installation

This plugin is available on RubyGems https://rubygems.org/gems/logstash-filter-sanitize_mac so we can install it via the logstash command

```sh
/usr/share/logstash/bin/logstash-plugin install logstash-filter-sanitize_mac
```

## Use in logstash

```sh
  if [program] == "radiusd" {

    grok {
      patterns_dir => "/etc/logstash/patterns/radiuslog"
      match => [ "syslog_message", "%{FREERADIUS}" ]
    }

    mutate {
      add_field => { "type_log" => "radius-log" }
      remove_field => [ "message" ]
      remove_field => [ "syslog_message" ]
      remove_tag => [ "syslog_message_unparsed" ]

    }

    sanitize_mac {
      match => { "radius_client_mac" => "radius_client_mac_clean" }
      fixcase => "lower"
      separator => ":"
    }

  }
```


## Contributing

All contributions are welcome: ideas, patches, documentation, bug reports, complaints, and even something you drew up on a napkin.

Programming is not a required skill. Whatever you've seen about open source and maintainers or community members  saying "send patches or die" - you will not see that here.

It is more important to the community that you are able to contribute.

For more information about contributing, see the [CONTRIBUTING](https://github.com/elastic/logstash/blob/master/CONTRIBUTING.md) file.
