# Deploying Padapunja to PythonAnywhere

This guide will walk you through deploying your Kannada Idioms Translator application to PythonAnywhere for free.

## Why PythonAnywhere?

- ✅ **Free tier** with no credit card required
- ✅ **MySQL support** - No database migration needed!
- ✅ **Always-on** - No cold starts or sleeping
- ✅ **Easy setup** - Perfect for Flask applications

---

## Prerequisites

- GitHub account with your code pushed
- Gmail account for sending OTP emails
- Gmail App Password ([How to create](https://support.google.com/accounts/answer/185833))

---

## Step-by-Step Deployment Guide

### Step 1: Create PythonAnywhere Account

1. Go to [https://www.pythonanywhere.com](https://www.pythonanywhere.com)
2. Click **"Start running Python online in less than a minute!"**
3. Choose the **Beginner** account (Free)
4. Sign up with your email
5. Verify your email address

### Step 2: Open a Bash Console

1. Once logged in, go to the **Dashboard**
2. Click on **"Consoles"** tab
3. Click **"Bash"** to open a new bash console

### Step 3: Clone Your Repository

In the bash console, run:

```bash
git clone https://github.com/AbhishekP141003/Padapunja.git
cd Padapunja
```

### Step 4: Create Virtual Environment

```bash
mkvirtualenv --python=/usr/bin/python3.11 padapunja-env
```

This creates a Python 3.11 virtual environment. PythonAnywhere will automatically activate it.

### Step 5: Install Dependencies

```bash
pip install -r requirements.txt
```

⏱️ This may take 5-10 minutes due to the many dependencies.

### Step 6: Create MySQL Database

1. Go to the **"Databases"** tab in PythonAnywhere dashboard
2. Under **"Create a new database"**, enter: `kannada_db`
3. Click **"Create"**
4. Note down your database details:
   - **Host**: `YOUR_USERNAME.mysql.pythonanywhere-services.com`
   - **Database name**: `YOUR_USERNAME$kannada_db`
   - **Username**: Your PythonAnywhere username
   - **Password**: Set a password (you'll need this!)

### Step 7: Import Database Schema

In the bash console:

```bash
mysql -u YOUR_USERNAME -h YOUR_USERNAME.mysql.pythonanywhere-services.com -p 'YOUR_USERNAME$kannada_db' < schema.sql
```

Enter your MySQL password when prompted.

### Step 8: Configure Environment Variables

Create a `.env` file:

```bash
nano .env
```

Paste the following (replace with your actual values):

```env
FLASK_SECRET=your_random_secret_key_here_min_32_chars
DATABASE_URL=mysql+pymysql://YOUR_USERNAME:YOUR_MYSQL_PASSWORD@YOUR_USERNAME.mysql.pythonanywhere-services.com/YOUR_USERNAME$kannada_db?charset=utf8mb4
MAIL_USERNAME=your_email@gmail.com
MAIL_PASSWORD=your_gmail_app_password
ADMIN_EMAIL=admin@example.com
ADMIN_PASSWORD=your_admin_password
FLASK_ENV=production
```

**Important**: 
- Replace `YOUR_USERNAME` with your PythonAnywhere username
- Replace `YOUR_MYSQL_PASSWORD` with the password you set in Step 6
- Use a Gmail **App Password**, not your regular password

Save and exit: Press `Ctrl+X`, then `Y`, then `Enter`

### Step 9: Create Web App

1. Go to the **"Web"** tab in PythonAnywhere dashboard
2. Click **"Add a new web app"**
3. Click **"Next"** (for the free domain)
4. Select **"Manual configuration"**
5. Choose **Python 3.11**
6. Click **"Next"**

### Step 10: Configure WSGI File

1. In the **Web** tab, scroll to **"Code"** section
2. Click on the **WSGI configuration file** link (it will be something like `/var/www/YOUR_USERNAME_pythonanywhere_com_wsgi.py`)
3. **Delete all the content** in the file
4. Paste the following:

```python
import sys
import os

# Add your project directory to the sys.path
project_home = '/home/YOUR_USERNAME/Padapunja'
if project_home not in sys.path:
    sys.path.insert(0, project_home)

# Load environment variables from .env file
from dotenv import load_dotenv
load_dotenv(os.path.join(project_home, '.env'))

# Import your Flask app
from app import create_app

application = create_app()
```

**Replace `YOUR_USERNAME`** with your PythonAnywhere username.

5. Click **"Save"** (top right)

### Step 11: Configure Virtual Environment

1. Still in the **Web** tab, scroll to **"Virtualenv"** section
2. Click **"Enter path to a virtualenv"**
3. Enter: `/home/YOUR_USERNAME/.virtualenvs/padapunja-env`
4. Click the checkmark ✓

### Step 12: Configure Static Files

1. Scroll to **"Static files"** section
2. Click **"Enter URL"** and type: `/static/`
3. Click **"Enter path"** and type: `/home/YOUR_USERNAME/Padapunja/static/`
4. Click the checkmark ✓

### Step 13: Reload Your Web App

1. Scroll to the top of the **Web** tab
2. Click the big green **"Reload"** button
3. Wait for it to finish reloading

### Step 14: Test Your Application

1. Click on your app URL (e.g., `YOUR_USERNAME.pythonanywhere.com`)
2. Your application should load! 🎉

---

## Testing Checklist

- [ ] Homepage loads without errors
- [ ] Can enter email and request OTP
- [ ] OTP email is received
- [ ] Can verify OTP and login
- [ ] Can search for idioms
- [ ] Admin login works at `/admin/login`
- [ ] Admin can add/edit idioms

---

## Troubleshooting

### Error: "Something went wrong"

1. Go to **Web** tab
2. Click on **"Error log"** link
3. Check the latest errors
4. Common issues:
   - Wrong database credentials in `.env`
   - Virtual environment not configured
   - Missing dependencies

### Email OTP Not Sending

1. Verify you're using a Gmail **App Password**, not your regular password
2. Check error logs for SMTP errors
3. Make sure `MAIL_USERNAME` and `MAIL_PASSWORD` are correct in `.env`

### Database Connection Error

1. Verify database name format: `YOUR_USERNAME$kannada_db`
2. Check MySQL password is correct
3. Ensure database was created in Step 6

### Static Files Not Loading (CSS/JS missing)

1. Check **Static files** configuration in Web tab
2. Verify path is correct: `/home/YOUR_USERNAME/Padapunja/static/`
3. Reload the web app

### Import Errors

1. Make sure virtual environment is activated:
   ```bash
   workon padapunja-env
   ```
2. Reinstall requirements:
   ```bash
   pip install -r requirements.txt
   ```

---

## Updating Your Application

When you make changes to your code:

1. **Push to GitHub**:
   ```bash
   git add .
   git commit -m "Your changes"
   git push
   ```

2. **Pull on PythonAnywhere** (in bash console):
   ```bash
   cd ~/Padapunja
   git pull
   ```

3. **Reload web app** in the Web tab

---

## Environment Variables Reference

| Variable | Description | Example |
|----------|-------------|---------|
| `FLASK_SECRET` | Secret key for Flask sessions | Random 32+ character string |
| `DATABASE_URL` | MySQL connection string | `mysql+pymysql://user:pass@host/db` |
| `MAIL_USERNAME` | Gmail address for OTP | `your_email@gmail.com` |
| `MAIL_PASSWORD` | Gmail App Password | 16-character app password |
| `ADMIN_EMAIL` | Admin login email | `admin@example.com` |
| `ADMIN_PASSWORD` | Admin login password | Strong password |

---

## Free Tier Limitations

- **CPU seconds**: 100 seconds/day (resets daily)
- **Disk space**: 512 MB
- **One web app**: Can only host one application
- **Always-on**: Your app is always running (no sleeping!)

For most small projects, these limits are sufficient.

---

## Getting Help

- **PythonAnywhere Forums**: [https://www.pythonanywhere.com/forums/](https://www.pythonanywhere.com/forums/)
- **PythonAnywhere Help**: [https://help.pythonanywhere.com/](https://help.pythonanywhere.com/)
- **Your Error Logs**: Web tab → Error log link

---

## Next Steps

Once deployed successfully:

1. ✅ Test all features thoroughly
2. ✅ Share your app URL with others
3. ✅ Monitor error logs regularly
4. ✅ Keep your GitHub repo updated

Your app URL will be: `https://YOUR_USERNAME.pythonanywhere.com`

**Congratulations! Your Padapunja app is now live! 🎉**
