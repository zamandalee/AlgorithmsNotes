# RUBY CONCEPTS/TRIVIA

## React vs. Redux
<img src="ReduxCyclewRails.png" width=550/>
- Redux: yellow, the store, the single-source of truth
- React: green

## Ruby vs. Rails
- Ruby: OOP interpreted programming language dev by Yukihiro Matsumoto
- Rails: web-application framework written with Ruby
  - Set of tools and abstractions that makes writing web applications easier
  - Helps write MVC web applications
    - Separation of logic: functions relating to data access (model), rendering data to the user (view), and business logic (controller)

## Callbacks
- Callback: method called at certain moment of object's life cycle
- Relational callbacks
  - ```dependent: :destroy```: on has_many, user's posts should be destroyed if the user is destroyed (else posts are widowed)
- Registered callbacks
  - ```before_validation```: handy as a last chance to set forgotten fields
  - ```after_create```: handy to do post-create logic, like send a confirmation email
  - ```after_destroy```: handy to perform post-destroy clean-up logic
