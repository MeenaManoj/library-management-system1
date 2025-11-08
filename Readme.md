Library Management System (LMS)
===========================================

This is a backend project built using Django and Django REST Framework (DRF).
It provides APIs for managing Books, Users, and Transactions in a library.

I have used SQLite*as the database because PostgreSQL was causing performance issues
and system lag during testing. SQLite is lightweight and works perfectly for development.
===========================================
Library Management System (LMS)
===========================================

This is a backend project built using Django and Django REST Framework (DRF).
It provides APIs for managing Books, Users, and Transactions in a library.

I have used SQLite as the database because PostgreSQL was causing performance issues
and system lag during testing. SQLite is lightweight and works perfectly for development.

-------------------------------------------
1️  PROJECT SETUP INSTRUCTIONS
-------------------------------------------

Follow these steps to run the project locally on your system.

-------------------------------------------
STEP 1: Clone or Download the Project
-------------------------------------------
If you are using Git:
    git clone https://github.com/your-username/library-management-system.git
    cd library-management-system

If you have the ZIP file:
    - Extract it anywhere on your system.
    - Open Command Prompt or VS Code Terminal inside the project folder.

-------------------------------------------
STEP 2: Create Virtual Environment
-------------------------------------------
To keep dependencies isolated, create a virtual environment.

For Windows:
    python -m venv venv
    venv\Scripts\activate

For macOS/Linux:
    python3 -m venv venv
    source venv/bin/activate

-------------------------------------------
STEP 3: Install Dependencies
-------------------------------------------
Use pip to install all the required packages.

    pip install -r requirements.txt

If the file is missing, install manually:
    pip install django djangorestframework drf-yasg

-------------------------------------------
STEP 4: Apply Migrations
-------------------------------------------
Run the following commands to create all database tables:

    python manage.py makemigrations
    python manage.py migrate

-------------------------------------------
STEP 5: Create a Superuser
-------------------------------------------
To access Django’s admin panel, create an admin account:

    python manage.py createsuperuser

Set username, email, and password as per your choice.

-------------------------------------------
STEP 6: Run the Development Server
-------------------------------------------
Start the local development server:

    python manage.py runserver

If successful, open your browser and visit:

    http://127.0.0.1:8000/

You can also check API documentation here:
    Swagger UI: http://127.0.0.1:8000/swagger/
    Redoc:      http://127.0.0.1:8000/redoc/
    Admin Panel: http://127.0.0.1:8000/admin/

-------------------------------------------
STEP 7: Authentication (if required)
-------------------------------------------
Some endpoints are protected and require authentication.
To access them:
    - Login via admin panel
    - Generate Token or use Django session login
    - Include token in request header:
      Authorization: Token <your_token_here>

-------------------------------------------
STEP 8: Testing the APIs
-------------------------------------------
You can test APIs using:
    - Swagger UI (built-in)
    - Postman
    - curl commands

-------------------------------------------
 The project should now be running successfully on your local machine!
-------------------------------------------


===========================================
2️  HOW TO DEPLOY (HOST) ON AWS EC2
===========================================

Here is the complete process to host this Django project on AWS.

-------------------------------------------
STEP 1: Launch an EC2 Instance
-------------------------------------------
1. Log in to AWS Console.
2. Go to EC2 → Launch Instance.
3. Choose "Ubuntu Server 22.04 LTS" (free tier).
4. Select t2.micro (Free Tier).
5. Add storage (default is fine).
6. Create a new key pair and download it (.pem file).
7. Launch the instance.

-------------------------------------------
STEP 2: Connect to EC2 Instance
-------------------------------------------
From your terminal (on local system):

    chmod 400 your-key.pem
    ssh -i your-key.pem ubuntu@<your-ec2-public-ip>

-------------------------------------------
STEP 3: Install Dependencies on Server
-------------------------------------------
Once logged in to EC2, run:

    sudo apt update
    sudo apt install python3-pip python3-venv nginx git -y

-------------------------------------------
STEP 4: Clone Your Project on Server
-------------------------------------------
    git clone https://github.com/your-username/library-management-system.git
    cd library-management-system

-------------------------------------------
STEP 5: Set Up Virtual Environment
-------------------------------------------
    python3 -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt

