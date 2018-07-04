![SAP HANA Academy](https://yt3.ggpht.com/-BHsLGUIJDb0/AAAAAAAAAAI/AAAAAAAAAVo/6_d1oarRr8g/s100-mo-c-c0xffffffff-rj-k-no/photo.jpg)

## SQL Trace ##
In the first video, we discuss the SQL trace facility for SAP HANA, its use cases, and how to enable it using SQL, SAP HANA studio, and the SAP HANA database explorer. 

You can enable SQL Trace using the Trace Configuration tab of the SAP HANA studio, or using the Trace Configuration context menu in the SAP HANA database explorer. Both interfaces will generate the corresponding SQL statements. 

![Trace Configuration](https://github.com/saphanaacademy/sqltrace/blob/master/img/config.png)

For scripting purposes, you can also use the SQL statements directly.  

To enable SQL trace for a tenant database, set the parameter for the indexserver process. 
```
ALTER SYSTEM ALTER CONFIGURATION ('indexserver.ini','DATABASE') SET
  ('sqltrace','trace')='on'
  WITH RECONFIGURE;
```  
To enable SQL trace for a tenant database, set the parameter for the nameserver process. 
```
ALTER SYSTEM ALTER CONFIGURATION ('nameserver.ini','SYSTEM') SET
  ('sqltrace','trace')='on'
  WITH RECONFIGURE;
``` 
To disable SQL Trace, set trace=off or UNSET sqltrace. Unsetting the parameter, will return the value to its default, which in case of SQL trace is off. 
```  
ALTER SYSTEM ALTER CONFIGURATION ('indexserver.ini','DATABASE') SET
  ('sqltrace','trace')='off'
  WITH RECONFIGURE;
  
ALTER SYSTEM ALTER CONFIGURATION ('indexserver.ini','DATABASE') UNSET
  ('sqltrace','trace')
  WITH RECONFIGURE;
```  
Below some more examples of the different configuration parameter settings availabe. 

![Trace Configuration](https://github.com/saphanaacademy/sqltrace/blob/master/img/param.png)
```
-- additional options
 ALTER SYSTEM ALTER CONFIGURATION ('indexserver.ini','DATABASE') SET
  ('aqltrace','trace')='on',
  ('aqltrace','level')='all_with_results',
  ('aqltrace','tracefile')='trace/apple.py',
  ('aqltrace','user')='system',
  ('aqltrace','statement_type')='dml,ddl',
  ('aqltrace','application')='hdbstudio'  
  WITH RECONFIGURE; 
```
### Tutorial Video ### 
[![SAP Trace](https://img.youtube.com/vi/ycRPnA-L07M/0.jpg)](https://www.youtube.com/watch?v=ycRPnA-L07M "SQL Trace")

### Documentation ### 
* [SQL Trace - SAP HANA Administration Guide](https://help.sap.com/viewer/6b94445c94ae495c83a19646e7c3fd56/latest/en-US/bedc9668bb5710149d56d29fe2632ba0.html)
* [2031647 - How to enable SQL Trace in SAP HANA Studio](https://launchpad.support.sap.com/#/notes/2031647)
* [2119087 - How-To: Configuring SAP HANA Traces](https://launchpad.support.sap.com/#/notes/2119087)

## SAP HANA SQL Trace Analyzer ##
In the next video, we provide an introduction to the SAP HANA SQL Trace Analyzer. Like most of the Python script files found in /usr/sap/<SID>/HDB##/exe/python_support, this was originally a non-documented tool for internal usage only (SAP product support). However, because of its usefulness in quickly gathering some information out of the massive amount of trace data, we now find it documented in SAP Note 2412519.  

To generate a trace report run the python command with the name of script and name of trace file. For other script options, see the usage information (run the script withouth trace file) or the mentioned SAP Note. 
 
```
python sqlTraceAnalyzer.py sqltrace_host_30003_000.py
``` 

### Tutorial Video ### 
[![SQL Trace Analyzer](https://img.youtube.com/vi/FvzN89vwcho/0.jpg)](https://www.youtube.com/watch?v=FvzN89vwcho "SQL Trace Analyzer")

### Documentation ### 
* [2412519 - FAQ: SAP HANA SQL Trace Analyzer](https://launchpad.support.sap.com/#/notes/2412519)


