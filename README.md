# Python Django Dev to Deployment

### Build and deploy a real estate application using Django framework & PostgreSQL
---

##### Take a basic HTML/CSS Bootstrap theme and turn it into a real working application with an admin area to manage resources, such as property listings, realtors, and contact inquiries.

[BT Real Estate](http:161.35.41.52/)

---
- make a directory for project
`mkdir btre_project`
- change into directory
`cd btre_project`
- open VS Code
`code .`
- open Terminal window, create virtual environment
`python -m venv ./venv`
- activate virtual environment
`/btre_project/venv/Scripts/activate.bat`
- Django install and project setup
`(venv) /btre_project>pip install django`
`(venv) /btre_project>pip freeze`
- use Django admin
`(venv) /btre_project>django-admin help`
- startproject 
`(venv) /btre_project>django-admin startproject btre .`
- run server
`(venv) /btre_project>python`
- create Pages app
`(venv) /btre_project>python manage.py startapp pages`
- in pages/apps.py, in INSTALLED_APPS, add:
`pages.apps.PagesConfig`
- in directory 'pages' create 'urls.py':
  - add 'index' url pattern:
<img src="/readme_img/image-3.png" width ="300">
- define 'index' in views.py
<img src="/readme_img/image-4.png" width="300">
- link to pages.urls from btre/urls.py:
<img src="/readme_img/image-5.png" width="300">
- Now 'index' view is working:
<img src="/readme_img/image-6.png" width="300">

### pages, templates & base layout

- in settings.py inform where directories for templates will be located:
<img src="/readme_img/image-7.png" width="400">
- create a 'templates' directory
- create a directory in 'templates' called 'pages', and files 'index.html' and 'about.html':
<img src="/readme_img/image-8.png" width="200">
- add an 'about' route like for 'index' in pages/urls.py:
<img src="/readme_img/image-9.png" width="300">
- create an 'about' method in views.py:
<img src="/readme_img/image-10.png" width="300">
- create base.html within templates to extend to other templates:
<img src="/readme_img/image-11.png" width="150">
<img src="/readme_img/image-12.png" width="400">
- extend base.html to index.html:
<img src="/readme_img/image-13.png" width="300">
- extend base.html to about.html:
<img src="/readme_img/image-14.png" width="300">

### static files & paths
- add directory 'static' within btre_project/btre
- copy assets (css, img, js, webfonts) into 'static'
- in btre/settings ‘STATIC_URL’:
  -  Add STATIC_ROOT & STATICFILES_DIRS:
<img src="/readme_img/image-15.png" width="400">
- add static files
`(venv) /btre_project>python manage.py collectstatic`

### Bootstrap layout markup
- in base.html, at the top, we can add:
<img src="/readme_img/image-16.png" width="200">
- for href attributes where input of static files, open a template tag, use 'static' keyword, and wrap path in quotes:
<img src="/readme_img/image-17.png" width="400">
<img src="/readme_img/image-18.png" width="400">

### Partials
- create directory in 'templates' called 'partials'.
  - inside create '_footer.html', '_navbar.html', '_topbar.html':
<img src="/readme_img/image-19.png" width="200">
- copy/paste footer into _footer.html, navabar into _navbar.html, and topbar into _topbar.html.
- in base.html replace sections:
<img src="/readme_img/image-20.png" width="300">

### Listings, Realtors URLs & Templates
- create app 'listings'
`(venv) /btre_project>python manage.py startapp listings`
- create app 'realtors'
`(venv) /btre_project>python manage.py startapp realtors`
- add 'listings' directory in 'templates' with listing.html and search.html:
<img src="/readme_img/image-21.png" width="150">
- in 'listings' directory add 'urls.py'.
  - inside add the 'urlpatterns':
<img src="/readme_img/image-22.png" width="400">
![Alt text](image-22.png)
- in btre/urls.py add the path listings.urls.py:
<img src="/readme_img/image-23.png" width="400">
- in btre/settings.py, in INSTALLED_APPS, add app definitions for listings and realtors:
<img src="/readme_img/image-24.png" width="200">

