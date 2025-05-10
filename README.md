# NotesHub

NotesHub is a Django-based web platform designed for IIT Bombay students to efficiently access and share academic resources. Users can browse, upload, and provide feedback on study materials, lecture notes, and previous year question papers, organized by courses. The platform features a robust search function for quick resource discovery and a feedback system to ensure high-quality content.

## Features

- **Course-Based Navigation**: Resources are systematically organized by courses.
- **Quick Search**: Locate specific notes or question papers instantly with a keyword search.
- **User Contributions**: Students can upload their own notes or question papers.
- **Feedback Mechanism**: Rate and comment on resources to highlight the best materials.
- **Responsive UI**: Optimized for seamless use across desktops and mobile devices.

## Tech Stack

- **Backend**: Django (Python)
- **Frontend**: HTML, CSS, JavaScript
- **Database**: SQLite (configurable for PostgreSQL or other databases)
- **Dependencies**: Listed in `requirements.txt`

## Prerequisites

Ensure the following are installed before setup:

- Python 3.8 or higher
- pip (Python package manager)
- Git
- (Optional) Virtualenv for environment isolation

## Setup Instructions

To run NotesHub locally, follow these steps:

1. **Clone the Repository**
   ```bash
   git clone https://github.com/puneet2601/NotesHub.git
   cd NotesHub
2. **Create a Virtual Environment** (Optional but recommended)
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
3. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
4. **Configure Environment Variables**  
    Create a ```.env``` file in your project's root directory to store sensitive settings:
    ```bash
    touch .env
    ```
    Add the following to ```.env```
    ```bash
    DJANGO_SECRET_KEY=your-django-secret-key-here
    ```
5. **Google Cloud Platform Setup**  
NotesHub integrates with Google Drive to store and retrieve uploaded files. To configure:  
    1. **Create a GCP Project**  
        * Go to the [Google Cloud Console](https://developers.google.com/workspace/guides/create-project) and create a new project.
    2. **Enable the Drive API**  
        * In your project, navigate to **APIs & Services > Library**, search for "Google Drive API", and click **Enable**.
    3. **Create Service Account Credentials**
        * Go to **APIs & Services > Credentials > Create Credentials > Service account**.
        * Give the service account a name and grant it the **Editor** role (or least permissions required).
        * After creation, under **Keys**, click **Add Key > Create new key** and select JSON. This will download a ```credentials.json``` file.
        * Move the ```credentials.json``` file to your project's directory.
    4. **Configure Django Settings**
        * In ```settings.py``` add:
        ```bash
        from decouple import config
        # load secret key from .env file
        SECRET_KEY = config('DJANGO_SECRET_KEY')
        # Google Drive storage configuration
        GOOGLE_DRIVE_STORAGE_JSON_KEY_FILE = 'credentials.json'
        GOOGLE_DRIVE_STORAGE_MEDIA_ROOT = 'YOUR_DIRECTORY_NAME_IN_GCP'
        ```
6. **Apply Database Migrations**
   ```bash
   python manage.py migrate
7. **Launch the Development Server**
   ```bash
   python manage.py runserver
8. **Access the Platform** Visit the following URL in your browser:
   ```bash
   http://127.0.0.1:8000/
   
## Usage Guide

* **Explore Resources**: Browse materials by course categories.
* **Search Materials**: Use the search bar to find specific resources.
* **Upload Content**: Authenticated users can upload notes or papers.
* **Provide Feedback**: Rate or comment to improve resource quality.