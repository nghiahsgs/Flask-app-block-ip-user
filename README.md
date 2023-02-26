# Flask-app-block-ip-user
Flask app block ip user

Assume we only want a specific IP can access your website: ALLOWED_IP

```
from flask import Flask, request

app = Flask(__name__)

# Define the IP address that is allowed to access the app
ALLOWED_IP = '192.46.231.188'

# Define a decorator function that checks the IP address of incoming requests
def require_ip(func):
    def wrapper(*args, **kwargs):
        if request.remote_addr != ALLOWED_IP:
            return "Access denied", 403
        return func(*args, **kwargs)
    return wrapper

# Apply the require_ip decorator to a route
@app.route('/')
@require_ip
def hello():
    return "Hello, world!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8081)
```
