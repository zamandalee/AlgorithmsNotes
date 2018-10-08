# RUBY CONCEPTS/TRIVIA


## Ruby vs. Rails
- Ruby: OOP interpreted programming language dev by Yukihiro Matsumoto
- Rails: web-application framework written with Ruby
  - Set of tools and abstractions that makes writing web applications easier
  - Helps write MVC web applications
    - Separation of logic: functions relating to data access (model, Active Record), rendering data to the user (view, Action View), and business logic (controller, Action Controller)

## Best Things About Rails
- Fast development
- Well-maintained and tested gems
- TDD highly-supported
- Mature, huge community

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
  - ```pry-rails```

## Callbacks
- Callback: method called at certain moment of object's life cycle
- Relational callbacks
  - ```dependent: :destroy```: on has_many, user's posts should be destroyed if the user is destroyed (else posts are widowed)
- Registered callbacks
  - ```before_validation```: handy as a last chance to set forgotten fields
  - ```after_create```: handy to do post-create logic, like send a confirmation email
  - ```after_destroy```: handy to perform post-destroy clean-up logic