-------------------------------------------
STEP 6: Configure Database (SQLite)
-------------------------------------------
Since this project uses SQLite, no database setup is required.
SQLite file will be created automatically after migrations.

Run migrations:
    python manage.py migrate

Create a superuser (optional):
    python manage.py createsuperuser

-------------------------------------------
STEP 7: Test the Server (Optional)
-------------------------------------------
    python manage.py runserver 0.0.0.0:8000

Go to your browser and open:
    http://<EC2-public-IP>:8000/

If you see the Django welcome page or your API, it’s working fine.

-------------------------------------------
STEP 8: Install and Configure Gunicorn
-------------------------------------------
Gunicorn is used to run Django apps in production.

    pip install gunicorn
    gunicorn --bind 0.0.0.0:8000 lms_project.wsgi

If it runs successfully, stop it using Ctrl+C and continue below.

-------------------------------------------
STEP 9: Setup Nginx as a Reverse Proxy
-------------------------------------------
    sudo nano /etc/nginx/sites-available/lms

Add this inside:
-------------------------------------------
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
-------------------------------------------

Enable site:
    sudo ln -s /etc/nginx/sites-available/lms /etc/nginx/sites-enabled
    sudo systemctl restart nginx

-------------------------------------------
STEP 10: Access Your Project from Browser
-------------------------------------------
Now open in your browser:
    http://<Your-EC2-Public-IP>/

You should see your Django API live!

-------------------------------------------
STEP 11: (Optional) Run Gunicorn as a Service
-------------------------------------------
To keep it running in background, create a service file:
    sudo nano /etc/systemd/system/gunicorn.service

Add:
-------------------------------------------
Unit
Description=Gunicorn daemon for LMS
After=network.target

Service
User=ubuntu
Group=www-data
WorkingDirectory=/home/ubuntu/library-management-system
ExecStart=/home/ubuntu/library-management-system/venv/bin/gunicorn --workers 3 --bind unix:/home/ubuntu/library-management-system/lms.sock lms_project.wsgi:application

Install
WantedBy=multi-user.target
-------------------------------------------

Save and start service:
    sudo systemctl start gunicorn
    sudo systemctl enable gunicorn

-------------------------------------------
 Your Django LMS Project is now hosted live on AWS EC2!
-------------------------------------------

===========================================
3️  SUMMARY
===========================================
 Built using Django + DRF  
 Used SQLite for simplicity & system performance  
 Works locally and can be easily deployed on AWS  
Includes Swagger & Redoc for API documentation  

-------------------------------------------
Developed by: Manoj Meena
Backend Developer | Python & Django
-------------------------------------------

-------------------------------------------
1️ PROJECT SETUP INSTRUCTIONS
-------------------------------------------

Follow these steps to run the project locally on your system.

-------------------------------------------
STEP 1: Clone or Download the Project
-------------------------------------------
If you are using Git:
    git clone https://github.com/your-username/library-management-system.git
    cd library-management-system

If you have the ZIP file:
    - Extract it anywhere on your system.
    - Open Command Prompt or VS Code Terminal inside the project folder.

-------------------------------------------
STEP 2: Create Virtual Environment
-------------------------------------------
To keep dependencies isolated, create a virtual environment.

For Windows:
    python -m venv venv
    venv\Scripts\activate

For macOS/Linux:
    python3 -m venv venv
    source venv/bin/activate

-------------------------------------------
STEP 3: Install Dependencies
-------------------------------------------
Use pip to install all the required packages.

    pip install -r requirements.txt

If the file is missing, install manually:
    pip install django djangorestframework drf-yasg

-------------------------------------------
STEP 4: Apply Migrations
-------------------------------------------
Run the following commands to create all database tables:

    python manage.py makemigrations
    python manage.py migrate

-------------------------------------------
STEP 5: Create a Superuser
-------------------------------------------
To access Django’s admin panel, create an admin account:

    python manage.py createsuperuser

Set username, email, and password as per your choice.

-------------------------------------------
STEP 6: Run the Development Server
-------------------------------------------
Start the local development server:

    python manage.py runserver

If successful, open your browser and visit:

    http://127.0.0.1:8000/

You can also check API documentation here:
    Swagger UI: http://127.0.0.1:8000/swagger/
    Redoc:      http://127.0.0.1:8000/redoc/
    Admin Panel: http://127.0.0.1:8000/admin/

