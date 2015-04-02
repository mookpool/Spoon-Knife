Al Wirtes <al.wirtes@hunterdouglas.com>
Wed, Mar 18, 2015 at 10:38 AM
To: Dave, Angela
Subject: DataHub Overview

Hi Dave & Angela,

Linda has asked me to provide you a general overview of our DataHub system.

DataHub consists of an RSS Atom feed of change information for both companies and Individuals in our CRM system. In addition to the change information, DataHub delivers full CRM demographic information for companies, individuals and relationships via a RESTful interface.  It is designed to be as flexible as possible to serve many use cases.  Currently both iCM and our internal Salesforce.com systems consume DataHub information.

We chose the Atom protocol in order to leverage standards-based tools for both creating and consuming these feeds.  I would recommend that you pick a standards-based tool for consuming the Atom feeds. We make extensive use of paging and HTTP response codes supported by the protocol. (A merged HDID that no longer exists returns a 301 or "Moved Permanently," redirecting you to the target of the merge, etc.)

Typically, DataHub is used by:
	1.	Monitoring of Company and Individual Atom feeds for changes
	2.	Following links provided in the change feed for full demographic and relational information
Here is a sample Atom feed of changes:
````
<?xml version="1.0" encoding="UTF-8"?>
<feed xmlns="http://www.w3.org/2005/Atom" xmlns:dh="urn:datahub.hunterdouglas.com">
  <id>tag:datahub.hunterdouglas.com,2012:Companies:feed</id>
  <title type="text">Companies</title>
  <aut
  '''
