---
title: admin
date: 2020-05-07
---
Example Python program admin.py

## Modules

* from django.contrib import admin
* from .models import Question, Choice, Document
* import os
* from django.conf import settings

## Classes

* class ChoiceInline(admin.TabularInline):
* class QuestionAdmin(admin.ModelAdmin):
* class DocAdmin(admin.ModelAdmin):

## Methods

* def handleBulkDelete(modeladmin, request, queryset):
* 	def delete_model(self, request, obj):
* 	def get_actions(self, request): # some help on this from the web but no idea if this is doing anything
* 	#def delete_selected(self, request, queryset):

## Code

Python example

    # Register your models here.
    from django.contrib import admin
    from .models import Question, Choice, Document
    import os
    from django.conf import settings
    
    def handleBulkDelete(modeladmin, request, queryset):
    	for obj in queryset:
    		path = os.path.join(settings.MEDIA_ROOT, obj.docfile.name)
    		os.unlink(path)
    		obj.delete()
    
    class ChoiceInline(admin.TabularInline):
    	model = Choice
    	extra = 3
    
    class QuestionAdmin(admin.ModelAdmin):
    	fieldsets = [
    		(None, 				 {'fields': ['question_text']}),
    		('Date information', {'fields': ['pub_date'], 'classes': ['collapse']}),
    	]
    	inlines = [ChoiceInline]
    	list_display = ('question_text', 'pub_date', 'was_published_recently')
    	list_filter = ['pub_date']
    	search_fields = ['question_text']
    
    class DocAdmin(admin.ModelAdmin):
    	def delete_model(self, request, obj):
    	    """
    	    Given a model instance delete it from the database.
    	    """
    	    obj.delete()
    	
    	
    	def get_actions(self, request): # some help on this from the web but no idea if this is doing anything
    		actions = super(DocAdmin, self).get_actions(request)  
    		if request.user.username[0].upper() != 'J':
    			if 'delete_selected' in actions:
    					actions['delete_selected'] = handleBulkDelete  #is this right?!
    		return actions
    
    	#def delete_selected(self, request, queryset):
    	#	print >> "here!"
    	#	for obj in queryset:
    	#		path = os.path.join(settings.MEDIA_ROOT, obj.docfile.name) #get the file to delete from the disk as well
    	##		obj.delete() #delete the reference for it for the model
    		
    
    
    admin.site.register(Question, QuestionAdmin)
    admin.site.register(Document, DocAdmin)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