### create view methods
- in listings/views.py create index, listing and search methods:
<img src="/readme_img/image-25.png" width="400">
  - as well as extending base.html, we can add header tags with titles for each
<img src="/readme_img/image-26.png" width="200">
<img src="/readme_img/image-27.png" width="400">
- Now that it’s all working, add sections with listings between the navbar and footer instead of the ‘Listings’ temporary header:
<img src="/readme_img/image-28.png" width="400">

### Install Postgres & PgAdmin
- choose latest version and download graphical installer
<img src="/readme_img/image-29.png" width="400">
- Use PgAdmin to create a database, 'btredb':
<img src="/readme_img/image-30.png" width="200">

### Django Postgres Setup & Migrate
`(venv) /btre_project>pip install psycopg2`
`(venv) /btre_project>pip install psycopg2-binary`
- in settings.py set up database parameters:
<img src="/readme_img/image-31.png" width="200">
- migrate:
`(venv) /btre_project>python manage.py migrate`
  *tables have been created in the db so Postgres is now interacting with our Django application:*
<img src="/readme_img/image-32.png" width="150">
- map out schemas for listing, realtor, contact:
<img src="/readme_img/image-33.png" width="400">
<img src="/readme_img/image-34.png" width="400">
- create 'Listing' model:
<img src="/readme_img/image-35.png" width="400">
- create 'Realtor' model:
<img src="/readme_img/image-36.png" width="400">
- create 'Contact' model:
<img src="/readme_img/image-37.png" width="400">
- run migrations
`(venv) /btre_project>python manage.py makemigrations`
- reveal the SQL statement:
`(venv) /btre_project>python manage.py sqlmigrate listings 0001`
- migrate
`(venv) /btre_project>python manage.py migrate`

*Now the tables ‘listings_listing’ and ‘realtors_realtor’ are in the database:*
<img src="/readme_img/image-38.png" width="200">
- create superuser
`(venv) /btre_project>python manage.py createsuperuser`
<img src="/readme_img/image-39.png" width="400">
<img src="/readme_img/image-40.png" width="400">
- register models with admin
<img src="/readme_img/image-41.png" width="400">
<img src="/readme_img/image-42.png" width="400">
<img src="/readme_img/image-43.png" width="400">

### Media Folder - add media folder settings
<img src="/readme_img/image-44.png" width="400">
- in btre/urls.py, import ‘settings’ & ‘static’ and configure MEDIA_ROOT and MEDIA_URL: 
<img src="/readme_img/image-45.png" width="400">
- create Realtors in admin
<img src="/readme_img/image-46.png" width="400"> 
- create Listings in admin
<img src="/readme_img/image-47.png" width="400"> 

### Admin and CSS
- create ‘admin’ directory with ‘base_site.html’ in ‘templates’.
  - extend the admin base template and since using a logo image, load ‘static’: 
<img src="/readme_img/image-48.png" width="300"> 
- change upper branding of admin, create a block 'branding':
<img src="/readme_img/image-49.png" width="400">
- add further style with another block:
<img src="/readme_img/image-50.png" width="400">
- create 'admin.css' within 'css' directory:
- target a change in div with id='header': 
<img src="/readme_img/image-51.png" width="400">
<img src="/readme_img/image-52.png" width="250">
- change links to same navy color:
<img src="/readme_img/image-53.png" width="150">
- customize admin display: include other data besides the address/title:
<img src="/readme_img/image-54.png" width="400">
<img src="/readme_img/image-55.png" width="400">
- choose which fields are links & customize which fields will be used to filter listings: 
<img src="/readme_img/image-56.png" width="400">
- modify ‘IS_PUBLISHED’ so that when you click it will toggle between published or not: 
<img src="/readme_img/image-57.png" width="400">
- build search field for chosen fields: 
<img src="/readme_img/image-58.png" width="400">
<img src="/readme_img/image-59.png" width="400">
- pagination setting in admin – list_per_page 
<img src="/readme_img/image-60.png" width="400">

### pull data from Listing model
  - fetch listings using model, then insert it into template, then loop through and output listings that are in the database. 
  - in listings/views.py, 
    - bring in Listing model 
