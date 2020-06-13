---
title: crawl_modify2
date: 2020-05-07
---
Example Python program crawl_modify2.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* from docx import Document
* from docx.shared import Pt
* from docx.shared import Inches
* from docx.oxml.ns import qn
* import re
* import json

## Methods

* def convertChineseDigitsToArabic (chinese_digits):

## Code

Python example

    # !/usr/bin/env python
    # -*- coding: utf-8 -*-
    
    from docx import Document
    from docx.shared import Pt
    from docx.shared import Inches
    from docx.oxml.ns import qn
    import re
    import json
    
    chs_arabic_map = {u'零':0, u'一':1, u'二':2, u'三':3, u'四':4,
            u'五':5, u'六':6, u'七':7, u'八':8, u'九':9,
            u'十':10, u'百':100, u'千':10 ** 3, u'万':10 ** 4,
            u'〇':0, u'壹':1, u'贰':2, u'叁':3, u'肆':4,
            u'伍':5, u'陆':6, u'柒':7, u'捌':8, u'玖':9,
            u'拾':10, u'佰':100, u'仟':10 ** 3, u'萬':10 ** 4,
            u'亿':10 ** 8, u'億':10 ** 8, u'幺': 1,
            u'０':0, u'１':1, u'２':2, u'３':3, u'４':4,
            u'５':5, u'６':6, u'７':7, u'８':8, u'９':9}
    
    #Convert Chinese Digit to Arabic.
    # Credit by Liam Huang http://liam0205.me/2016/07/26/translate-Chinese-digits-to-Arabic-number/
    def convertChineseDigitsToArabic (chinese_digits):
        if isinstance (chinese_digits, str):
            chinese_digits = chinese_digits
    
        result = 0
        tmp = 0
        hnd_mln = 0
        for count in range(len(chinese_digits)):
            curr_char = chinese_digits[count]
            curr_digit = chs_arabic_map.get(curr_char, None)
            # meet 「亿」 or 「億」
            if curr_digit == 10 ** 8:
                result = result + tmp
                result = result * curr_digit
                # get result before 「亿」 and store it into hnd_mln
                # reset `result`
                hnd_mln = hnd_mln * 10 ** 8 + result
                result = 0
                tmp = 0
            # meet 「万」 or 「萬」
            elif curr_digit == 10 ** 4:
                result = result + tmp
                result = result * curr_digit
                tmp = 0
            # meet 「十」, 「百」, 「千」 or their traditional version
            elif curr_digit >= 10:
                tmp = 1 if tmp == 0 else tmp
                result = result + curr_digit * tmp
                tmp = 0
            # meet single digit
            elif curr_digit is not None:
                tmp = tmp * 10 + curr_digit
            else:
                return result
        result = result + tmp
        result = result + hnd_mln
        return result
    
    input_file = '2016-12-WT-Outlines-S1.docx'
    #Read input documents
    document1 = Document(input_file)
    document1.save('demo.docx')
    document2 = Document('demo.docx')
    
    all_paragraphs = document2.paragraphs
    
    for p in document2.paragraphs:
        inline = p.runs
        # Loop added to work with runs (strings with same style)
        x = ""
        for i in range(len(inline)):
            x += inline[i].text
            inline[i].clear()
            inline[0].text = x
    
    document2.save('demo.docx')
    
    # Copy demo.docx to demo1.docx and change the strings to different para.
    document3 = Document('demo.docx')
    document4 = Document()
    
    for p in document3.paragraphs:
        # if 1 == 0:
            x = p.text
            ss = re.match(r'(^(壹|贰|叁|肆|伍|陆|柒|捌|玖|拾|一|二|三|四|五|六|七|八|九|十|[0-9]|[a-z]).*)(——)'
                          r'((参|创|出|利|民|申|书|士|得|撒上|撒下|王上|王下|代上|代下|拉|尼|斯|伯|诗|箴|传|歌|赛|耶|哀|结|但|何|珥|摩|俄|拿|弥|鸿|哈|番|该|亚|玛|太|可|路|'
                          r'徒|罗|林前|林后|加|弗|腓|西|帖前|帖后|提前|提后|多|门|来|雅|彼前|彼后|约壹|约贰|约参|犹|启|约|一|二|三|四|五|六|七|八|九|十|[0-9]).*)([：|。|:])', x)
            tt = re.match(r'(^(读经：|读经:)(.*))', x)
            if ss:
            #if not ss is None:
                #found all verse reference
                document4.add_paragraph(x)
                sss = ss.group(4)
                # print (sss) # used for debugging
                sss_split = sss.split('，')
                book = ""
                for j in sss_split:
                    j = re.sub(r'^参(.*)', r'\1', j)
                    book_check = re.match(r'^(创|出|利|民|申|书|士|得|撒上|撒下|王上|王下|代上|代下|拉|尼|斯|伯|诗|箴|传|歌|赛|耶|哀|结|但|何|珥|摩|俄|拿|弥|鸿|哈|番|该|亚|玛|太|可|路|'
                                          r'徒|罗|林前|林后|加|弗|腓|西|帖前|帖后|提前|提后|多|门|来|雅|彼前|彼后|约壹|约贰|约参|犹|启|约)'
                                          r'(一|二|三|四|五|六|七|八|九|十).*(\d+)',j)
                    no_book_check = re.match(r'^(一|二|三|四|五|六|七|八|九|十).*(\d+)',j)
                    if book_check:
                        book = book_check.group(1)
    
                    if no_book_check:
                        # print('book name is: ' + book) #for debugging
                        j = book + j
                        # print ('j add book name is: ' + j) #for debugging
                    document4.add_paragraph(j)
            elif tt:
                document4.add_paragraph(x)
                ttt = tt.group(3)
                ttt_split = ttt.split('，')
                for j in ttt_split:
                    j = re.sub(r'^参(.*)', r'\1', j)
                    book_check = re.match(r'^(创|出|利|民|申|书|士|得|撒上|撒下|王上|王下|代上|代下|拉|尼|斯|伯|诗|箴|传|歌|赛|耶|哀|结|但|何|珥|摩|俄|拿|弥|鸿|哈|番|该|亚|玛|太|可|路|'
                                          r'徒|罗|林前|林后|加|弗|腓|西|帖前|帖后|提前|提后|多|门|来|雅|彼前|彼后|约壹|约贰|约参|犹|启|约)'
                                          r'(一|二|三|四|五|六|七|八|九|十).*(\d+)',j)
                    no_book_check = re.match(r'^(一|二|三|四|五|六|七|八|九|十).*(\d+)',j)
                    if book_check:
                        book = book_check.group(1)
    
                    if no_book_check:
                        j = book + j
                    document4.add_paragraph(j)
            else:
                document4.add_paragraph(x)
    
    document3.save('demo.docx')
    document4.save('demo1.docx')
    
    document5 = Document('demo1.docx')
    document6 = Document()
    
    for p in document5.paragraphs:
        x = p.text
        #check if 、 exist, if yes, split the line into different sections, check the first section and extract
        # the book and chapter and store to a variables. write into a docx, add the variable
        #into following paragraphs and write them into the new docx
        ss = re.match(r'^(创|出|利|民|申|书|士|得|撒上|撒下|王上|王下|代上|代下|拉|尼|斯|伯|诗|箴|传|歌|赛|耶|哀|结|但|何|珥|摩|俄|拿|弥|鸿|哈|番|该|亚|玛|太|可|路|'
                      r'徒|罗|林前|林后|加|弗|腓|西|帖前|帖后|提前|提后|多|门|来|雅|彼前|彼后|约壹|约贰|约参|犹|启|约)(.*)',
                      x)
        if ss:
            sss = ss.group()
            if "、" in sss:
                sss_split = sss.split('、')
                book_chapter = ""
                for j in sss_split:
                    book_check = re.match(r'(^\D+)(\d+)', j)
                    verse_check = re.match(r'^\d+', j)
                    if book_check:
                        book_chapter = book_check.group(1)
                    elif verse_check:
                        j = book_chapter + j
                    document6.add_paragraph(j)
            else:
                document6.add_paragraph(sss)
        else:
            document6.add_paragraph(x)
    document5.save('demo1.docx')
    document6.save('demo2.docx')
    
    # open a new docx
    # check if ~ exist, if yes, record the number before and after ~ sign. list all the value into new docx
    document7 = Document('demo2.docx')
    document8 = Document()
    for p in document7.paragraphs:
        x = p.text
        ss = re.match(r'^(创|出|利|民|申|书|士|得|撒上|撒下|王上|王下|代上|代下|拉|尼|斯|伯|诗|箴|传|歌|赛|耶|哀|结|但|何|珥|摩|俄|拿|弥|鸿|哈|番|该|亚|玛|太|可|路|'
                      r'徒|罗|林前|林后|加|弗|腓|西|帖前|帖后|提前|提后|多|门|来|雅|彼前|彼后|约壹|约贰|约参|犹|启|约)(.*)',
                      x)
        if ss:
            sss = ss.group()
            if "～" in sss:
                book_chapter = ""
                first_verse = ""
                last_verse = ""
                range_check = re.match(r'(\D+)(\d+)～(\d+)', sss)
                if range_check:
                    book_chapter = range_check.group(1)
                    first_verse = range_check.group(2)
                    last_verse = range_check.group(3)
                    sss = book_chapter + first_verse
                    document8.add_paragraph(sss)
                    for num in range (int(first_verse)+1, int(last_verse)+1):
                        content = book_chapter + str(num)
                        document8.add_paragraph(content)
            else:
                document8.add_paragraph(x)
        else:
            document8.add_paragraph(x)
    document8.save('demo3.docx')
    
        # open a new docx
        # replace all the verse reference with actural verses.
    document9 = Document('demo3.docx')
    document10 = Document()
    data_file = open('bible-zh.js', 'r', encoding='utf-8')
    data = json.load(data_file)
    for p in document9.paragraphs:
        x = p.text
        ss = re.match(r'^(创|出|利|民|申|书|士|得|撒上|撒下|王上|王下|代上|代下|拉|尼|斯|伯|诗|箴|传|歌|赛|耶|哀|结|但|何|珥|摩|俄|拿|弥|鸿|哈|番|该|亚|玛|太|可|路|'
                      r'徒|罗|林前|林后|加|弗|腓|西|帖前|帖后|提前|提后|多|门|来|雅|彼前|彼后|约壹|约贰|约参|犹|启|约)(\D+)(\d+)(.*)',
                      x)
        if ss:
            # check if contains 上、下
            if ss.group(4) == "上" or ss.group(4) == "下":
                #print('ss.group(2) is: ' + ss.group(2))
                id = ss.group(1) + " " + str(convertChineseDigitsToArabic(ss.group(2))) + ":" + ss.group(3)+ss.group(4)
                if id in data["verse"]:
                    paragraph = document10.add_paragraph (id + "\t" + data["verse"][id])
                    paragraph.paragraph_format.left_indent = Inches(0.5)
                else:
                    id = ss.group(1) + " " + str(convertChineseDigitsToArabic(ss.group(2))) + ":" + ss.group(3)
                    paragraph = document10.add_paragraph (id + "\t" + data["verse"][id])
                    paragraph.paragraph_format.left_indent = Inches(0.5)
            else:
                id = ss.group(1) + " " + str(convertChineseDigitsToArabic(ss.group(2))) + ":" + ss.group(3)
                if id in data["verse"]:
                    paragraph = document10.add_paragraph (id + "\t" + data["verse"][id])
                    paragraph.paragraph_format.left_indent = Inches(0.5)
                else:
                    paragraph = document10.add_paragraph (id + "\t" + data["verse"][id + "上"] + data["verse"][id + "下"])
                    paragraph.paragraph_format.left_indent = Inches(0.5)
        else:
            paragraph = document10.add_paragraph (x)
    document9.save('demo3.docx')
    document10.save('demo4.docx')

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
