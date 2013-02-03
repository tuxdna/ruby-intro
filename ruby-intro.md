#An introduction to...
##The Ruby Programming Language

![logo](logo.gif)

#Saleem Ansari
    twitter: tuxdna

#22nd March, 2012 at Red Hat, Pune (India)

---
# Outline
## A bit of history
## Ruby - getting started
## Basic data types and variables
## Basic IO
## Control Structures
## Regular Expressions
## Methods ( or functions )
## Object Oriented Programming
## Modules and Mix-Ins
## Gems
## Additional Topics

---
#Historical perspective on Ruby?
## 1991 - Linux kernel released ( by Linux Torvalds )
## 1991 - Python released ( by Guido van Rossum )
## 1995 - Java released (by James Gosling at Sun Microsystems )
## 1995 - Ruby language released (by Yukihiro Matsumoto / Matz )
![logo](Ruby_logo.svg)
## in the mean-time all the Ruby documentation was in Japanese only
## 2000 - the first english book publish - Programming Ruby
## 2004 - initial release of Ruby on Rails ( by David Heinemeier Hansson )
### [Currently, on github , Ruby (17%) is only second to Javascript (19%) in popularity, followed by Python (9%).](http://www.wikivs.com/wiki/Python_vs_Ruby#Popularity)

--- 
# Ruby - getting started
## Ruby - influenced by Python, Perl, Lisp, Smalltalk
## Strongly Typed, Late Binding
## Runs on VM, Garbage Collected, Object Oriented
## Single Inheritance, Mxins
    !bash
    $ sudo yum install ruby ruby-irb rubygems # installation on Fedroa / RHEL
    $ ruby my-script.rb      # running a ruby script
    $ irb                    # interactive ruby
    $ gem install wirble     # optional
--- 
# Basic data types and variables
##Variables - local, global, instance, class, constant
##Numbers - Fixnum, Bignum
##String - single-quote, double-qoute, delimeters, interpolation, here-doc
##Shell Commands - back-quotes
##Symbol
##Range
##Array
##Hash

    !ruby
    name = "Matz"            # local variable
    age = 46                 # local variable
    $debug = true            # global variable
    @id = 10                 # instance variable
    @dept = "Engineering"    # instance variable
    @@total_instances = 10   # class variable
    MyClass                  # class name
    LOG_LEVEL = 10           # constant 
    var.object_id            # everything is an object
    :north                   # symbol
    [1,2,3,4]                # array
    {:age => 46, :name => "matz" }     # hash
---
#Basic Input / Output

    !ruby
    puts LOG_LEVEL
    print "Hello"
    p "Object"
    printf "My name is %s. I am %d years old.", 'matz', 46
    line = gets
---
# Control Structures
## if / elsif / else / end
## while / end
## case / when / else / end

    !ruby
    grade = gets.chomp
    if grade == "A"
      "excellent"
    elsif grade == "B"
      "good"
    else
      "no one can save you now!"
    end
    # while loop
    input = ""
    while input != "quit"
      input = gets.chomp
      puts input
    end
    # statement modifier
    puts "not a valid end of loop" if input != "quit"
    puts "Never say die!" while true
    # switch-case construct
    grade = gets.chomp
    case grade
    when "A", "B"
      puts "Pass"
    else
      puts "Fail"
    end

---
# Regular Expressions
    !ruby
    /Perl (is|isn't) good/ # /regex/
    r = Regexp.new("Perl (is|isn't) good")
    str1 = "Perl is good"
    str2 = "Perl isn't good"
    str1 =~ /Perl (is|isn't) good/ # => 0
    r.match(str2)      # => #<MatchData "Perl isn't good" 1:"isn't">
    md = r.match(str2)
    input = gets.chomp
    puts "Matched" if input =~ /Perl (is|isn't) good/
---
# Methods ( or functions )
# Everything ( except Fixnum ) is pass-by-reference
    !ruby
    # check whether a string is a palindrome or not
    def palindrome?(s)
      a = s.gsub(/[\W]/, "").downcase
      return true if a.reverse == a
      return false
    end
    
    # factorial of a number
    def fact(number)
      if number < 0
         raise "Invalid input"
      end
      if number > 1
        return number*fact(number-1)
      else
        return number
      end
    end

---
# Object Oriented Programming
# Class, instance variables
    !ruby
    class Person
       @@total_instances = 0
       def initialize(name, address)
         @name = name
         @address = address
         @@total_instances += 1
       end
       def say_hello
         printf "I am #{@name}, and I live at: #{@address}"
       end
       def Person.how_many
         @@total_instances
       end
    end
    class Employee < Person
      def init
    end

---
# OOPs continued.
    !ruby
    class Employee < Person
      def initialize(name, address, company)
        super(name, address)
        @company = company
      end
      def say_hello
        super
        printf "I work at %s.\n", @company
      end
    end
    
    p1 = Person.new("Saleem", "Magarpatta")
    p2 = Person.new("Matz", "Japan")
    p1.say_hello
    p2.say_hello
    printf "Persons instantiated so far: %d\n\n", Person.how_many
    
    e1 = Employee.new("Rambo", "Italy", "Hollywood")
    e1.say_hello
    printf "Persons instantiated so far: %d\n\n", Person.how_many

---
# Modules and Mix-Ins
## Module as a namespace
    !ruby
    require 'person'
    module College
      class Student < Person
      end
    end
    e4 = College::Student.new("Messi", "Argentina")
    e4.say_hello
    printf "Persons instantiated so far: %d\n\n", Person.how_many

## Module as a mixin
    !ruby
    class Person
      include Comparable
      def <=>(other) 
        self.name.length <=> other.name.length
      end
    end
---
# Ruby Gems
    !bash
    # gem install <gem-name>
    # gem list
---
# Additional Topics
## Exception Handling
## Blocks and Iterators
## Proc, Lambda, Closure
## Continuation
## Duck Typing
## Ruby one-liners

---
#Questions?
## IRC: #ruby

---
#Thanks

---
#References

[Programming Ruby](http://www.ruby-doc.org/docs/ProgrammingRuby/)
[Ruby Global Variables](http://www.rubyist.net/~slagell/ruby/globalvars.html)
[Ruby Introductory Tutorial](http://www.bitwisemag.com/copy/programming/ruby/intro/1/ruby3.html)
[Ruby Symbols](http://www.troubleshooters.com/codecorn/ruby/symbols.htm)
[Ruby Comparable Interface](http://ruby-doc.org/core-1.8.7/Comparable.html)