<img src="/readme_img/image-61.png" width="400">
    - Fetch all objects from ‘listings’ into a variable, create a dictionary with this variable as the value & provide a key, pass into the render the variable representing the dictionary: 
<img src="/readme_img/image-62.png" width="400">
- in ‘listings.html’ template we can delete all but one of the pre-populated listings and create a loop for accessing each listing from the database: 
<img src="/readme_img/image-63.png" width="400">
- end the for loop and provide an else block for when there aren’t any listings, and finally end if statement: 
<img src="/readme_img/image-64.png" width="400">
- instead of hard-coded data, as above, alter so we get dynamic data:
<img src="/readme_img/image-65.png" width="400">
- List prices ($550000) are without commas automatically, so use the app ‘humanize’: 
<img src="/readme_img/image-66.png" width="200">
- Then load it into template listings.html
<img src="/readme_img/image-67.png" width="300">
- to access the functions from humanize use the pipe symbol between the field and function:
<img src="/readme_img/image-68.png" width="300">

### pagination
- start by wrapping the unordered list with an if statement which determines if listings hasn’t any more pages than what we specify, pagination won’t show: 
<img src="/readme_img/image-69.png" width="400">
<img src="/readme_img/image-70.png" width="400">

### order listing by date
- instead of ‘objects.all’ we want to ‘order_by’, and pass in ‘list_date’ with a ‘-’ for descending: 
<img src="/readme_img/image-72.png" width="400">
- to make sure the listings in the database whose ‘is_published’ value is ‘False’ don’t populate in listings.html, use a filter: 
<img src="/readme_img/image-74.png" width="400">

### home page dynamic content - views.py
- import Listing
- order by list date
- filter those that are published
- limit to 3 listings
<img src="/readme_img/image-75.png" width="400">

### home page dynamic content - index.html
<img src="/readme_img/image-76.png" width="600">
<img src="/readme_img/image-77.png" width="600">

### about page dynamic content 
- views.py
<img src="/readme_img/image-79.png" width="400">
- about.html 
  - Our Team
<img src="/readme_img/image-80.png" width="600">
  - Seller of the Month
<img src="/readme_img/image-81.png" width="600">

### single listing page 
- listings/views.py
  - to use ‘get_object_or_404’ need to import
<img src="/readme_img/image-82.png" width="400">
- listing.html
<img src="/readme_img/image-83.png" width="500">
<img src="/readme_img/image-84.png" width="500">
<img src="/readme_img/image-85.png" width="500">
<img src="/readme_img/image-86.png" width="500">
<img src="/readme_img/image-87.png" width="500">

### search form choices
- opt to shorten the markup of the home page – currently all options for search are embedded in index.html, but we can store these elsewhere in a dictionary and call when needed
- in ‘listings’ directory create ‘choices.py’ and in it create dictionaries for (bedroom, price, state): 
<img src="/readme_img/image-88.png" width="300">
- because we’re working with the home page index.html, we’ll work in pages/views.py: 
  - import the dictionaries
<img src="/readme_img/image-89.png" width="400">
  - pass them into the html through the context
<img src="/readme_img/image-90.png" width="500">
- in templates/pages/index.html we want to loop through each of those that have option fields: 
<img src="/readme_img/image-91.png" width="500">
<img src="/readme_img/image-92.png" width="500">
- fix the action attribute of the form tag:
<img src="/readme_img/image-93.png" width="400">
<img src="/readme_img/image-94.png" width="400">
*we know this action attribute will work because in listings/urls.py, we’ve given the name ‘search’ and it calls the search method from views:*
<img src="/readme_img/image-95.png" width="400">
-  in listings/views.py verify the search method renders the correct search.html template:
<img src="/readme_img/image-96.png" width="400">
- add the markup to the search.html page:
<img src="/readme_img/image-97.png" width="600">
*the form here also includes all options for states, bedrooms, prices so can be shortened as before by calling in from dictionaries in choices.py:*
- in listings/views.py import dictionaries in choices.py and in the ‘search’ method provide access to the dictionaries there: 
<img src="/readme_img/image-98.png" width="600">
<img src="/readme_img/image-99.png" width="400">
- in templates/listings/search.html and again delete all hardcoded options and loop to access as before:
<img src="/readme_img/image-100.png" width="600">

