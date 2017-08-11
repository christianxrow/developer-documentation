# eZ Platform 1.4.2 Release Notes


**September 20th 2016**

eZ announces the availability of 1.4.2, a maintenance release available for all users of eZ Platform 1.4.0.

Follow the [eZ Platform Update Instructions](updating_ez_platform.md) to apply this update to your platforms.



## Package updates

Here are the ezsystems packages that have received an update as part of this release:

 

| package                      |  version   |
|------------------------------|------------|
| ezsystems/ezpublish-kernel   | v6.4.1-rc1 |
| ezsystems/platform-ui-bundle | v1.4.1-rc1 |
| ezsystems/ezplatform         | v1.4.1-rc1 |

 

## Updates and fixes in this release

|                                                                |                                                                                                                                                           |                                                                                                                 |              |              |
|----------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|--------------|--------------|
| Key                                                            | Summary                                                                                                                                                   | T                                                                                                               | Created      | Updated      |
| [EZP-25003](https://jira.ez.no/browse/EZP-25003?src=confmacro) | [Clear HTTP cache when trashing, recovering and deleting content/locations](https://jira.ez.no/browse/EZP-25003?src=confmacro)                            | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-25003?src=confmacro) | Oct 20, 2015 | Aug 10, 2016 |
| [EZP-25533](https://jira.ez.no/browse/EZP-25533?src=confmacro) | [Hardcoded anonymous\_hash in FosHttpCache mismatches what is generated by Platform](https://jira.ez.no/browse/EZP-25533?src=confmacro)                   | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-25533?src=confmacro) | Mar 03, 2016 | Oct 04, 2016 |
| [EZP-25913](https://jira.ez.no/browse/EZP-25913?src=confmacro) | [urlAliasGenerator::generate issues in console command / cli](https://jira.ez.no/browse/EZP-25913?src=confmacro)                                          | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-25913?src=confmacro) | Jun 20, 2016 | Sep 05, 2016 |
| [EZP-26042](https://jira.ez.no/browse/EZP-26042?src=confmacro) | [Some mandatory parameters are missing ("language") to generate a URL for route "\_ez\_content\_view"](https://jira.ez.no/browse/EZP-26042?src=confmacro) | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26042?src=confmacro) | Jul 07, 2016 | Aug 25, 2016 |
| [EZP-26081](https://jira.ez.no/browse/EZP-26081?src=confmacro) | [ae-toolbars not displayed on Microsoft Edge](https://jira.ez.no/browse/EZP-26081?src=confmacro)                                                          | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26081?src=confmacro) | Jul 15, 2016 | Aug 03, 2016 |
| [EZP-26086](https://jira.ez.no/browse/EZP-26086?src=confmacro) | [Unable to inject additional service or value into QueryType as a service](https://jira.ez.no/browse/EZP-26086?src=confmacro)                             | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26086?src=confmacro) | Jul 18, 2016 | Jul 20, 2016 |
| [EZP-26101](https://jira.ez.no/browse/EZP-26101?src=confmacro) | [Integer and Float Fields validation broken in Firefox](https://jira.ez.no/browse/EZP-26101?src=confmacro)                                                | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26101?src=confmacro) | Jul 19, 2016 | Aug 03, 2016 |
| [EZP-26106](https://jira.ez.no/browse/EZP-26106?src=confmacro) | [Error when tagging a service as a QueryType if the class is a parameter](https://jira.ez.no/browse/EZP-26106?src=confmacro)                              | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26106?src=confmacro) | Jul 19, 2016 | Jul 21, 2016 |
| [EZP-26116](https://jira.ez.no/browse/EZP-26116?src=confmacro) | [Error trashing an object with multiple locations](https://jira.ez.no/browse/EZP-26116?src=confmacro)                                                     | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26116?src=confmacro) | Jul 22, 2016 | Aug 25, 2016 |
| [EZP-26117](https://jira.ez.no/browse/EZP-26117?src=confmacro) | [Required richtext not validated as filled with single embed](https://jira.ez.no/browse/EZP-26117?src=confmacro)                                          | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26117?src=confmacro) | Jul 25, 2016 | Sep 01, 2016 |
| [EZP-26124](https://jira.ez.no/browse/EZP-26124?src=confmacro) | [Results of search in UDW overflow](https://jira.ez.no/browse/EZP-26124?src=confmacro)                                                                    | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26124?src=confmacro) | Jul 27, 2016 | Jul 28, 2016 |
| [EZP-26125](https://jira.ez.no/browse/EZP-26125?src=confmacro) | [Missing language parameter when generating \_ez\_content\_view route](https://jira.ez.no/browse/EZP-26125?src=confmacro)                                 | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26125?src=confmacro) | Jul 27, 2016 | Sep 08, 2016 |
| [EZP-26127](https://jira.ez.no/browse/EZP-26127?src=confmacro) | [Cannot publish content via content on the fly after select location](https://jira.ez.no/browse/EZP-26127?src=confmacro)                                  | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26127?src=confmacro) | Jul 27, 2016 | Aug 02, 2016 |
| [EZP-26130](https://jira.ez.no/browse/EZP-26130?src=confmacro) | [Search for content in many location hangs UI](https://jira.ez.no/browse/EZP-26130?src=confmacro)                                                         | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26130?src=confmacro) | Jul 28, 2016 | Sep 07, 2016 |
| [EZP-26141](https://jira.ez.no/browse/EZP-26141?src=confmacro) | [Search API appears to conduct some form of 'OR' search not an 'AND' search](https://jira.ez.no/browse/EZP-26141?src=confmacro)                           | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26141?src=confmacro) | Aug 02, 2016 | Nov 25, 2016 |
| [EZP-26145](https://jira.ez.no/browse/EZP-26145?src=confmacro) | [Unable to undo in the RichText editor](https://jira.ez.no/browse/EZP-26145?src=confmacro)                                                                | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26145?src=confmacro) | Aug 02, 2016 | Sep 05, 2016 |
| [EZP-26149](https://jira.ez.no/browse/EZP-26149?src=confmacro) | [Slashes in view parameters cause php notice](https://jira.ez.no/browse/EZP-26149?src=confmacro)                                                          | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26149?src=confmacro) | Aug 04, 2016 | Sep 02, 2016 |
| [EZP-26186](https://jira.ez.no/browse/EZP-26186?src=confmacro) | [Discarding content draft, and deleting Users does not correctly update Solr index](https://jira.ez.no/browse/EZP-26186?src=confmacro)                    | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26186?src=confmacro) | Aug 22, 2016 | Nov 02, 2016 |
| [EZP-26188](https://jira.ez.no/browse/EZP-26188?src=confmacro) | [Twig globals are not available in fields templates](https://jira.ez.no/browse/EZP-26188?src=confmacro)                                                   | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26188?src=confmacro) | Aug 22, 2016 | Aug 23, 2016 |
| [EZP-26228](https://jira.ez.no/browse/EZP-26228?src=confmacro) | [Delete content breaks content listing](https://jira.ez.no/browse/EZP-26228?src=confmacro)                                                                | [![Bug](https://jira.ez.no/images/icons/issuetypes/bug.png)](https://jira.ez.no/browse/EZP-26228?src=confmacro) | Aug 31, 2016 | Sep 08, 2016 |

 [20 issues](https://jira.ez.no/secure/IssueNavigator.jspa?reset=true&jqlQuery=project%3DEZP+AND+fixVersion+in+%28+%221.4.2%22+%29+ORDER+BY+issuetype+DESC%2C+key+ASC+++++++++++++&src=confmacro "View all matching issues in JIRA.")