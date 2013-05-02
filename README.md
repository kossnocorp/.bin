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

Let's create blank ruby script (`~/.bin/pomo`):

``` ruby
#!/usr/bin/env ruby
puts 'Hello world!'
```

Make it executable:

``` sh
chmod +x ~/.bin/pomo
```

### Let's write some code

We need to write prototype for 5 minutes. Let's do it:

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
        
        rule[:minutes] do |minutes_pass|
          minutes_left = rule[:minutes] - minutes_pass
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

### Improve it

Now things goes compicated:

``` ruby
#!/usr/bin/env ruby

require 'rubygems'
require 'main'
require 'talks'

MINUTE = 60

class Timer
  class << self
    def start!(minutes, &draw)
      minutes_left = minutes

      while minutes_left > 0 do
        draw.call(minutes_left) if block_given?
        minutes_left -= 1
        sleep MINUTE
      end
    end
  end
end

Main {
  def run
    while true
      rules.each do |rule|
        puts rule[:title]

        Timer.start!(rule[:minutes]) do |minutes_left|
          timer_report minutes_left
        end
      end
    end
  end

  def rules
    [{ title: "Let's work", minutes: 25 },
     { title: "Let's rest", minutes: 5 }] * 4 +
    [{ title: "Let's walk for 15 minutes", minutes: 15 }]
  end

  def say(text)
    puts text
    Talks.say text
  end

  def timer_report(minutes_left)
    say minutes_left

    File.open(File.expand_path('~/.pomo_stat'), 'w') do |f|
      f.write("#{minutes_left} minutes left")
    end
  end
}
```

### Done.

Now you have to go and done some awesome work using brand new tool.


## License

Anything you want. But I'm not responsible.