### search form filtering
- any field filled in when submitted, first check if the field exists.  Then pull it out of the request and put it into a variable and base queryset on the filtering of the variable.  This will be done in listings/views.py in the ‘search’ method: 
<img src="/readme_img/image-101.png" width="400">
- in templates/listings/search.html use the same markup code as in listings.html where we loop through available listings from the db.  It will be filtered based on user queries, but this will do for a start:
<img src="/readme_img/image-102.png" width="600">
<img src="/readme_img/image-103.png" width="400">
- within the search function of listings/views.py, start adding some filters (keyword, city, state, bedroom, max price): 
<img src="/readme_img/image-104.png" width="600">

### preserving form input
- In listings/views.py/search let’s add to the dictionary ‘context’ a variable ‘values’ with a value ‘request.GET’: 
<img src="/readme_img/image-105.png" width="400">
- back to ‘search.html’ in ‘keywords’ input add ‘value’ attributes to each input: 
<img src="/readme_img/image-106.png" width="400">
<img src="/readme_img/image-107.png" width="400">
<img src="/readme_img/image-108.png" width="400">
<img src="/readme_img/image-109.png" width="400">
<img src="/readme_img/image-110.png" width="400">

### Accounts App & URLs
- create a seperate app 'accounts'
`(venv) /btre_project>python manage.py startapp accounts`
- create routes for 'REGISTER' and 'LOGIN' buttons:
  - in ‘templates’ directory create directory ‘accounts’ with ‘dashboard.html’, ‘login.html’, and ‘register.html’.  In each of these files, temporarily add a header tag with respective titles: 
- within 'accounts' directory create urls.py
- in btre/settings.py add new app to INSTALLED_APPS:
<img src="/readme_img/image-111.png" width="300">
- in accounts/urls.py configure routes:
<img src="/readme_img/image-112.png" width="500">
- in btre/urls.py add routes:
<img src="/readme_img/image-113.png" width="500">
- add accounts view methods inside views.py:
<img src="/readme_img/image-114.png" width="400">
- fix the ‘REGISTER’ and ‘LOGIN’ links.  They are in templates/partials/__navbar.html.  Not only can we change the href attributes to be dynamic, but also use conditionals to either keep a link active or not: 
<img src="/readme_img/image-115.png" width="500">
- fill the markup for each html page just created
<img src="/readme_img/image-116.png" width="600">
<img src="/readme_img/image-117.png" width="600">
- change the form ‘action’ attribute of both register.html and login.html.  Be sure to specify the methods' attributes as ‘POST’:
<img src="/readme_img/image-118.png" width="400">
- csrf token
  - IMPORTANT! When a form is making a POST request, add a ‘csrf’ token, which prevents cross-site forgery by tying the form to the user’s session.  This can be placed just following the opening form tag: 
<img src="/readme_img/image-119.png" width="400">
- in accounts/views.py identify if the request to register and login is a post or a get.  Temporarily print a message in the terminal to test: 
<img src="/readme_img/image-120.png" width="400">
  - after filling in the registration form, the terminal prints ‘SUBMITTED REG’:
<img src="/readme_img/image-121.png" width="400">

### Message Alerts
- in btre/settings.py:
<img src="/readme_img/image-122.png" width="400">
- in templates/partials create a file ‘_alerts.html’: 
<img src="/readme_img/image-123.png" width="150">
  - inside we add the code for a bootstrap themed alert:
<img src="/readme_img/image-124.png" width="400">
- test this.  First in accounts/views.py, import messages and use messages.error():
<img src="/readme_img/image-125.png" width="400">
- open ‘templates/accounts/register.html’ and put the alerts message just above the form tag:
<img src="/readme_img/image-126.png" width="400">
- also in login.html as well:
<img src="/readme_img/image-127.png" width="400">
- use JavaScript to animate the error message to disappear.  In btre/static/js/main.js:
<img src="/readme_img/image-128.png" width="400">
  - since this is in the static folder in btre, run ‘collectstatic’ so that it goes into the main static folder:
