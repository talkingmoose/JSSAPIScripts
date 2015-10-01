#JSSAPIScripts

JSS Utility scripts featuring the JAMF API by Jeffrey Compton

Table of Contents
=================

  * [jssMigrationUtility\.bash](#jssmigrationutilitybash)
  * [getSelfServicePolicyIcons\.bash](#getselfservicepolicyiconsbash)
  
jssMigrationUtility.bash
==================

Version 1.1

The JSS Migration Utility uses the JAMF API to download resources from a source JSS and 
upload those resources to a destination JSS.  The utiltiy does NOT migrate computers.  

The primary goal and use-case for this utiltiy is to provide a mechanism where a JAMF 
admin can set up a barebones, clean JSS and import management resources (categories, 
scripts, extension attributes, computer groups, etc.) from another JSS instance.  This is 
perhaps most helpful when circumstances (e.g. a crufty database) prevent JSS migration via
the usual process - a database restore.

Basic Process:

1. XML files are downloaded from source JSS to local system 
2. XML files are parsed, depending on the current resource 
3. XML files are then uploaded to destination JSS

WARNINGS:

For this to work correctly, some data must be stripped from the downloaded XML before
uploading to new server.  This occurs during the parsing process.  Before each group of 
resource files are parsed, a warning will display explaining what data, if any, will be 
stripped.  For example, before the ldapservers resource files are parsed, you will see
this message -- 

Passwords for authenticating to LDAP will NOT be included!
You must enter passwords for LDAP in web app

Local File System:

By default, XML files are stored to ~/Desktop/JSS_Migration  Before work begins on each
resource, the utility looks for the presence of any previously downloaded resources and
archives to ~/Desktop/JSS_Migration/archives if necessary


getSelfServicePolicyIcons.bash
==================

Casper Admins aren't perfect.  Sometimes we forget to save all the icons we use for 
Self Service policies.  After all - they are in the JSS.  But if you have to stand up
a separate JSS or a new one from scratch - you may want to get those.

This script finds all Self Service policies in your JSS and downloads the icons for each.

But what if we have uploaded the same icon more than once ? Now we have multiple versions
of the same icon, each slightly different - different resolution, new style, etc.  

No worries - this script will ensure that all flavors of the same icon are downloaded.  
The file name will be appended with a "-" and the policy ID, ensuring all versions of 
same icon are downloaded.

But wait!  There's more!  At the end of the download process, you will be asked if you
want to rename each file with a resolution indicator.  That way you can more easily find
the right version of the icon you are looking for.