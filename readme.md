# <img src="https://cloud.githubusercontent.com/assets/7833470/10899314/63829980-8188-11e5-8cdd-4ded5bcb6e36.png" height="60"> Rails Validations &amp; Error-Handling

Starter code and challenges for <a href="https://github.com/sf-wdi-24/modules/tree/master/week-07-rails-continued/day-02/module-02">Validations & Error-Handling</a> in Rails.

## Getting Started

1. Fork this repo, and clone it into your `develop` folder on your local machine.
2. Run `rake db:create db:migrate` in the Terminal to create and migrate your database.
3. Run `rails s` in the Terminal to start your server.
4. Navigate to `localhost:3000` in the browser.

## Challenges

#### Model Validations

1. Add validations to the `Pet` model. Pets are required to have both `name` and `breed`, and `name` must be at least 3 characters. See the <a href="http://guides.rubyonrails.org/active_record_validations.html" target="_blank">Active Record Validation docs</a> for guidance.

2. In the Terminal, open up the Rails console, and try adding an invalid pet to the database using the `.create` method:

  ```zsh
  irb(main):001:0> pet = Pet.create(name: "Ty")
  ```

  What happens?

3. Now try storing the invalid pet in memory with the `.new` method, and check if it's valid:

  ```zsh
  irb(main):001:0> pet = Pet.new(name: "Ty")
  irb(main):002:0> pet.valid?
  ```

4. Use `.errors.full_messages` to display the user-friendly error messages for the invalid pet you just created.

#### Refactor Pets Controller to Handle Errors

1. The `pets#create` method currently looks like this:

  ```ruby
  #
  # app/controllers/pets_controller.rb
  #
  def create
    pet_params = params.require(:pet).permit(:name, :breed)
    pet = Pet.create(pet_params)
    redirect_to pet_path(pet)
  end
  ```

  What happens when you navigate to `localhost:3000/pets/new` in the browser and try to submit a blank form?

  Refactor your `pets#create` controller method to better handle this error. **Hint:** Use `.new` and `.save`.

2. Once you've refactored `pets#create` to redirect in the case of an error, add flash messages to show the user the specific validation error they triggered, so they won't make the same mistake twice. **Hint:** Set the flash message in the controller, and render the flash message in the layout (`app/views/layouts/application.html.erb`).

## Stretch Challenges

1. You already have routes for `pets#edit` and `pets#update`, since you're calling `resources :pets` in `routes.rb`. Now set up controller methods for `pets#edit` and `pets#update`, as well as a view for editing pets (edit form).

2. Make sure your `pets#update` method also handles errors by redirecting if the user submits invalid data and displaying a flash message in the view.

3. Read the <a href="http://guides.rubyonrails.org/layouts_and_rendering.html#using-partials" target="_blank">Rails docs for partials</a>, and use a partial to DRY up the code in `new.html.erb` and `edit.html.erb`.