`(venv) btre_project>python manage.py collectstatic`

### User Registration
- in accounts/views.py, in the register method, implement logic to register user now that testing the error message is finished: 
<img src="/readme_img/image-129.png" width="600">

### User Login
- in accounts/views.py/login
<img src="/readme_img/image-130.png" width="600">

### Logout & navbar auth links
- fill in markup for ‘dashboard.html’, in Breadcrumb add dynamic href attribute:
<img src="/readme_img/image-131.png" width="600">
- in templates/partials/_navbar.html use conditionals to show ‘Register’ and ‘Login’ buttons if user is not authenticated and show ‘Logout’ and ‘Dashboard’ buttons otherwise.  To logout use JavaScript within the href attribute of the anchor tag and add the form within that same list item element: 
<img src="/readme_img/image-132.png" width="600">
<img src="/readme_img/image-133.png" width="500">
- in accounts/views.py complete the logout method:
<img src="/readme_img/image-134.png" width="400">

### Dynamic page titles
- in templates/base.html add a block within the title tag: 
<img src="/readme_img/image-135.png" width="400">
- in templates/pages/index.html use the ‘title’ block and use ‘Welcome’ for home page:
<img src="/readme_img/image-136.png" width="400">
- in templates/pages/about.html similar as above:
<img src="/readme_img/image-137.png" width="400">
- in templates/listings/listings.html: 
<img src="/readme_img/image-138.png" width="400">
- in templates/listings/search.html:
<img src="/readme_img/image-139.png" width="400">
*do similar for: dashboard.html, login.html, register.html.*
- in templates/listings/listing.html dynamically add the title for a particular listing:
<img src="/readme_img/image-140.png" width="400">

### Contacts app & model
- create 'contacts' app:
`(venv) /btre_project>python manage.py startapp contacts`
- in contacts/models.py create the ‘Contact’ model:
<img src="/readme_img/image-141.png" width="600">
- in btre/settings add the ‘Contacts’ app to INSTALLED_APPS:
<img src="/readme_img/image-142.png" width="300">
- to put a table in the database for contacts, create a migration: 
`(venv) /btre_project>python manage.py makemigrations contacts`
- run migration
`(venv) /btre_project>python manage.py migrate`
- register ‘Contact’ model in contacts/admin.py:
<img src="/readme_img/image-143.png" width="400">

### Contact form prep
- in templates/listings/listing.html: 
  - add ‘action’ and ‘method’ attributes to form tag
  - add ‘csrf’ token
  - collect ‘user_id’ through hidden input if user is authenticated
  - collect realtor ‘email’ through hidden input 
  - collect ‘listing_id’ through hidden input 
  - make listing input’s value attribute dynamic
  - for ‘name’ and ‘email’ inputs, if user is authenticated add their name and email value attributes 
<img src="/readme_img/image-144.png" width="600">
<img src="/readme_img/image-145.png" width="600">
- Because there isn’t an URL with the name of ‘contact’, create ‘urls.py’ in ‘contacts’:
<img src="/readme_img/image-146.png" width="600">
- in btre/urls.py:
<img src="/readme_img/image-147.png" width="400">
- in contacts/views.py define a contact method, collect form submissions, check if user has already made inquiry, create a contact, save, provide a success message, and redirect to the same listing page: 
<img src="/readme_img/image-148.png" width="600">
<img src="/readme_img/image-149.png" width="600">
- above, the option to send email has been commented out, but if needed also add email configuration in btre/settings.py: 
<img src="/readme_img/image-150.png" width="300">
- in contacts/views.py import ‘send_mail’: 
<img src="/readme_img/image-151.png" width="300">

