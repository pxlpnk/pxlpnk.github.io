---
layout: post
title: "Create an interactive console for your library with Pry"
date: 2014-03-07 23:56
author: at
categories:
- ruby
- pry

---
When working on a library written in Ruby the interactive part of trying and using it during development is sometimes hard and painful.
Tools like [irb][1] and [Pry][2] can help here a lot.
In general every RubyGem should have a console to have your library right at your fingertips.
This makes learning the API and becoming a look and feel way easier if someone wants to use your code or contribute to it.

The easiest way to do this with Pry is to push your models into the load path, require them and start a Pry command line.

```ruby ./bin/console.rb
#!/usr/bin/env ruby
$LOAD_PATH << 'lib'
require 'your_models'
require 'pry'

Pry::CLI.parse_options
```
In combination with [pry-rescue][3] and [pry-debugger][4] or [pry-byebug][5] this turns into a very powerful tool to speedup your development process.
Within the console predefined structures and objects can be created to DRY up your workflow.


[1]: http://www.ruby-doc.org/stdlib-2.0/libdoc/irb/rdoc/IRB.html
[2]: http://pryrepl.org/
[3]: https://github.com/ConradIrwin/pry-rescue
[4]: https://github.com/nixme/pry-debugger
[5]: https://github.com/deivid-rodriguez/pry-byebug
[6]: http://blog.jayfields.com/2014/01/repl-driven-development.html
