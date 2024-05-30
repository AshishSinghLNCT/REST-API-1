from selenium import webdriver
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.common.desired_capabilities import DesiredCapabilities
import time
import time
import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
from email.mime.image import MIMEImage

def send_email():
    subject = 'Python (Selenium) Assignment - Ashish Singh'
    email_from = 'ashishzoom1991@gmail.com'
    email_to = ['tech@themedius.ai']
    email_cc = ['HR@themedius.ai']
    email_body = 'Please find the screenshot of the confirmation page attached.'

   
    msg = MIMEMultipart()
    msg['Subject'] = subject
    msg['From'] = email_from
    msg['To'] = ', '.join(email_to)
    msg['Cc'] = ', '.join(email_cc)

    msg.attach(MIMEText(email_body, 'plain'))

    with open('FORM SUBMITTED.jpg', 'rb') as f:
        img = MIMEImage(f.read())
        img.add_header('Content-Disposition', 'attachment', filename='FORM SUBMITTED.jpg')
        msg.attach(img)
     
    with open('APPROACH.txt', 'r') as f:
        txt1 = MIMEText(f.read())
        txt1.add_header('Content-Disposition', 'attachment', filename='APPROACH.txt')
        msg.attach(txt1)

   
    with open('CODES.txt', 'r') as f:
        txt2 = MIMEText(f.read())
        txt2.add_header('Content-Disposition', 'attachment', filename='CODES.txt')
        msg.attach(txt2)

    smtp_server = 'smtp.gmail.com'
    smtp_port = 587
    smtp_username = 'ashishzoom1991@gmail.com'
    smtp_password = 'Ashish1991'
    
    with smtplib.SMTP(smtp_server, smtp_port) as server:
        server.starttls()
        server.login(smtp_username, smtp_password)
        server.send_message(msg)

send_email()