### Dashboard functionality
- in accounts/views.py flesh out the dashboard function which gathers contacts.  First, import Contact from contacts.models: 
<img src="/readme_img/image-152.png" width="300">
<img src="/readme_img/image-153.png" width="600">
- in templates/accounts/dashboard.html make dynamic where necessary.  Just before the table use a conditional to determine if there are any contacts for this user.  If so, use a for loop in the table body to print id, listing and button linking to the listing. In else statement indicate there aren’t any contacts: 
<img src="/readme_img/image-154.png" width="600">

### Django deployment to Ubuntu
*Any commands with "$" at the beginning run on your local machine and any "#" run when logged into the server*
- sign up to account with Digital Ocean (create Droplet)
- creating SSH keys
`$ ssh-keygen`
- hit enter all the way through and it will create a public and private key at
`~/.ssh/id_rsa`
`~/.ssh/id_rsa.pub`
- copy the public key (.pub file)
`$ cat ~/.ssh/id_rsa.pub`
- copy the entire output and add as an SSH key for Digital Ocean
- login to your server
`$ ssh root@YOUR_SERVER_IP`
- create new user
`# adduser djangoadmin`
- give root privileges
`# usermod -aG sudo djangoadmin`
- SSH keys for the new user
    - get them from your local machine
`# exit`
- You can generate a different key if you want but we will use the same one so lets output it, select it and copy it
`$ cat ~/.ssh/id_rsa.pub`
- log back into the server
`$ ssh root@YOUR_SERVER_IP`
- add SSH key for new user
  - Navigate to the new users home folder and create a file at '.ssh/authorized_keys' and paste in the key
```
# cd /home/djangoadmin
# mkdir .ssh
# cd .ssh
# nano authorized_keys
Paste the key and hit "ctrl-x", hit "y" to save and "enter" to exit
```
- login as new user
`$ ssh djangoadmin@YOUR_SERVER_IP`
- disable root login
`# sudo nano /etc/ssh/sshd_config`
- change the following
```
PermitRootLogin no
PasswordAuthentication no
```
reload sshd service
`# sudo systemctl reload sshd`

#### Simple Firewall Setup
- See which apps are registered with the firewall
`# sudo ufw app list`
- allow OpenSSH
`# sudo ufw allow OpenSSH`
- enable firewall
`# sudo ufw enable`
- check status
`# sudo ufw status`

#### Software
- update packages
```
# sudo apt update
# sudo apt upgrade
```
- install Python 3, Postgres & NGINX
`# sudo apt install python3-pip python3-dev libpq-dev postgresql postgresql-contrib nginx curl` 
- Postgres database & user setup
`# sudo -u postgres psql`
  - You should now be logged into the pg shell
- create a database
`CREATE DATABASE btre_prod;`
- create user
`CREATE USER dbadmin WITH PASSWORD 'abc123!';`
- Set default encoding, transaction isolation scheme (Recommended from Django)
```
ALTER ROLE dbadmin SET client_encoding TO 'utf8';
ALTER ROLE dbadmin SET default_transaction_isolation TO 'read committed';
ALTER ROLE dbadmin SET timezone TO 'UTC';
```
- give User access to database
`GRANT ALL PRIVILEGES ON DATABASE btre_prod TO dbadmin;`
- Quit out of Postgres
`\q`

#### Virtual Environment
- install the python3-venv package
`# sudo apt install python3-venv`
- Create project directory
```
# mkdir pyapps
# cd pyapps
```
- create venv
`# python3 -m venv ./venv` 
- activate the environment
`# source venv/bin/activate`

#### Git & Upload
- Pip dependencies
  - from local machine, create requirements.txt with app dependencies. Push this to repo
`$ pip freeze > requirements.txt`
- Clone the project into the app folder on your server (Either HTTPS or setup SSH keys)
`# git clone https://github.com/yourgithubname/btre_project.git`
- install pip modules from requirements
`# pip install -r requirements.txt`

#### Local Settings Setup
- Add code to your settings.py file and push to server
```
try:
    from .local_settings import *
except ImportError:
    pass
```
- create a file called local_settings.py on server alongside settings.py and add:
  - SECRET_KEY
  - ALLOWED_HOSTS
  - DATABASES
  - DEBUG
  - EMAIL_*

