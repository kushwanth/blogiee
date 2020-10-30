---
layout: post
title:  "Making Django project into PWA"
description: "Making Django project into PWA"
date:   2020-10-30
---
Progressive Web Apps(PWA's), are a type of application that is developed using web technologies and can be installed on any device like a traditional application. Creating a simple PWA is very easy as it involves adding two important files to the project which are manifest.json and serviceworker.js. After that, the PWA would be ready to be installed on any Operating System.

Django is an python based web application framework which is helpful for building variety of web application. Django also includes an extensible Django-Admin interface, Default SQLIte3 database, which is also extensible to PostgreSQL, MySQL databases and few other components to build efficient web apps.

#### Now we will build PWA
Progressive Web Apps(PWA’s), are a type of application that is developed using web technologies and can be installed on any device like a traditional application. We will build PWA for using a PWA library. lets first install it

```python
# installing Django pwa
pip3 install django-pwa
```

Add the PWA library to installed apps in settings file

```python
# adding pwa to installed apps
'pwa',
```

Now we will configure PWA details from settings file, Add the below at last code in settings.py file

```python
PWA_APP_NAME = 'geeksforgeeks'
PWA_APP_DESCRIPTION = "GeeksForGeeks PWA"
PWA_APP_THEME_COLOR = '#000000'
PWA_APP_BACKGROUND_COLOR = '#ffffff'
PWA_APP_DISPLAY = 'standalone'
PWA_APP_SCOPE = '/'
PWA_APP_ORIENTATION = 'any'
PWA_APP_START_URL = '/'
PWA_APP_STATUS_BAR_COLOR = 'default'
PWA_APP_ICONS = [
    {
        'src': '<icon path>',
        'sizes': '160x160'
    }
]
PWA_APP_ICONS_APPLE = [
    {
        'src': '<icon path>',
        'sizes': '160x160'
    }
]
PWA_APP_SPLASH_SCREEN = [
    {
        'src': '<icon path>',
        'media': '(device-width: 320px) and (device-height: 568px) and (-webkit-device-pixel-ratio: 2)'
    }
]
PWA_APP_DIR = 'ltr'
PWA_APP_LANG = 'en-US'
```

We have already added PWA blocks to our templates, So finaly we built our pwa but we got one last thing to do.

Now go to your Django Projects base template and add following tags

```python
{% load pwa %}
<!DOCTYPE html>
<html>
<head>
{% progressive_web_app_meta %}
<!-- your meta, style and script tags -->
</head>
<body>
<!-- you base template -->
</body>
</html>
```

Now go to urls.py file of your django project and add PWA urls

```python
from django.contrib import admin
from django.urls import path, include, re_path
from django.conf import settings
from django.conf.urls.static import static


urlpatterns = [
.....
    # urls handling pwa
    re_path('', include('pwa.urls')),
.....
]
```

Restart your Project and to apply the route. You can also check PWA compatibility using Lighthouse tool.