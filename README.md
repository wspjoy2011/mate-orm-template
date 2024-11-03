# Django ORM Project Template

This project is a minimal Django setup designed for working with Django ORM in a simple structure. 
The project includes configurations for setting up models, writing queries, and running them independently of a full 
Django application.

## Project Structure

```
.
├── README.md
├── db
│   ├── __init__.py
│   ├── migrations
│   │   └── __init__.py
│   ├── models.py         # Define Django models here
│   └── queries.py        # Write Django ORM queries here
├── init_django_orm.py    # Initializes Django ORM for standalone use
├── manage.py             # Django management commands
├── requirements.txt      # Project dependencies
└── settings.py           # Minimal Django settings configuration
```

### Files Overview

- `db/models.py`: Contains the definitions of the database models used by Django ORM.
- `db/queries.py`: Where you can write and run Django ORM queries.
- `init_django_orm.py`: Sets up Django ORM outside of Django's typical runtime, allowing scripts to run independently.
- `settings.py`: Minimal configuration for Django, connecting to an SQLite database.
- `requirements.txt`: Lists all dependencies for the project, including Django and `django-extensions`.

## Requirements

- Python 3.10 or higher
- [pip](https://pip.pypa.io/en/stable/installation/)

## Installation

1. **Clone the repository**:
    ```bash
    git clone https://github.com/wspjoy2011/mate-orm-template.git
    cd mate-orm-template
    ```

2. **Create a virtual environment**:
    ```bash
    python -m venv venv
    source venv/bin/activate   # On Windows: venv\Scripts\activate
    ```

3. **Install dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

## Database Setup

1. **Apply Migrations**:
    Run the following command to create tables in your SQLite database based on models in `db/models.py`:
    ```bash
    python manage.py migrate
    ```

2. **Create Migrations for Models**:
    If you add new models or update existing ones, create migrations:
    ```bash
    python manage.py makemigrations
    ```

## Usage

### Running Django Shell

To interact with the database and test ORM queries, start the Django shell:
```bash
python manage.py shell
```

### Running Queries

You can write queries in `db/queries.py` and run them independently. 
This script is prepared to work with Django ORM using `init_django_orm.py`.

1. Open `db/queries.py`.
2. Write your query using Django ORM syntax.
3. Run the file using:
    ```bash
    python db/queries.py
    ```

### Example Query

In `db/queries.py`, you can write queries like:
```
from db.models import Movie

# Example: Get all movies
movies = Movie.objects.all()
for movie in movies:
    print(movie.name)
```

## Additional Tools

The project includes `django-extensions`, which provides extra Django management commands. To see available commands:
```bash
python manage.py help
```

## Configuring Django Support in PyCharm

To enable Django support in PyCharm, follow these steps:

1. **Open Settings**:
   - In PyCharm, go to **File** -> **Settings** (on macOS: **PyCharm** -> **Preferences**).

2. **Navigate to Django Settings**:
   - In the **Settings** window, go to **Languages & Frameworks** -> **Django**.

3. **Enable Django Support**:
   - Check the box **"Enable Django Support"** if it’s available.

4. **Configure Django Project Settings**:
   - **Django project root**: Set this to the root directory of your Django project (where `manage.py` is located).
   - **Settings**: Point to the `settings.py` file. In this project, it would be `settings.py` in the root directory.
   - **Manage script**: Select the `manage.py` file, located in the root directory.

5. **Apply and Close**:
   - Click **Apply** and then **OK** to save the configuration.

6. **Restart or Reload PyCharm** (if needed):
   - Sometimes a restart is necessary to fully initialize Django support.

To modify the starting script for the Django console in PyCharm and enable it to launch with `shell_plus`, follow these steps:

1. **Open Settings**:
   - Go to **File** -> **Settings** (on macOS: **PyCharm** -> **Preferences**).

2. **Navigate to Console Settings**:
   - Go to **Build, Execution, Deployment** -> **Console** -> **Django Console**.

3. **Modify the Starting Script**:
   - In the **Starting script** field, replace the existing script with the following:

   ```
   import sys;
   print("Python {} on {}".format(sys.version, sys.platform))
   import django;
   print("Django {}".format(django.get_version()))
   sys.path.extend([WORKING_DIR_AND_PYTHON_PATHS])
   if "setup" in dir(django): django.setup()
   
   from django_extensions.management.shells import import_objects
   from django.core.management.color import color_style
   
   style = color_style(force_color=True)
   globals().update(import_objects({"dont_load": [], "quiet_load": False}, style))
   
   from django_extensions.management.debug_cursor import monkey_patch_cursordebugwrapper
   monkey_patch_cursordebugwrapper(print_sql=True).__enter__()  # activate monkey patch inside context manager
   
   import django_manage_shell;
   django_manage_shell.run(PROJECT_ROOT)
   ```

4. **Apply and Close**:
   - Click **Apply** and then **OK** to save the changes.

#### Explanation

This modified script sets up the Django console to use `shell_plus` from `django-extensions`, which automatically 
imports all models and essential modules when starting the Django shell. 
Additionally, `monkey_patch_cursordebugwrapper(print_sql=True)` enables SQL query debugging, 
printing each SQL query executed in the console.

Now, when you open the Django console in PyCharm, it will launch with `shell_plus`, allowing easier access to all models
and enhanced debugging features.

## License

This project is licensed under the MIT License.

