TO VIEW THIS IN VS CODE CLICK 
    Ctlr + Shift + V



### **Step 1: Install Python**  
Ensure you have Python installed. You can check by running:  
```sh
python --version
```
or  
```sh
python3 --version
```
If not installed, download it from [python.org](https://www.python.org/).

---

### **Step 2: Create a Project Directory**  
Navigate to the directory where you want your Django project and create a new folder:  
```sh
mkdir my_project
cd my_project
```

---

### **Step 3: Create and Activate a Virtual Environment**  
Run the following command to create a virtual environment inside your project folder:  
```sh
python -m venv venv
```
Activate the virtual environment:  
- **On Windows (cmd/PowerShell)**:  
  ```sh
  venv\Scripts\activate
  ```
- **On macOS/Linux**:  
  ```sh
  source venv/bin/activate
  ```

---

### **Step 4: Install Django**  
Once the virtual environment is activated, install Django:  
```sh
pip install django
```

Verify installation:  
```sh
django-admin --version
```

---

### **Step 5: Create a Django Project**  
Run the following to create a new Django project:  
```sh
django-admin startproject myproject .
```
(Ensure you include the dot `.` at the end to create the project in the current directory.)

---

### **Step 6: Run Initial Migrations**  
Before starting the app, apply initial migrations:  
```sh
python manage.py migrate
```

---

### **Step 7: Create the Django App**  
Now, you can run:  
```sh
python manage.py startapp home
```

---

### **Step 8: Register the App in `settings.py`**  
Open `myproject/settings.py` and add `'home'` to the `INSTALLED_APPS` list:  
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'home',  # Add this line
]
```

---

### **Step 9: Run the Server to Test**  
To check if everything is set up correctly, start the server:  
```sh
python manage.py runserver
```
Then, visit **http://127.0.0.1:8000/** in your browser.

---

### **Optional: Create a Superuser for Admin Panel**  
If you plan to use the Django admin panel:  
```sh
python manage.py createsuperuser
```
Follow the prompts to set up a username and password.

---

### **Every Time You Work on Your Project**  
Whenever you return to your project, follow these steps:  
1. Navigate to your project directory:  
   ```sh
   cd my_project
   ```
2. Activate the virtual environment:  
   - **Windows:**  
     ```sh
     venv\Scripts\activate
     ```
   - **macOS/Linux:**  
     ```sh
     source venv/bin/activate
     ```
3. Run the server or necessary commands.

---

### **Next steps**  

## **1. Define a View**
Open `home/views.py` and add a basic function-based view:

```python
from django.http import HttpResponse

def home_view(request):
    return HttpResponse("Welcome to the Home Page!")
```

---

## **2. Create a URL Pattern for the App**
1. Inside the `home` folder, create a new file named `urls.py`.  
2. Add the following code to `home/urls.py`:

```python
from django.urls import path
from .views import home_view

urlpatterns = [
    path('', home_view, name='home'),
]
```

---

## **3. Include the App’s URLs in the Main Project**
Now, open `myproject/urls.py` and modify it to include the `home` app's URLs:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('home.urls')),  # Include home app URLs
]
```

---

## **4. Use Templates Instead of HttpResponse**
Django works better with HTML templates. So, let’s change `home_view` to use a template.

1. Inside the `home` folder, create a new folder called `templates`.  
2. Inside `templates`, create another folder named `home` (this helps with organization).  
3. Inside `home/templates/home/`, create a new file named `home.html`.  
4. Add some basic HTML to `home.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Home Page</title>
</head>
<body>
    <h1>Welcome to the Home Page!</h1>
</body>
</html>
```

5. Modify `views.py` to render the template:

```python
from django.shortcuts import render

def home_view(request):
    return render(request, 'home/home.html')
```

---

## **Step 5: Run the Server and Test**
Run the Django server:  
```sh
python manage.py runserver
```
Then visit **http://127.0.0.1:8000/** in your browser. You should see the "Welcome to the Home Page!" message from the template.

---

## **6. Add Static Files (CSS, JS, Images)**
1. Inside `home/`, create a folder called `static`.  
2. Inside `static/`, create another folder named `home/` (for organization).  
3. Inside `home/static/home/`, create a CSS file (`styles.css`) and add some styles:

```css
body {
    background-color: #f4f4f4;
    text-align: center;
}
```

4. Link this CSS file in `home.html`:

```html
<link rel="stylesheet" type="text/css" href="{% static 'home/styles.css' %}">
```

5. To enable static files, open `settings.py` and add this:

```python
from django.conf import settings
from django.conf.urls.static import static

if settings.DEBUG:
    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

With this, the project supports **views, URLs, templates, and static files**!

---

