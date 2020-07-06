# SAP-Hash-Harvester
This ABAP report is a post-exploitation means of retrieving password hashes in order to offline brute force them

The exchange of Business Critical data between systems via ALE
The SAP systems which run your business processes store data in local databases. There are however many scenarios where data is exchanged between SAP systems. One typical method of exchanging data between systems is Application Link enabling (ALE). The business data flowing from one to another system is packaged in so called Intermediate Documents (Idocs). These Idocs often contain business critical objects like Vendor records, Sales orders, Credit card information or Product information. This is important to realize, especially when it comes to securing your SAP platform.
So, I have Idocs being sent all over the place, what’s the risk?
Idocs are stored in the database in for example table EDIDC. When people have access to these tables they can extract the sensitive data directly out of those tables. This makes it easy to harvest large amounts of sensitive security-related data.
A simple PoC to demonstrate the risk; The HashHarvester (HaHa)
In order to demonstrate the associated risk, I created a simple PoC. The challenge was to see how hard it would be to extract SAP User Password Hashes from the EDIDC table. When customers use Central User Administration, the replication of users is done via Idocs that might contain password hashes. 

As I would have guessed, it was not hard at all to harvest the password hashes. The only thing needed to harvest the data you are looking for is to know the specific message-type you are looking for, in this case ‘USERCLONE’. Every Masterdata object in SAP has its own message-type that identifies the unique type of data being transferred. Once you know this message-type you can use for example an ABAP program to harvest the data you want. For a quick written example of such a program see the ABAP code herebelow.
