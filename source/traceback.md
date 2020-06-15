---
title: traceback
date: 2020-05-07
---
Example Python program traceback.py


## Code

Python example

    Internal Server Error: /admin/sponsors/sponsor/2/
    Traceback (most recent call last):
      File "/app/.heroku/python/lib/python3.4/site-packages/django/core/handlers/base.py", line 111, in get_response
        response = wrapped_callback(request, *callback_args, **callback_kwargs)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/contrib/admin/options.py", line 567, in wrapper
        return self.admin_site.admin_view(view)(*args, **kwargs)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/utils/decorators.py", line 105, in _wrapped_view
        response = view_func(request, *args, **kwargs)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/views/decorators/cache.py", line 52, in _wrapped_view_func
        response = view_func(request, *args, **kwargs)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/contrib/admin/sites.py", line 204, in inner
        return view(request, *args, **kwargs)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/contrib/admin/options.py", line 1440, in change_view
        return self.changeform_view(request, object_id, form_url, extra_context)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/utils/decorators.py", line 29, in _wrapper
        return bound_func(*args, **kwargs)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/utils/decorators.py", line 105, in _wrapped_view
        response = view_func(request, *args, **kwargs)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/utils/decorators.py", line 25, in bound_func
        return func.__get__(self, type(self))(*args2, **kwargs2)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/db/transaction.py", line 394, in inner
        return func(*args, **kwargs)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/contrib/admin/options.py", line 1388, in changeform_view
        self.save_model(request, new_object, form, not add)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/contrib/admin/options.py", line 1029, in save_model
        obj.save()
      File "/app/.heroku/python/lib/python3.4/site-packages/django/db/models/base.py", line 590, in save
        force_update=force_update, update_fields=update_fields)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/db/models/base.py", line 618, in save_base
        updated = self._save_table(raw, cls, force_insert, force_update, using, update_fields)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/db/models/base.py", line 677, in _save_table
        for f in non_pks]
      File "/app/.heroku/python/lib/python3.4/site-packages/django/db/models/base.py", line 677, in <listcomp>
        for f in non_pks]
      File "/app/.heroku/python/lib/python3.4/site-packages/django/db/models/fields/files.py", line 301, in pre_save
        file.save(file.name, file, save=False)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/db/models/fields/files.py", line 88, in save
        name = self.field.generate_filename(self.instance, name)
      File "/app/.heroku/python/lib/python3.4/site-packages/django/db/models/fields/files.py", line 315, in generate_filename
        return os.path.join(self.get_directory_name(), self.get_filename(filename))
      File "/app/.heroku/python/lib/python3.4/site-packages/django/db/models/fields/files.py", line 312, in get_filename
        return os.path.normpath(self.storage.get_valid_name(os.path.basename(filename)))
      File "/app/.heroku/python/lib/python3.4/site-packages/django/utils/functional.py", line 224, in inner
        self._setup()
      File "/app/.heroku/python/lib/python3.4/site-packages/django/core/files/storage.py", line 308, in _setup
        self._wrapped = get_storage_class()()
      File "/app/.heroku/python/lib/python3.4/site-packages/storages/backends/s3boto.py", line 141, in __init__
        access_key, secret_key = self._get_access_keys()
      File "/app/.heroku/python/lib/python3.4/site-packages/storages/backends/s3boto.py", line 176, in _get_access_keys
        secret_key = os.environ.get(SECRET_KEY_NAME)
      File "/app/.heroku/python/lib/python3.4/_collections_abc.py", line 406, in get
        return self[key]
      File "/app/.heroku/python/lib/python3.4/os.py", line 628, in __getitem__
        value = self._data[self.encodekey(key)]
      File "/app/.heroku/python/lib/python3.4/os.py", line 704, in encode
        raise TypeError("str expected, not %s" % type(value).__name__)
    TypeError: str expected, not NoneType

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
