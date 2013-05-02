# .bin

Becoming craftsman.

## Installation

``` sh
export PATH=~/.bin:$PATH
mkdir ~/.bin
echo "echo 'Hello world'" > ~/.bin/hello_world
echo "#\!/bin/sh\necho 'Hello world\!'" > ~/.bin/hello_world
chmod +x ~/.bin/hello_world
hello_world
#=> Hello world!
```

## Example of usage

Like pomodoro technique? Awesome, me too. Let's build own pomodoro timer.

### Preparing

Let's create blank ruby script:

`~/.bin/pomo`:
``` ruby
#!/usr/bin/env ruby
puts 'Hello world!'
```

Make it executable:

``` sh
chmod +x ~/.bin/pomo
```

### Let's write some code

``` ruby
#!/usr/bin/env ruby

require 'rubygems'
require 'main'

MINUTES = 60

Main {
  def run
    while true
      puts 'Lets work!'
      
      rules.each do |rule|
        puts rule[:title]
        
        rule.minutes do |minutes_pass|
          minutes_left = rule.minutes - minutes_pass
          puts "#{minutes_left} left"
          sleep MINUTE
        end
      end
    end
  end

  def rules
    [{ title: "Let's work", minutes: 25 },
     { title: "Let's rest", minutes: 5 }]
  end
}
```

### Done.

Now you are master.
