##DataHub Overview
From: Al Wirtes
To: Dave, Angela
Date: Wed, Mar 18, 2015 at 10:38 AM
Subject: DataHub Overview

Hi Dave & Angela,

Linda has asked me to provide you a general overview of our DataHub system.

DataHub has two main features:

1. RSS Atom feed of CRM change information.
2. Full dealer demographic information available through a RESTful interface.

DataHub is designed to be as flexible as possible to serve many use cases.  Currently both iCM and our  Salesforce.com systems consume DataHub information. 

We chose the Atom protocol in order to leverage standards-based tools for creating and consuming these feeds.  This  allowed us to build the system quickly, since we didn't have to reinvent any wheels.  I recommend that you choose a standards-based tool for consuming the Atom feeds for these same reasons. 

We make extensive use of paging and HTTP response codes supported by the protocol. (A merged entity that no longer exists returns a 301 or "Moved Permanently," redirecting you to the target of the merge, etc.)

Typically, DataHub is used by:

1. Monitoring of Company and Individual Atom feeds for changes
2. Following links provided in the change feed for full demographic and relational information

Here is a sample Atom feed of changes:
````
<?xml version="1.0" encoding="UTF-8"?>
<feed xmlns="http://www.w3.org/2005/Atom" xmlns:dh="urn:datahub.hunterdouglas.com">
  <id>tag:datahub.hunterdouglas.com,2012:Companies:feed</id>
  <title type="text">Companies</title>
  <generator version="1.0.0-BUILD-SNAPSHOT">datahub-abdera</generator>
  <updated>2015-03-18T14:46:03.580Z</updated>
  <entry>
    <id>tag:datahub.hunterdouglas.com,2012:Companies:entry:91696</id>
    <title type="text">The Drapes of Wrath, Inc. (HDID: 1656826)</title>
    <updated>2015-03-18T14:46:03.580Z</updated>
    <category scheme="urn:datahub.hunterdouglas.com:ChangeType" term="U"/>
    <link href="/datahub/companies/1137296" rel="alternate"/>
  </entry>

[...]

  <link href="/datahub/companies" rel="self"/>
  <link href="/datahub/companies?since-index=300718" rel="next"/>
  <link href="/datahub/companies?since-index=0" rel="first"/>
  <dh:end-index>300718</dh:end-index>
</feed>
````
In the first entry you can see that there has been a change to The Drapes of Wrath, Inc (HDID: 1656826). The link element provides a link to full information about the changed company, ```/datahub/companies/1656826```.  Following this link provides full information about the company:
````
<?xml version="1.0" encoding="UTF-8"?>
<entry xmlns="http://www.w3.org/2005/Atom">
  <id>tag:datahub.hunterdouglas.com,2012:Companies:entry:92192</id>
  <title type="text">The Drapes of Wrath, Inc. (HDID: 1656826)</title>
  <updated>2015-03-18T14:44:12.187Z</updated>
  <category scheme="urn:datahub.hunterdouglas.com:ChangeType" term="U"/>
  <content type="application/xml">
    <Company xmlns="urn:datahub.hunterdouglas.com:Company" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" HDID="1656826">
      <Name>The Drapes of Wrath, Inc.</Name>
      <Type>Dealer</Type>
      <SponsoringFabricator HDID="15" href="/datahub/companies/15">
        <Name>HD Midwest Sales Region</Name>
        <Account>12345678</Account>
        <SalesRep HDID="1442742" href="/datahub/individuals/1442742">Salesman, Joe</SalesRep>
      </SponsoringFabricator>
      <Contacts>
        <Contact HDID="1656827" rel="employee" href="/datahub/individuals/1656827">Dealer, Gina</Contact>
        <Contact HDID="1656827" rel="primary-contact" href="/datahub/individuals/1656827">Dealer, Gina</Contact>
      </Contacts>
      <Addresses>
[...]
````
Note that relationship information is provided in the ````<SponsoringFabricator>```` and ````<Contacts>```` sections. The same individual can have multiple relationships in the ````<Contacts>```` section. This is how multiple roles are represented.

At this point you could continue to follow links in the contacts for individual data. For example, ````/datahub/individuals/1656827```` would provide you with similar information about Gina Dealer.  You could also monitor the individual Atom feed to listen for changes to individuals.

That's a high-level overview of how DataHub works. I have included sample files of the feeds mentioned here.

Let me know when you'd like to get together for a quick call to go over the tool, our experiences using it, etc. We can take a deeper dive into the tool at that time.

Thanks,
Al