#### Run Migrations
```
# python manage.py makemigrations
# python manage.py migrate
```

#### Create super user
`# python manage.py createsuperuser`

#### create static files
`python manage.py collectstatic`

#### Create exception for port 8000
`# sudo ufw allow 8000`

#### Run Server
`# python manage.py runserver 0.0.0.0:8000`

#### Test the site at YOUR_SERVER_IP:8000
- add some data in the admin area

### Gunicorn Setup
- install gunicorn
`# pip install gunicorn`
- add to requirements.txt
`# pip freeze > requirements.txt`

#### Test Gunicorn serve
`# gunicorn --bind 0.0.0.0:8000 btre.wsgi`
*images, etc will be gone*

#### stop server & deactivate virtual env
```
ctrl-c
# deactivate
```

#### open gunicorn.socket file
`# sudo nano /etc/systemd/system/gunicorn.socket`

#### copy this code, paste it in and save
```
[Unit]
Description=gunicorn socket

[Socket]
ListenStream=/run/gunicorn.sock

[Install]
WantedBy=sockets.target
```

#### open gunicorn.service file
`# sudo nano /etc/systemd/system/gunicorn.service`

#### Copy this code, paste it in and 
```
[Unit]
Description=gunicorn daemon
Requires=gunicorn.socket
After=network.target

[Service]
User=djangoadmin
Group=www-data
WorkingDirectory=/home/djangoadmin/pyapps/btre_project
ExecStart=/home/djangoadmin/pyapps/venv/bin/gunicorn \
          --access-logfile - \
          --workers 3 \
          --bind unix:/run/gunicorn.sock \
          btre.wsgi:application

[Install]
WantedBy=multi-user.target
```

#### start and enable Gunicorn socket
```
# sudo systemctl start gunicorn.socket
# sudo systemctl enable gunicorn.socket
```

#### check status of Gunicorn
`# sudo systemctl status gunicorn.socket`

#### check the existence of gunicorn.sock
`# file /run/gunicorn.sock`

### NGINX setup
- Create project folder
`# sudo nano /etc/nginx/sites-available/btre_project`
- paste into the file:
```
server {
    listen 80;
    server_name YOUR_IP_ADDRESS;

    location = /favicon.ico { access_log off; log_not_found off; }
    location /static/ {
        root /home/djangoadmin/pyapps/btre_project;
    }
    
    location /media/ {
        root /home/djangoadmin/pyapps/btre_project;    
    }

    location / {
        include proxy_params;
        proxy_pass http://unix:/run/gunicorn.sock;
    }
}
```

#### enable the file by linking to the sites-enabled dir
`# sudo ln -s /etc/nginx/sites-available/btre_project /etc/nginx/sites-enabled`

#### test NGINX config
`# sudo nginx -t`

#### restart NGINX
`# sudo systemctl restart nginx`

#### remove port 8000 from firewall and open up firewall to allow normal traffic on port 80
```
# sudo ufw delete allow 8000
# sudo ufw allow 'Nginx Full'
```
---
*probably need to up the max upload size to be able to create listings with images*

#### open up nginx conf file
`# sudo nano /etc/nginx/nginx.conf`

---

#### add to http{} area:
`client_max_body_size 20M;`

#### reload NGINX
`# sudo systemctl restart nginx`

#### media file issue
*may have issues with images not showing up. Delete all data, start fresh and remove the "photos" folder in the "media folder":*
`# sudo rm -rf media/photos`

### domain setup
- go to domain registrar, create the following A record:
```
@  A Record  YOUR_IP_ADDRESS
www  CNAME  example.com
```

#### go to local_settings.py on the server, change "ALLOWED_HOSTS" to include the domain
`ALLOWED_HOSTS = ['IP_ADDRESS', 'example.com', 'www.example.com']`

#### edit /etc/nginx/sites-available/btre_project:
```
server {
    listen: 80;
    server_name xxx.xxx.xxx.xxx example.com www.example.com;
}
```

#### reload NGINX & Gunicorn
```
# sudo systemctl restart nginx
# sudo systemctl restart gunicorn
```




