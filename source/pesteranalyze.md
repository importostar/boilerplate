---
title: pesteranalyze
date: 2020-05-07
---
Example Python program pesteranalyze.py

## Modules

* import sys
* import re
* from os import path
* from wordcloud import WordCloud
*   import matplotlib.pyplot as plt

## Methods

* def wordcloud():
*   def duped_messages(messages):

## Code

Python example

    import sys
    import re
    from os import path
    from wordcloud import WordCloud
    
    def wordcloud():
      lines = sys.stdin.readlines()
      line = ''.join(lines).replace('&nbsp;', ' ').replace('\n', ' ').replace('<br/>', '\n')
      line = re.sub('<.*?>', '', line)
      lines = [ line.split('         ') for line in line.split('\n') ]
      messages = [ message for datestr, message in lines if len(message) > 0 ]
    
      def duped_messages(messages):
        carets = 0
        for message in messages:
          if message[0] is '^':
            carets += 1
            continue
          yield message
          while carets > 0:
            yield message
            carets -= 1
      duped_messages_generator = duped_messages(messages)
    
      text = ' '.join(duped_messages_generator)
    
      # Generate a word cloud image
      wordcloud = WordCloud().generate(text)
    
      # Display the generated image:
      # the matplotlib way:
      import matplotlib.pyplot as plt
      plt.imshow(wordcloud)
      plt.axis('off')
    
      # lower max_font_size
      wordcloud = WordCloud(max_font_size=40).generate(text)
      plt.figure()
      plt.imshow(wordcloud)
      plt.axis('off')
      plt.show()
    
      # The pil way (if you don't have matplotlib)
      #image = wordcloud.to_image()
      #image.show()
    
    if __name__ == '__main__':
      wordcloud()
    
    # Pipfile
    #[[source]]
    #
    #url = "https://pypi.python.org/simple"
    #verify_ssl = true
    #
    #[packages]
    #
    #wordcloud = "*"
    #matplotlib = "*"

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
