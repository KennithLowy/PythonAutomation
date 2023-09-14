# PythonAutomation
Practice new class work on Python automation in the cloud
import os
import random
import sendgrid
from sendgrid.helpers.mail import Mail, Email, To, Content

# Set your SendGrid API key
SENDGRID_API_KEY = 'YOUR_SENDGRID_API_KEY'

# Initialize SendGrid client
sg = sendgrid.SendGridAPIClient(api_key=SENDGRID_API_KEY)

# List of random quotes
quotes = [
    "The only way to do great work is to love what you do. - Steve Jobs",
    "Innovation distinguishes between a leader and a follower. - Steve Jobs",
    "Your time is limited, don't waste it living someone else's life. - Steve Jobs"
]

# Cloud Function entry point
def send_random_quote(request):
    # Select a random quote
    random_quote = random.choice(quotes)
    
    # Define email content
    from_email = Email("your_email@example.com")
    to_email = To("recipient@example.com")
    subject = "Your Daily Random Quote"
    content = Content("text/plain", random_quote)

    # Create a SendGrid email
    mail = Mail(from_email, to_email, subject, content)

    # Send the email
    try:
        response = sg.client.mail.send.post(request_body=mail.get())
        return f"Email sent with status code: {response.status_code}"
    except Exception as e:
        return f"Email sending failed with error: {str(e)}"
