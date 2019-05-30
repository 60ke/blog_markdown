---
title: pymysql
date: 2017-09-15 10:46:51
categories: default
tags: []
urlname: 68
---
    import os
    import json
    import codecs
    import pymysql
    import re
    
    jsondir = os.getcwd() + "/all"
    
    
    
    # print(os.walk(jsondir))
    jsonnames = []
    for dirs in os.walk(jsondir):
    	jsonnames = dirs[2]
    conn = pymysql.connect(
    user = 'root',
    password = '529966',
    host = 'localhost',
    port = 3306,
    database = 'ceve',
    use_unicode=True,
    charset = 'utf8'
    )
    cursor = conn.cursor()
    for jsonname in jsonnames:
    	f = codecs.open(jsondir+'/'+jsonname,'r',encoding='utf-8')
    	data = json.load(f,encoding="utf-8")
    	# print(data)
    	# import pdb
    	# pdb.set_trace()
    
    
    	ceve_id = data['vid']
    	name = data['vid']
    	try:
    		pub_date = data['published-datetime']
    		pub_date = re.findall("(.+?)T",pub_date)[0]
    	except:
    		pub_date = "null"
    	try:
    		description =data['description']
    		description = cursor.connection.escape(description)
    	except:
    		description = "null"
    	# print(type(data['vuln_cvss']))
    	try:
    		cvss_score = data['vuln_cvss']['cvss_score']
    		cvss_score = cursor.connection.escape(cvss_score)
    	except:
    		cvss_score = "null"
    	
    	try:
    		cvss_confidentiality_impact = data['vuln_cvss']["cvss_confidentiality-impact"]
    		cvss_confidentiality_impact = cursor.connection.escape(cvss_confidentiality_impact)
    	except:
    		cvss_confidentiality_impact = "null"
    	
    	try:
    		cvss_integrity_impact = data['vuln_cvss']["cvss_integrity-impact"]
    		cvss_integrity_impact = cursor.connection.escape(cvss_integrity_impact)
    	except:
    		cvss_integrity_impact = "null"
    	
    	try:
    		cvss_availability_impact = data['vuln_cvss']["cvss_availability-impact"]
    		cvss_availability_impact = cursor.connection.escape(cvss_availability_impact)
    	except:
    		cvss_availability_impact = "null"
    	
    	try:
    		cvss_access_complexity = data['vuln_cvss']["cvss_access-complexity"]
    		cvss_access_complexity = cursor.connection.escape(cvss_access_complexity)
    	except:
    		cvss_access_complexity = "null"
    	
    	try:
    		cvss_access_vector = data['vuln_cvss']["cvss_access-vector"]
    		cvss_access_vector = cursor.connection.escape(cvss_access_vector)
    	except:
    		cvss_access_vector = "null"
    	
    	try:
    		cvss_authentication = data['vuln_cvss']['cvss_authentication']
    		cvss_authentication = cursor.connection.escape(cvss_authentication)
    	except:
    		cvss_authentication ="null"
    	
    	# import pdb
    	# pdb.set_trace()
    	# except:
    	# 	print(jsonname)	
    	# ,`published-datetime`,`last-modified-datetime`,`vuln_cvss`,`vuln_cwe`,`vuln_references`,`summary`,`vulnerable-software-list`
    	# cursor.execute("INSERT INTO vuler_ceve(`ceve_id`,`name`,`pub_date`,`description`,`cvss_score`,`cvss_confidentiality_impact`,`cvss_integrity_impact`,`cvss_availability_impact`,`cvss_access_complexity`,`cvss_access_vector`,`cvss_authentication`) VALUES(ceve_id,name,pub_date,description,cvss_score,cvss_confidentiality_impact,cvss_integrity_impact,cvss_availability_impact,cvss_access_complexity,cvss_access_vector,cvss_authentication)")
    	try:
    		cursor.execute("INSERT INTO vuler_ceve(`ceve_id`,`name`,`pub_date`,`description`,`cvss_score`,`cvss_confidentiality_impact`,`cvss_integrity_impact`,`cvss_availability_impact`,`cvss_access_complexity`,`cvss_access_vector`,`cvss_authentication`) VALUES('%s','%s','%s',%s,%s,%s,%s,%s,%s,%s,%s)"%(ceve_id,name,pub_date,description,cvss_score,cvss_confidentiality_impact,cvss_integrity_impact,cvss_availability_impact,cvss_access_complexity,cvss_access_vector,cvss_authentication))
    		conn.commit()
    	except Exception as e:
    		print(jsonname)
    		print(e)
    
    	# import pdb
    	# pdb.set_trace()
    	f.close()
    cursor.close()