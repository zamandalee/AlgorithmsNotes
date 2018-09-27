# Cross-Site Request Forgery
- Cross-site (originates on one site but attacks another) request forgery (issues an unintended request)


## Rails' default protection
- Sets authenticity token in session on each request
- non-GET request --> expects client to upload authenticity token in params
  ```html
  <form action="pages/appacademy/like" method="post">
<input type="hidden"
       name="authenticity_token"
       value="<%= form_authenticity_token %>">
  ```
- ```form_authenticity_token``` helper compares user session token with authenticity token stored in form
  - If equal, user submitting form was the one who requested it
  - If not equal, Rails will raise the ActionController::InvalidAuthenticityToken exception (from application_controller.rb)
