---
title: wordpresspython
date: 2020-05-07
---
Example Python program wordpresspython.py
For Python version 2.x.
To test your Python version use:

    python --version

## Modules

* import datetime, xmlrpclib
* import urllib
* from wordpress_xmlrpc import Client, WordPressPost
* from wordpress_xmlrpc.methods import posts
* import xmlrpclib
* from wordpress_xmlrpc.compat import xmlrpc_client
* from wordpress_xmlrpc.methods import media, posts
* import os

## Classes

* class Custom_WP_XMLRPC:

## Methods

* 	def post_article(self,wpUrl,wpUserName,wpPassword,articleTitle, articleCategories, articleContent, articleTags,PhotoUrl):

## Code

Python example

    import datetime, xmlrpclib
     2 
     3 wp_url = "http://www.yourblog.com/xmlrpc.php"
     4 wp_username = "USERNAME"
     5 wp_password = "PASSWD"
     6 wp_blogid = ""
     7 status_draft = 0
     8 status_published = 1
     9 
    10 server = xmlrpclib.ServerProxy(wp_url)
    11 
    12 title = "Title with spaces"
    13 content = "Body with lots of content"
    14 date_created = xmlrpclib.DateTime(datetime.datetime.strptime("2011-10-20 21:08", "%Y-%m-%d %H:%M"))
    15 categories = ["category here"]
    16 tags = ["sometag", "othertag"] 
    17 data = {'title': title, 'description': content, 'dateCreated': date_created, 'categories': categories, 'mt_keywords': tags}
    18 
    19 post_id = server.metaWeblog.newPost(wp_blogid, wp_username, wp_password, data, status_published)
    
    ------------------------------------------------------------------------------------------------------------------------
    
    import urllib
    from wordpress_xmlrpc import Client, WordPressPost
    from wordpress_xmlrpc.methods import posts
    import xmlrpclib
    from wordpress_xmlrpc.compat import xmlrpc_client
    from wordpress_xmlrpc.methods import media, posts
    import os
    ########################### Read Me First ###############################
    '''
    ------------------------------------------In DETAIL--------------------------------
    Description
    ===========
    Add new posts to WordPress remotely using Python using XMLRPC library provided by the WordPress.
    
    Installation Requirement
    ************************
    Verify you meet the following requirements
    ==========================================
    Install Python 2.7 (Don't download 3+, as most libraries dont yet support version 3). 
    Install from PyPI using easy_install python-wordpress-xmlrpc 
    Easy_Install Link: https://pypi.python.org/pypi/setuptools
    ==========================================
    
    Windows Installation Guide
    ==========================
    -Download and Install Easy_Install from above Link -Extract Downloaded File and from CMD go to the extracted directory and run 'python setup.py install'. This will install easy_install. -Go to %/python27/script and run following command easy_install python-wordpress-xmlrpc
    
    Ubuntu Installation Guide
    =========================
    sudo apt-get install python-setuptools 
    sudo easy_install python-wordpress-xmlrpc
    
    Note: Script has its dummy data to work initially which you can change or integrate with your code easily for making it more dynamic.
    
    ****************************************
    For Bugs/Suggestions
    contact@waqasjamal.com
    ****************************************
    ------------------------------------------In DETAIL--------------------------------		
    '''
    class Custom_WP_XMLRPC:
    	def post_article(self,wpUrl,wpUserName,wpPassword,articleTitle, articleCategories, articleContent, articleTags,PhotoUrl):
    		self.path=os.getcwd()+"\\00000001.jpg"
    		self.articlePhotoUrl=PhotoUrl
    		self.wpUrl=wpUrl
    		self.wpUserName=wpUserName
    		self.wpPassword=wpPassword
    		#Download File
    		f = open(self.path,'wb')
    		f.write(urllib.urlopen(self.articlePhotoUrl).read())
    		f.close()
    		#Upload to WordPress
    		client = Client(self.wpUrl,self.wpUserName,self.wpPassword)
    		filename = self.path
    		# prepare metadata
    		data = {'name': 'picture.jpg','type': 'image/jpg',}
    		
    		# read the binary file and let the XMLRPC library encode it into base64
    		with open(filename, 'rb') as img:
    			data['bits'] = xmlrpc_client.Binary(img.read())
    		response = client.call(media.UploadFile(data))
    		attachment_id = response['id']
    		#Post
    		post = WordPressPost()
    		post.title = articleTitle
    		post.content = articleContent
    		post.terms_names = { 'post_tag': articleTags,'category': articleCategories}
    		post.post_status = 'publish'
    		post.thumbnail = attachment_id
    		post.id = client.call(posts.NewPost(post))
    		print 'Post Successfully posted. Its Id is: ',post.id
    
    
    
    
    #########################################
    # POST & Wp Credentials Detail #
    #########################################
    
    #Url of Image on the internet
    ariclePhotoUrl='http://i1.tribune.com.pk/wp-content/uploads/2013/07/584065-twitter-1375197036-960-640x480.jpg' 
    # Dont forget the /xmlrpc.php cause thats your posting adress for XML Server
    wpUrl='http://YourWebSite.com/xmlrpc.php' 
    #WordPress Username
    wpUserName='WordPressUsername'
    #WordPress Password
    wpPassword='YourWordPressPassword'
    #Post Title
    articleTitle='Testing Python Script version 3'
    #Post Body/Description
    articleContent='Final .... Testing Fully Automated'
    #list of tags
    articleTags=['code','python'] 
    #list of Categories
    articleCategories=['language','art'] 
    
    #########################################
    # Creating Class object & calling the xml rpc custom post Function
    #########################################
    xmlrpc_object	=	Custom_WP_XMLRPC()
    #On Post submission this function will print the post id
    xmlrpc_object.post_article(wpUrl,wpUserName,wpPassword,articleTitle, articleCategories, articleContent, articleTags,ariclePhotoUrl)

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