-------------------------------------------
STEP 7: Authentication (if required)
-------------------------------------------
Some endpoints are protected and require authentication.
To access them:
    - Login via admin panel
    - Generate Token or use Django session login
    - Include token in request header:
      Authorization: Token <your_token_here>

-------------------------------------------
STEP 8: Testing the APIs
-------------------------------------------
You can test APIs using:
    - Swagger UI (built-in)
    - Postman
    - curl commands

-------------------------------------------
The project should now be running successfully on your local machine!
-------------------------------------------


===========================================
2️ HOW TO DEPLOY (HOST) ON AWS EC2
===========================================

Here is the complete process to host this Django project on AWS.

-------------------------------------------
STEP 1: Launch an EC2 Instance
-------------------------------------------
1. Log in to AWS Console.
2. Go to EC2 → Launch Instance.
3. Choose "Ubuntu Server 22.04 LTS" (free tier).
4. Select t2.micro (Free Tier).
5. Add storage (default is fine).
6. Create a new key pair and download it (.pem file).
7. Launch the instance.

-------------------------------------------
STEP 2: Connect to EC2 Instance
-------------------------------------------
From your terminal (on local system):

    chmod 400 your-key.pem
    ssh -i your-key.pem ubuntu@<your-ec2-public-ip>

-------------------------------------------
STEP 3: Install Dependencies on Server
-------------------------------------------
Once logged in to EC2, run:

    sudo apt update
    sudo apt install python3-pip python3-venv nginx git -y

-------------------------------------------
STEP 4: Clone Your Project on Server
-------------------------------------------
    git clone https://github.com/your-username/library-management-system.git
    cd library-management-system

-------------------------------------------
STEP 5: Set Up Virtual Environment
-------------------------------------------
    python3 -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt

-------------------------------------------
STEP 6: Configure Database (SQLite)
-------------------------------------------
Since this project uses SQLite, no database setup is required.
SQLite file will be created automatically after migrations.

Run migrations:
    python manage.py migrate

Create a superuser (optional):
    python manage.py createsuperuser

-------------------------------------------
STEP 7: Test the Server (Optional)
-------------------------------------------
    python manage.py runserver 0.0.0.0:8000

Go to your browser and open:
    http://<EC2-public-IP>:8000/

If you see the Django welcome page or your API, it’s working fine.

-------------------------------------------
STEP 8: Install and Configure Gunicorn
-------------------------------------------
Gunicorn is used to run Django apps in production.

    pip install gunicorn
    gunicorn --bind 0.0.0.0:8000 lms_project.wsgi

If it runs successfully, stop it using Ctrl+C and continue below.

-------------------------------------------
STEP 9: Setup Nginx as a Reverse Proxy
-------------------------------------------
    sudo nano /etc/nginx/sites-available/lms

Add this inside:
-------------------------------------------
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
-------------------------------------------

Enable site:
    sudo ln -s /etc/nginx/sites-available/lms /etc/nginx/sites-enabled
    sudo systemctl restart nginx

-------------------------------------------
STEP 10: Access Your Project from Browser
-------------------------------------------
Now open in your browser:
    http://<Your-EC2-Public-IP>/

You should see your Django API live!

-------------------------------------------
STEP 11: (Optional) Run Gunicorn as a Service
-------------------------------------------
To keep it running in background, create a service file:
    sudo nano /etc/systemd/system/gunicorn.service

Add:
-------------------------------------------
Description=Gunicorn daemon for LMS
After=network.target

User=ubuntu
Group=www-data
WorkingDirectory=/home/ubuntu/library-management-system
ExecStart=/home/ubuntu/library-management-system/venv/bin/gunicorn --workers 3 --bind unix:/home/ubuntu/library-management-system/lms.sock lms_project.wsgi:application

[Install]
WantedBy=multi-user.target
-------------------------------------------

Save and start service:
    sudo systemctl start gunicorn
    sudo systemctl enable gunicorn

-------------------------------------------
 Your Django LMS Project is now hosted live on AWS EC2!
-------------------------------------------

===========================================
3 SUMMARY
===========================================
 Built using Django + DRF  
 Used SQLite for simplicity & system performance  
 Works locally and can be easily deployed on AWS  
 Includes Swagger & Redoc for API documentation  


Developed by: Manoj Meena
Backend Developer | Python & Django

