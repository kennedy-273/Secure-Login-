# Django Login and Success Page Project

This project demonstrates how to create a secure login page and success page in Django. It includes mockup created with advanced design tools,showing planned UI/UX design,and is deployed on a production server using uWSGI and Nginx. The project follows secure session management practices.

## Table of Contents

-   [Project Overview](#project-overview)
-   [Prerequisites](#prerequisites)
-   [Setup Instructions](#setup-instructions)
    -   [1. Setting Up the Django Application](#1-setting-up-the-django-application)
    -   [2. Database Setup](#2-database-setup)
    -   [3. Running the Application Locally](#3-running-the-application-locally)
    -   [4. uWSGI and Nginx Deployment](#4-uwsgi-and-nginx-deployment)
-   [Mockups](#mockups)
-   [Security Practices](#security-practices)
-   [Sample Pages](#sample-pages)


## Project Overview

-   **Signup Page**: Allows new users to create an account.
-   **Login Page**: A user-friendly login page where users can authenticate.
-   **Success Page**: A page users are redirected to after successfully logging in.
-   **Advanced Mockups**: Created with [tool_name] to demonstrate a professional design approach.
-   **Production Deployment**: Set up using uWSGI and Nginx for serving the application in a production environment.
-   **Secure Session Management**: Following industry standards for session security, including HTTPS, secure cookies, and CSRF protection.

## Prerequisites

Before running this project,ensure you have the following installed:

-Python3.8+
-Django4.0+
-uWSGI
-Nginx
-PostgresSQL or SQLIte(depending on your environment)
-DEsign/Wireframe tools (e.g., Figma)

### Setup Instructions

#### 1. Setting Up Django Application

1. Clone the repository

    bash

        git clone https://github.com/your-repo/django-login-success.git
		cd django-login-success`

2. Create a virtual environment:

    bash

        python -m venv env
	    source env/bin/activate`

3. Install the dependencies:
     
     bash

        `pip install -r requirements.txt` 

4. Add login_app to your INSTALLED_APPS in Settings.py 

    Python

        `INSTALLED_APPS = [
	        # other apps
	        'login_app',
	    ]`
5.  Set up your session settings in `settings.py`:
    
    python
    
    
	    `SESSION_COOKIE_SECURE = True
	    CSRF_COOKIE_SECURE = True
	    SECURE_BROWSER_XSS_FILTER = True
	    SECURE_CONTENT_TYPE_NOSNIFF = True
	    SECURE_SSL_REDIRECT = True  # For production`

### Database Setup

1. Migrate the database

    bash

        `python manage.py migrate`

2. Create a superuser for Django admin interface:

    bash

        `python manage.py createsuperuser`

3. Run the application locally to verify the setup:

    bash

        `python manage.py runserver

### 3. Running the Application Locally 

-   Access the signin page at `http://127.0.0.1:8000/signin/`.
-   Access the login page at `http://127.0.0.1:8000/login/`.
-   After a successful login, you'll be redirected to the success page at `http://127.0.0.1:8000/success/`.

#### 4. uWSGI and Nginx Deployment 

For deploying the application in a production environment, follw these steps:

1. **Install uWSGI**

    bash
        pip install uwsgi

2. **Configure uWSGI** Create a uwsgi.in file in your project directory:

    ini
        `[uwsgi]
		    module = django_login_success.wsgi:application
		    master = true
		    processes = 5
		    socket = /path/to/your/project/django_login_success.sock
		    chmod-socket = 660
		    vacuum = true
		    die-on-term = true` 

3. **Installing and Configure NGinx:**

- install Nginx

    bash

        sudo apt-get install nginx

-   Configure Nginx for your Django project by creating a file in `/etc/nginx/sites-available/django_login_success`:
        
        nginx
        
        Copy code
        
		        `server {
		            listen 80;
		            server_name your_domain_or_ip;
		        
		            location / {
		                include         uwsgi_params;
		                uwsgi_pass      unix:/path/to/your/project/django_login_success.sock;
		            }
		        
		            location /static/ {
		                alias /path/to/your/project/static/;
		            }
		        
		            location /media/ {
		                alias /path/to/your/project/media/;
		            }
		        }` 
		        
		    -   Enable the Nginx configuration:
		        
		        bash
		        
		        Copy code
		        
		        `sudo ln -s /etc/nginx/sites-available/django_login_success /etc/nginx/sites-enabled
		        sudo systemctl restart nginx`

## Mockups

Mockups were created using [wireframe tool of choice] and can be found in the `mockups/` folder of this repository. These mockups showcase the design and layout of the signup, login, and success pages.

1.  **Signup Page Mockup**
    
2.  **Login Page Mockup**
    
3.  **Success Page Mockup**
    

----------

## Security Practices

-   **Sessions**: Session management is securely handled using Django's default session framework. This includes the use of secure cookies and CSRF protection.
-   **HTTPS**: Enforced HTTPS connections for security in production by setting `SECURE_SSL_REDIRECT` and using `SESSION_COOKIE_SECURE`.
-   **XSS and CSRF**: All forms are protected against Cross-Site Request Forgery (CSRF) attacks, and HTTP headers are configured to mitigate XSS (Cross-Site Scripting) attacks.

----------


## Sample Pages

1.  **Signup Page**: A form allowing users to create an account by providing their username, email, and password. After a successful signup, they are redirected to the login page.
    
2.  **Login Page**: Allows users to enter their username and password. If the credentials are correct, they will be redirected to the success page.
    
3.  **Success Page**: Displayed after a successful login, confirming the user’s authentication.

## Scripts

-   To start the Django development server:
    
    bash
  
		    
		    `python manage.py runserver` 
    
-   To migrate the database:
    
    bash
    
    
		    `python manage.py migrate` 
            
    
-   To create a superuser for accessing the admin panel:
    
    bash
    
    
		    `python manage.py createsuperuser` 
    
-   To run uWSGI:
    
    bash
    
    
		    `uwsgi --ini uwsgi.ini`