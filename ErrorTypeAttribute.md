Definition Type Attribute exception on query

# Introduction #

There is a bug in adf 11g for task flow switch and saved search of af:query.


# Details #
## Version ##
  * JDeveloper 11.1.1.2 and 11.1.1.3
  * Weblogic 10.3.2 and 10.3.3

## Developement ##
You can skip this section by download the project source directly.

The program is very simple, there are 2 pages, one search page and one blank page. The search page contains an af:query with saveQueryMode="readOnly", the query is binding to a ViewObject, the ViewObject has 2 view criteria. Therefore, the query in the search page has 2 Saved Search items.

There are some condition for the 2 view criterias,
Criteria 1 is defined as a Quick Search, which includes some simple fields;
Criteria 2 is defined as an Advance Search, which includes all the fields defined in Criteria 1, and some extra fields. The most important is Criteria 2 must include some extra fields that have a ListOfValue (a dropdown selection in the query UI).

Finally, the search page has a link (action="toblank") go to blank page. and the blank page has a link (action="tosearch") go to search page. The "toblank" and "tosearch" is defined in the taskflow xml. (use Link is very important! button has no problem).

## Bug Details ##
To see the bug, please follow the steps below in the project:
  1. Visit the search page, click Search (The default search is Criteria 1: Quick Search)
  1. select Advance Search from Saved Search dropdown, and click the Search again.
  1. go to blank page by click the link in search page.
  1. go to search page by click the link in blank page.
  1. Select quick search from Saved Search dropdown, and click the search.
  1. go to blank page by click the link in search page.
  1. go to search page by click the link in blank page.

at step 7 you will find an popup exception as below (the exception popup whenever you visit the search page! until redeploy the application.):

```
Messages for this page are listed below.
	
Definition __vcrow_indexed_attribute__FkGrade_0 of type Attribute is not found in ApplicationModule_PostingVO1_PostingQuickSearch_12237.
	
Definition __vcrow_indexed_attribute__FkAppointment_0 of type Attribute is not found in ApplicationModule_PostingVO1_PostingQuickSearch_12237.
```


# Resources #
[Demo Output](http://code.google.com/p/adf-samples-demos/issues/detail?id=2)

[Demo Source](http://adf-samples-demos.googlecode.com/files/ErrorTypeAttribute.rar)