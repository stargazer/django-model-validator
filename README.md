[![Build Status](https://travis-ci.org/stargazer/django-model-validator.png?branch=master)](https://travis-ci.org/stargazer/django-model-validator)
[![Coverage Status](https://coveralls.io/repos/stargazer/django-model-validator/badge.png?branch=master)](https://coveralls.io/r/stargazer/django-model-validator?branch=master)
[![PyPI version](https://badge.fury.io/py/django-model-validator.svg)](http://badge.fury.io/py/django-model-validator)
[![PyPI](https://img.shields.io/pypi/dm/django-model-validator.svg)](https://pypi.python.org/pypi/django-model-validator/)

# Django Model Validator

A Django Mixin capable of converting python data structures to clean Django models.

In detail:
 * It can convert dictionaries of data or lists of dictionaries, to Django model instances

  * For security, only specified dictionary keys are allowed to *slip* into the models

 * Validates models, running them through [*full_clean*](https://docs.djangoproject.com/en/1.8/ref/models/instances/#django.db.models.Model.full_clean)

Tested in ``Python 2.7`` and ``Python 3.2`` against ``Django >= 1.5``.

## How to install

    pip install django-model-validator

## How to use

Simply have your Class-Based View inherit from 
``model_validator.mixins.ModelValidationMixin``. From that point on, the view can use the ``validate`` method directly.

In the following example, the ``validate`` method transforms ``data`` into a *clean* instance of the ``User`` model

```python
from model_validator.mixins import ModelValidationMixin
from django.views.generic.base import View
from django.contrib.auth.models import User

class MyView(View, ModelValidationMixin):
    def post(self, request, *args, **kwargs):
        data = {
            'id': 1,
            'first_name': 'Randy',
            'last_name': 'Marsh',
            'username': 'randy'
        }

        user = self.validate(data, User, 
                             allowed_fields=['first_name', 'last_name', 'username'])
```

             


