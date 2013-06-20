---
comments: true
published: false
date: 2012-03-10 23:52:00
layout: post
slug: a-simple-python-prog-with-douban-api
title: '[分享][代码]一个简单的python小程序————使用douban API通过ISBN查询书籍信息'
wordpress_id: 646
categories:
- dev
- sexy python
- Techs
tags:
- douban
- xml
---

## 前言

 

刚学python时做的一个小程序，虽然小，但是也用到了不少内容。具体有以下几个方面： 

  * 命令行的解析 
  * 文件的读写 
  * XML解析 
  * http连接 
  * 多线程 
 

短短不到200行的程序就可以做到这些，可以算是python的推广广告吧，哈哈 



    
    
    # -*- coding=utf-8 -*-
    '''
    Created on 2011-12-4
    
    @author: liuyix
    '''
    '''
    输入文件格式定义:每行一个isbn，可能有重复，错误的
    输出格式：
    书名--评分--评分人数--作者--出版社等信息--豆瓣链接--书简介--rawxml
    
    douban xml:
    tags
    <id>#{http://www.w3.org/2005/Atom}id
    <title>#{http://www.w3.org/2005/Atom}title
    <category>#{http://www.w3.org/2005/Atom}category#category有多个attrib
    <author>#{http://www.w3.org/2005/Atom}author#注意author还有subelement
    <link>#{http://www.w3.org/2005/Atom}link#存在多个link，每个link中的attrib不同，且attrib中的key都是一个
    <summary>#{http://www.w3.org/2005/Atom}summary
    <attribute>#{http://www.douban.com/xmlns/}attribute#存在多个attribute，每个attribute的attrib[name]不同，且都是一个
    <tag>#{http://www.douban.com/xmlns/}tag#存在多个tag，每个tag都有一个dictionary，其中有2个key:name,count
    <rating>#{http://schemas.google.com/g/2005}rating#该元素中有一个含有多个key的字典
    
    '''
    
    import sys,os,httplib,threading,time
    import argparse
    import xml.etree.ElementTree as ET
    
    myapikey=01234567890 #此处换成你的APIKEY
    
    def writeFile(file,lock,str):
        lock.acquire()
        try:
            file.write(str)
        finally:
            lock.release()
    
    def getISBNList(isbnfile):
        '''
        从string名字中读入ISBN，返回list数组
        version1:不保证有重复数据
        '''
        isbnlist = []
        while True:
            tmp = isbnfile.readline().strip()
            if len(tmp) == 0:
                break
            isbnlist.append(tmp)
            pass
        isbnfile.close()
        return isbnlist
        pass
    
    def httpconn(isbn):
        conn = httplib.HTTPSConnection('api.douban.com')
        conn.request('GET', '/book/subject/isbn/%s?apikey='+myapikey % isbn)
        response = conn.getresponse()
        print 'status:%s#reason:%s'  % (response.status,response.reason)
        if str(response.status) != '200':
            print '未查到ISBN为%s' % isbn
            return None
        data = response.read()
        print data #debug输出
        return data
        pass
    
    def parseDoubanXml(wfile,wlock,element):
        '''
        从输入的xml.etree.ElementTree.Element对象开始解析XML，解析格式见上
        '''
        
        if element == None:
            return
        root = element
        
        bookitem = ''
        space_sep = '\t'
    #    for k in list(root):
    #        print k
        #书名
        booktitle = root.findtext('{http://www.w3.org/2005/Atom}title').encode('utf-8')
        #print '书名:%s' % (booktitle)
        bookitem += booktitle + space_sep
        
        #作者
        #print '作者: ',
    #    for i in list(root.find('{http://www.w3.org/2005/Atom}author')):
    #        #print '%s' % [k.text for k in i.findall('{http://www.w3.org/2005/Atom}name')]
    #        print      
        #authors = [k.text for k in root.find('{http://www.w3.org/2005/Atom}author').findall('{http://www.w3.org/2005/Atom}name')]
        #print authors
        bookitem += '['
        author_element = root.find('{http://www.w3.org/2005/Atom}author')
        if author_element != None:
            for i in author_element.findall('{http://www.w3.org/2005/Atom}name'):
                #print i.text,
                bookitem += i.text.encode('utf-8') + ' '
            #print ''
        else:
            bookitem += '未查到'
        bookitem += ']' + space_sep
        
        #评分及人数
        ratingElem = root.find('{http://schemas.google.com/g/2005}rating')
        #print '评分：%s 评价人数: %s' % (ratingElem.attrib['average'],ratingElem.attrib['numRaters'])
        rating = ratingElem.attrib['average']
        numRater = ratingElem.attrib['numRaters']
        ratingInfo = rating + '(' + numRater + ')'
        bookitem += ratingInfo + space_sep
        
        #出版社等一系列信息
    #    bookinfos = {}
    #    for k in root.findall('{http://www.douban.com/xmlns/}attribute'):
    #        bookinfos[k.attrib['name']] = str(k.text.encode('utf-8'))
    #        #print '%s:%s' % (k.attrib['name'],k.text)
    #        pass
    #    for k in bookinfos:
    #        print '%s:%s' % (k,bookinfos[k])
        #豆瓣链接
        links = root.findall('{http://www.w3.org/2005/Atom}link')
        for k in links:
            if k.attrib['rel'] == 'alternate':
                #print '豆瓣链接:%s' % (k.attrib['href'])
                doubanLink = k.attrib['href']
                bookitem += doubanLink + space_sep
        #书简介
    #    print '简介:'
    #    print '%s' % (root.findtext('{http://www.w3.org/2005/Atom}summary'))
        print bookitem
        
        wlock.acquire()
        wfile.write(bookitem + '\n')
        wfile.flush()
        wlock.release()
        
    
    def loadXmlfile(filename):
        #得到xml的根节点
        
        #parser = ET.XMLParser(encoding='utf-8')
        #tree = ET.parse(filename,parser=parser)
        tree = ET.parse(filename)    
        parseDoubanXml(tree.getroot())
    
    def loadXmlString(wfile,wlock,xmlstr):
        element = ET.fromstring(xmlstr)
        parseDoubanXml(wfile,wlock,element)
            
    
    def processQuery(wfile,wlock,isbn):
        data = httpconn(isbn)
        if data != None:
            loadXmlString(wfile,wlock,data)
        
    
    if __name__ == '__main__':
        #loadXmlfile('/home/cnliuyix/test.xml')
        #data = httpconn('9787508624136')
        #loadXmlString(data)
    
        parser = argparse.ArgumentParser(description='批量处理ISBN脚本')
        #parser.add_argument()
        parser.add_argument('-f','--file',help='批量的ISBN文本',type=file,required=True,metavar='isbn.txt')
        parser.add_argument('-o','--output',help='输出的文件名',type=argparse.FileType('w'),required=True,metavar='bookinfo.txt')
        
        opts = vars(parser.parse_args())
        
        print opts
        #sys.exit(0)
        
        
        #isbnFile = file('/home/cnliuyix/codes/python/ISBN.txt')
        isbnFile = opts['file']
        #storefile = file('/home/cnliuyix/books.txt','w')
        storeFile = opts['output']
    #    if storeFile == None or not isbnFile.exists():
    #        print '创建文件失败'
    #        sys.exit(-1)
        wlock = threading.Lock()    
        sleeptime  = 2
        isbnList = getISBNList(isbnFile)
        print 'list size:%d' % len(isbnList)
        cnt = 0
        subThreads = []
        
        for i in isbnList:
            cnt += 1
    #        if cnt % 10 == 0:
    #            print '休息%ds' % sleeptime
    #            #time.sleep(sleeptime)
            t = threading.Thread(target=processQuery,args=(storeFile,wlock,i))
            subThreads.append(t)
            t.setDaemon(True)
            t.start()
        for i in subThreads:
            i.join()
        
        
    
