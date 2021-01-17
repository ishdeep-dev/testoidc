# COSGrid Networks OpenID Test Project

Built with the Django Framework and django-oidc-provider


## Installation

Setup project environment with virtualenv and pip.

```bash
$ virtualenv -p /usr/bin/python3 project_env

$ source project_env/bin/activate

$ pip install -r requirements.txt
```

Run your provider.

```bash
$ python manage.py migrate
$ python manage.py creatersakey
$ python manage.py createsuperuser
$ python manage.py runserver
```

Open your browser and go to `http://localhost:8000`. Voilà!



## Usage

### Obtaining an Access Token

We use the code value to obtain access_token and refresh_token:

```bash
curl -X POST \
    -H "Cache-Control: no-cache" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    "http://localhost:8000/token/" \
    -d "client_id=230337" \
    -d "client_secret=301f441306cbef4c560c436590a1afb79279c44948f47f72fa4b361b" \
    -d "code=4acc9246c11646008ac6fddf36571d92" \
    -d "redirect_uri=http://example.org/" \
    -d "grant_type=authorization_code"
```


Then you can grab the access token and ask for user data by doing a GET request to the /userinfo endpoint:
```bash
curl -X GET \
    -H "Cache-Control: no-cache" \
    "http://localhost:8000/userinfo/?access_token=9e0cda9231084d85bcd8fc1c899b6487"

```
##
### Expiration and Refresh of Access Tokens

If you receive a 401 Unauthorized status when using the access token, this probably means that your access token has expired.

The RP application can request a new access token by using the refresh token. Send a POST request to the /token endpoint with the following request parameters:

```bash
curl -X POST \
    -H "Cache-Control: no-cache" \
    -H "Content-Type: application/x-www-form-urlencoded" \
    "http://localhost:8000/token/" \
    -d "client_id=651462" \
    -d "client_secret=37b1c4ff826f8d78bd45e25bad75a2c0" \
    -d "grant_type=refresh_token" \
    -d "refresh_token=0bac2d80d75d46658b0b31d3778039bb"
```



## Property of
[COSGrid](https://www.cosgrid.com)
