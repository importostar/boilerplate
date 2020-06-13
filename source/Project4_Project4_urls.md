---
title: Project4_Project4_urls
date: 2020-05-07
---
Example Python program Project4_Project4_urls.py

## Modules

* 1. Add an import:  from my_app import views
* 1. Add an import:  from other_app.views import Home
* 1. Import the include() function: from django.conf.urls import url, include
* from django.conf.urls import url
* from django.contrib import admin

## Code

Python example

    """Project4 URL Configuration
    
    The `urlpatterns` list routes URLs to views. For more information please see:
        https://docs.djangoproject.com/en/1.10/topics/http/urls/
    Examples:
    Function views
        1. Add an import:  from my_app import views
        2. Add a URL to urlpatterns:  url(r'^$', views.home, name='home')
    Class-based views
        1. Add an import:  from other_app.views import Home
        2. Add a URL to urlpatterns:  url(r'^$', Home.as_view(), name='home')
    Including another URLconf
        1. Import the include() function: from django.conf.urls import url, include
        2. Add a URL to urlpatterns:  url(r'^blog/', include('blog.urls'))
    """
    from django.conf.urls import url
    from django.contrib import admin
    
    urlpatterns = [
        url(r'^admin/', admin.site.urls),
    ]
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
