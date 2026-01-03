# Padapunja - Kannada Idioms Translator

A web application for translating and learning Kannada idioms with their meanings and usage examples.

## Features

- 🔍 Search and translate Kannada idioms
- 📚 Comprehensive database of Kannada idioms
- 👤 User authentication with OTP verification
- 🔐 Admin panel for managing idioms
- 📧 Email-based OTP verification
- 💾 MySQL database for data persistence

## Tech Stack

- **Backend**: Python Flask
- **Database**: MySQL
- **Frontend**: HTML, CSS, JavaScript
- **Authentication**: Email OTP verification
- **Email Service**: SMTP (Gmail)

## Prerequisites

- Python 3.11.9 or higher
- MySQL Server
- Gmail account for SMTP (or other email service)

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/AbhishekP141003/Padapunja.git
   cd Padapunja
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   venv\Scripts\activate  # On Windows
   # source venv/bin/activate  # On macOS/Linux
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up MySQL database**
   - Create a new MySQL database
   - Import the schema:
     ```bash
     mysql -u your_username -p your_database_name < schema.sql
     ```

5. **Configure environment variables**
   Create a `.env` file in the root directory with the following:
   ```env
   SECRET_KEY=your_secret_key_here
   DATABASE_HOST=localhost
   DATABASE_USER=your_mysql_username
   DATABASE_PASSWORD=your_mysql_password
   DATABASE_NAME=your_database_name
   MAIL_USERNAME=your_email@gmail.com
   MAIL_PASSWORD=your_app_password
   ADMIN_EMAIL=admin@example.com
   ADMIN_PASSWORD=your_admin_password
   ```

   **Note**: For Gmail, you need to use an [App Password](https://support.google.com/accounts/answer/185833) instead of your regular password.

6. **Run the application**
   ```bash
   python app.py
   ```

7. **Access the application**
   Open your browser and navigate to `http://localhost:5000`

## Project Structure

```
Padapunja/
├── app.py              # Application entry point
├── routes.py           # Route definitions
├── models.py           # Database models
├── extensions.py       # Flask extensions
├── utils.py            # Utility functions
├── schema.sql          # Database schema
├── requirements.txt    # Python dependencies
├── .env               # Environment variables (not in repo)
├── .gitignore         # Git ignore file
├── Main Dataset.tsv   # Idioms dataset
├── static/            # Static files (CSS, JS, images)
│   └── js/
│       └── main.js
└── templates/         # HTML templates
    ├── index.html
    ├── login.html
    ├── verify.html
    ├── admin_login.html
    └── admin.html
```

## Usage

### For Users
1. Visit the home page
2. Enter your email to login
3. Verify your email with the OTP sent
4. Search for Kannada idioms and view translations

### For Admins
1. Navigate to `/admin/login`
2. Login with admin credentials
3. Manage idioms database through the admin panel

## Deployment

This application can be deployed on platforms like:
- Render
- Heroku
- Railway
- PythonAnywhere

Make sure to:
- Set all environment variables on your hosting platform
- Use a production-ready database (not local MySQL)
- Configure SMTP settings for email functionality

## Environment Variables

| Variable | Description |
|----------|-------------|
| `SECRET_KEY` | Flask secret key for sessions |
| `DATABASE_HOST` | MySQL host address |
| `DATABASE_USER` | MySQL username |
| `DATABASE_PASSWORD` | MySQL password |
| `DATABASE_NAME` | Database name |
| `MAIL_USERNAME` | Email address for sending OTPs |
| `MAIL_PASSWORD` | Email app password |
| `ADMIN_EMAIL` | Admin login email |
| `ADMIN_PASSWORD` | Admin login password |

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License.

## Contact

For any queries or support, please contact [your-email@example.com]

## Acknowledgments

- Kannada idioms dataset
- Flask framework
- MySQL database
