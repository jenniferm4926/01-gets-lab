## Objectives

1. Understand the significance of capturing and operating on user input in a CLI application.
2. Create a prompt for user input in a CLI.
3. Use the `#gets` method to capture, store, and operate on that input.

## User Input and the CLI

> I think it's fair to say that personal computers have become the most empowering tool we've ever created. They're tools of communication, they're tools of creativity, and they can be shaped by their user. –– Bill Gates

It is inarguable that the advent of personal computing has changed the world and the way that individuals interact with it and with one another. The core of this revolution has been interactivity. The capability of computers to *be interacted with*. Who builds this interactive capability? We do! As a programmer, the underlying functionality of many of the applications you build will be interaction, the interaction between a user and your program. There are many ways in which that interaction can play out. Here, we'll discuss one of the most basic ways––the `#gets` method and the command line interface (CLI).  

## CLI Flow

 The basic flow of a CLI app goes something like this:

 1. Greet the user.
 2. Ask the user for input.
 3. Capture and store that input.
 4. Do something with that input.

In this exercise, we'll be familiarizing ourselves with a CLI application that has already been built. To experience the user-flow of this application, first fork and clone this lab.

Run `rspec` 

You'll need to modify the `greeting` method in `lib/hello_ruby_programmer.rb` so
that it accepts an argument called `name`.

**HINT:** Just change the line that reads `def greeting` to `def greeting(name)`.

Then run `ruby bin/greeting` in your terminal, from within the directory of this project.

Note that you are greeted, asked to provide input and then greeted again, this time with a phrase that uses the input you provided.

Let's take a closer look at the structure of this application.


## Project Structure

Check out the file structure below.

```
bin
   |–– greeting
lib
   |–– hello_ruby_programmer.rb
...
```  

Let's take a moment to review:

### The `bin` Directory

The `bin` directory holds our **executable** file. This file is responsible for running the program. It contains code that actually enacts the command line interaction––i.e. greeting the user, asking the user for input, storing that input and then acting on it.

Open up `bin/greeting`. Notice that we are requiring the `lib/hello_ruby_programmer.rb` file.

### The `lib` Directory

The `lib` directory is where we place the code that our program relies on to run. It is the meat of our CLI application. Our executable file *requires* the files in the `lib` directory and uses the code (for example, calling on any methods we might define) to enact the CLI.

Open up `lib/hello_ruby_programmer.rb` file. Notice that it defines a `#greeting` method that is called in the `bin/greeting` file. This is the pattern you'll become familiar with for CLI applications––defining methods in a `lib` directory and calling those methods in `bin` executable files to actually run the program.

Now, let's take a closer look at our code.

## The CLI Pattern

In `bin/greeting` you should see the following code:

```ruby
puts "Hi! Welcome to the wonderful world of Ruby programming."
puts "Please enter your name so that we can greet you more personally:"
name = gets.chomp
greeting(name)
```

Here, we have all of the CLI flow steps outlined above. Let's break it down:

1 . Greet the user:

```ruby
puts "Hi! Welcome to the wonderful world of Ruby programming."
```

2 . Ask the user for input:

```ruby
puts "Please enter your name so that we can greet you more personally:"
```

3 . Capture that input using `#gets`

```ruby
name = gets.chomp
```

4 . Use that input to do something else:

```ruby
greeting(name)
```

In this case, we are passing the user's input into the `#greeting` method as an argument. The greeting method then uses string interpolation to `#puts` out a personalized message.


## The `gets` Method

We've talked a lot about capturing and storing a user's input to the terminal and using it in our Ruby program. Now we'll take a closer look at exactly how that happens.

Let's take another look at our code from `bin/greeting`

```ruby
puts "Hi! Welcome to the wonderful world of Ruby programming."
puts "Please enter your name so that we can greet you more personally:"
name = gets.chomp
greeting(name)
```

On the third line, the `gets` method is being called. Calling the `gets` method captures the last thing the user typed into the terminal. Whenever your program makes a call to `gets`, it will freeze and wait for user input.

### Waiting for the user Input

If the user never types anything in, your program will wait forever until it is otherwise exited. If you find your tests and your program stalling for long periods of time (anything over 5-10 seconds generally), you might be trapped in a `gets`.

From executing a program, a `gets` will look like:

![gets in program](https://dl.dropboxusercontent.com/s/ezddrtyotw5ahow/2015-09-10%20at%2012.12%20PM.png)

From a test run, a stalled gets will look like:

![gets in test](https://dl.dropboxusercontent.com/s/tijh1wyuvdfz11a/2015-09-10%20at%2012.13%20PM.png)

### Return value for `gets`

The return value of `gets` is the text typed into the terminal. So, setting a variable, `name`, equal to invoking the `gets` method sets that variable equal to the return value of `gets`––the last thing typed into the terminal. Then, the following line uses that `name` variable in string interpolation.

Once we store the return value of `gets` in a variable, we can treat that variable as we would any variable pointing to a string––interpolate with it, convert it to an integer, add it to an array, you name it.

### Sanitizing User Input: The `chomp` Method

One thing to know about the `#gets` method is that it captures a new line character at the end of whatever input it is storing. When the user types their response and presses `enter`, the `enter` is captured as an extra line.  We don't want new lines to be appended to the user input we are trying to store. So, we can chain a call to the `#chomp` method to remove any new lines.

## Practice on your own

Try it out for yourself! Create a new file in the root of this repository called `mimick.rb`.

1. Define a new method `#me_too(name)` that will `puts` the string `NAME??? That's my name too!!!`.  Notice how we're shouting the name.
2. After your method definition, `puts` a greeting that asks the user for their name.
3. Use `gets.chomp` and store the result in a variable, such as `user_name`.
4. Call your `#me_too` method using `user_name` to turn your CLI into a lying mimicker.
5. Use `ruby mimick.rb` to test it out for yourself.

NOTE: there is no `rspec` test for this.

### #gets data types

By default, the return value of `#gets` is always a string.  So if you ever ask the user for a number, make sure to include the `.to_i` method to convert it to an integer.

For example: `user_age = gets.chomp.to_i`

Conversely, if you ever need to go in the other direction, `.to_s` will convert a number into a string.

## Keep playing!

Use what you've learned to turn your CLI into your new best friend (or worst enemy).