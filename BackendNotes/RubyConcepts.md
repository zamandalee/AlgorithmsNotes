# RUBY CONCEPTS/TRIVIA


## Ruby vs. Rails
- **Ruby**: OOP interpreted programming language dev by Yukihiro Matsumoto
- **Rails**: web-application framework written with Ruby
  - Set of tools and abstractions that makes writing web applications easier
  - Helps write MVC web applications
    - Separation of logic: functions relating to data access (model, Active Record), rendering data to the user (view, Action View), and business logic (controller, Action Controller)

## Best Things About Rails
- Fast development
- Well-maintained and tested gems
- TDD highly-supported
- Mature, huge community

## CRUD and RESTful routes
- Create is ```POST```, read is ```GET```, update is ```PATCH```, delete is ```DELETE```
|   NAME   |     PATH       |   HTTP VERB     |            PURPOSE                   |
|----------|----------------|-----------------|--------------------------------------|
| Index    | /blog          |      GET        | Displays all blog post               |
| New      | /blog/new      |      GET        | Shows new form for new blog entry    |
| Create   | /blog          |      POST       | Creates new blog post              |
| Show     | /blog/:id      |      GET        | Shows specific blog post        |
| Edit     | /blog/:id/edit |      GET        | Shows edit form for specific blog post    |
| Update   | /blog/:id      |      PUT        | Updates specific blog post       |
| Destroy  | /blog/:id      |      DELETE     | Deletes specific blog post       |

## OOP
Inheritance
- BasicObject --> Object --> Module --> Class
- **Class**: blueprint from which objects can be created
  - Object of class ```Class```, assigned to a global constant (the name of the assignment)
- **Module**: similar to classes, but can't be instantiated (classes all about objects)

Methods
- **Class method**: ```class Foo   def self.bar ... end end```, for anything that doesn't deal with individual instance
  - Ex.: ```module ActiveRecord
  class Base
    def self.validates_presence_of(...)
      # make sure present
    end
  end
end```
- **Singleton method**: method given to a single object, often used for buttons of a GUI
- Method access control
  - **Public method**: no access control
  - **Protected**: access w/i family, invoked by obj of defining class and subclasses
  - **Private**: receive must be self, only called in context of current obj
- Method lookup path: singleton --> extended module --> prepended module --> class itself --> included module --> super class
  - If multiple extended, included, or prepended modules, the last definition comes first

Variables
- Class variables: one copy shared by all objs of that class

## Proc vs. Lambda
- **Proc**
  - Ex.: ```p = Proc.new {|a, b| puts a + b }``` ```p.call 1``` --> NoMethodError
- **Lambda**: creates proc that checks number of args
  - Ex.: ```l = lambda {|a, b| puts a + b }``` ```l.call 1``` --> ArgumentError
- Control flow keywords difference
  - Return in a Proc returns from its enclosing block/method as well as Proc, return in a lambda returns only from lambda

## Gems
- Code organization
  - Code and tests
    - ```lib```: code
    - ```test``` or ```spec```
    - ```Rakefile```: automates tests and generate code
    - ```bin```: contains executable file, loaded into user's path upon installation
  - Documentation: ```README```
  - gemspec

- Cool gems
  - ```better_errors```: inspect source code live through a console
  - ```faker```: fake data within models
  - ```capybara```: testing framework

## RSpec
```rb
require 'fileName'

RSpec.describe ClassName do
  describe "#initialize" do
    # sloth = Sloth.new("Jimmy")
    subject(:sloth) (Sloth.new("Jimmy"))

    # each it block has own scope
    it "assigns the sloth a name" do
        expect(sloth.name).to eq("Jimmy")
    end

    it "declares ..."
  end
end
```
- Writing own RSpec: ```#describe(str, blk)```

## Callbacks
- **Callback**: method called at certain moment of object's life cycle
- Relational callbacks
  - ```dependent: :destroy```: on has_many, user's posts should be destroyed if the user is destroyed (else posts are widowed)
- Registered callbacks
  - ```before_validation```: handy as a last chance to set forgotten fields
  - ```after_create```: handy to do post-create logic, like send a confirmation email
  - ```after_destroy```: handy to perform post-destroy clean-up logic

## Rack
- **Rack**: interface between framework (Rails) and web server, sits between every request and response
- Rack middleware: can be used to log, sessions, cache, security

## ActiveJob
- **Active Job**: framework for declaring jobs and making them run on a variety of queueing backends
  - Jobs should be small units of work that run in parallel: regularly scheduled clean-ups, billing charges, mailings

## ActiveRecord
- Object Relational Mapper, so you don't have to manually call database yourself (no SQL needed)

## Asset Pipeline
- **Asset pipeline**: framework to compress JS and CSS assets
  - Implemented by default by sprockets-rails gem
  - Features
    1. Concats assets (all JS into master .js file, same w css) --> reduce requests made by browser
    2. Compresses assets (remove comments and whitespace from css)
    3. Allows assets via higher-level language w preocmpilation down to actual assets
      - Ex.: Sass for CSS, CoffeeScript for JS, etc.
