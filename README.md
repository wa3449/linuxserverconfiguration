# Name
Linux Server Configuration
# Project Description
The project entails hosting the Item Catalog Tool that was created in the previous Udacity FullStack project on a Linux server, and also securing the Linux server instance against a number of attack vectors covered in the Udacity Fullstack instruction.

The Item Catalog Tool is a python application that manages a list of items within a set of pre-defined categories. Registered users who have successfully authenticated with their Google login will have the ability to post, edit and delete their own items. The solution space for this particular implementation of category/item(s) is Literary Genres. Literary Genres include works of prose, poetry, drama, hybrid forms, or other literature that are distinguished by shared literary conventions, similarities in topic, theme, style, or common settings, character types, or formulaic patterns of character interactions and events, and an overall predictable form.

The Item Catalog Tool has a browser based GUI and a number of API endpoints that provide access to the item catalog data.

## GUI
The item catalog tool GUI supports the following views:
1. Home - the Home view displays a list of categories in one pane, and a list of 5 items that were most recently added/updated. The Home view will display an Add Item control for a user that has logged in.
2. Category Items - the Category Items view displays all the items for a selected category.
3. Item Detail - the Item Detail view displays item details.
4. Add Item - the Add Item view supports a form that can be used to add an item.
5. Edit Item - the Edit Item view supports a form that can be used to update item attributes and category relationship.
6. Delete Item - the Delete Item view supports a form that can be used to delete an item.
7. Login - the login view displays a means to support user login via Google.

## REST API Endpoints
The item catalog tool REST APIs support the following operations:
1. Get all categories and for each category, all category items: "address/catalog.JSON"
2. Get all items for a category: "address/catalog/<string:categoryName>/items/JSON"
3. Get all a specific item for a category: "address/catalog/<string:categoryName>/<string:itemName>/JSON"

## REST API Endpoints for database seeding
There are also API endpoints which are used to seed the item catalog database:
1. Create a user: "address/catalog/user"
2. Create a category "address/catalog/categories"
3. Create a category item: "address/catalog/items"

## The model:

The model consists of 3 object types:
1. category
2. item
3. user

Each of the object types has the following data elements:
1. category
- id, pk
- name, string, indexed
2. item
- id, pk
- name, string, indexed
- description, string
- edited_on, datetime
- category id, fk
- user id, fk
3. user
- id, integer, pk
- username, string, indexed
- email, string, indexed
- password_hash, string
- picture, string

The object types have the following relationships:
1. category, 1:M item
2. user , 1:M item

The application supports the following operations on the object types:
1. categories - cr
2. item - crud
3. user - cr

The object types must support the following regulations:
1. An item can only be updated or deleted by the user that created the item
2. Only an authenticated and authorized user can add, update, or delete an item

# Requirements
## Structure
The Item Catalog Tool uses the following enabling technologies:
* Amazon Lightsail
* Ubuntu Linux
* PostgreSQL
* SQLAlchemy
* HTML
* CSS
* Apache web server
* WSGI module
* Python
* Pip
* Flask
* Psycopg
* OATH2client
* Git

## Application directory structure

The application directory is /Catalog with the following sub-directories:

```
/catalog
    /static
    /templates
```

1. The catalog directory is the application directory
2. The static directory contains reference files used by the presentation
3. The templates directory contains the application HTML files

## Application Code

1. models.py - Creates the database instance
2. seeddb.py - Seeds the database instance. Note: there is a dependency on running the views.py since API endpoints are used by seeddb.py to seed the database. I did this to get more experience with API endpoints and JSON but would change this in the future to remove the dependency with the application.py code.
3. __init__.py - Supports the HTML, JSON, and other endpoints for the application, model methods, and main loop.

## Create the database schema and load the data needed for the Project

The catalog database has been created and seeded.

# Linux Server Configuration
## Get your server
Amazon Lightsail running Ubuntu Linux instance

IP address: 35.170.78.21

SSH port: 2200

Item Catalog Tool URL:
```
http://35.170.78.21.xip.io
```

## Secure your server

Update all installed packages

Change SSH port from 22 to 2200

Configure UFW for SSH port 2200, HTTP, and NTP

## Give grader access

Create a new user account named grader

Grant grader sudo permission

Create a SSH key pair for grader using ssh-ten

## Prepare to deploy your project

Install and configure apache2 web server

Install and configure a new PostgreSQL database user named catalog with limited permissions to the catalog db

## Install git

## Deploy the Item Catalog project

Clone the project from github

Configure project to use the PostgreSQL db - note user:password in connect (would hide in a production implementation)

Configure project to access local files (for Google login)

Configure Google access with new DNS address: ip.xip.io

Configure apache and WSGI

Configure apache (security.conf) to disallow access to .git directory

## Usage

1. Open a browser and type the following to display the Item Catalog Tool GUI:

```
http://35.170.78.21.xip.io
```
## External resources employed
* https://www.digitalocean.com/community/tutorials/how-to-install-and-use-postgresql-on-ubuntu-14-04
* https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
* https://help.ubuntu.com/lts/serverguide/httpd.html
* https://askubuntu.com
* Udacity student hub & knowledge
