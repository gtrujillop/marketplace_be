# Marketplace API

This is a small RoR 5.1.3 + Ruby 2.3.1 proyect. It serves as backend tier for a small Marketplace Web application

### LIVE VERSION:
http://marketplace-api-getp.herokuapp.com/v1/products

### API DOCS
http://marketplace-api-getp.herokuapp.com/api/docs

## Getting Started:

If you want to try this repo locally, Please clone this repo and consider the RoR & Ruby versions mentioned above. Also, install postgresql 9.x version and create databases for testing and development envs the way are defined on database.yml files

After having all basic settings, update your gemfile by running `bundle install --whitout production`. After that, run migrations and start your puma server

Also, run your redis server and your resque jobs

```
redis-server
```

then

```
QUEUE='*' VERBOSE=1 rake environment resque:work
```
This will allow You to send emails locally. However, we sugggest to try this via online version

## Usage

After having all initial config done and project running, please open up a rails console `rails c` and create an initial admin user

```
User.create(first_name: 'Admin', last_name: 'User', email: 'adminuser@myemail.com', pasword: '12345678', password_confirmation: '1234567', is_admin: true)
```
If there were no issues while creating the Admin user, go ahead and add products by running a POST request to

`http://localhost:3000/v1/products`
and pass your auth keys as headers on the request:

```
X-API-EMAIL:gaston.trujillo.java@gmail.com
X-API-TOKEN:prqKSa8-RxGtaqQ5LLoy3RrqTjexy6rSeA
```
Both values can be reviewed via console

```
rails c
> User.last.authentication_token
> 'prqKSa8-RxGtaqQ5LLoy3RrqTjexy6rSeA'
> User.last.email
> gaston.trujillo.java@gmail.com
```

The body of the POST request must be the JSON file shared with this assessment

OR You can run a CURL request by running
something like

```curl -vX POST http://localhost:3000/v1/products -d @products.json --header "Content-Type: application/json" --header "X-API-TOKEN: prqKSa8-RxGtaqQ5LLoy3RrqTjexy6rSeA" --header "X-API-EMAIL: gaston.trujillo.java@gmail.com"```

If products were loaded, You'll get a 200 OK respone AND you can review'em via GET request to

`http://localhost:3000/v1/products`

## Author:

* **Gaston Trujillo Pulgar**
