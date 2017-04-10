# CS Content API  {#cs-content-api} {Draft Only}

### Introductory note

At this point this document is only a small part of the wider work on refining and defining the Content API more generally. Part of that more general work involves teasing out what API services we want. "Content API" can be very narrowly defined or it can be a more general thing. 

Initially the approach I took was to walk through [this spreadsheet](Research_Site_Panel_Breakdown_3-31-17.xlsx) alongside the latest mockups from vShift, and just document specific use cases. 

However, after mocking up a few varying use cases, and after discussion with Graeme / Javed it seemed like it would be good to make the "Content API" problem more focused on just the "purely content" related things.

It is undeniably true that there needs to be *somewhere* where the various types of 'content' need to combined and matched together, it is not at all a given that the job of 'combining' content from a range of APIs should be part of the Content API per se. For example [this page](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226615007) combines recommendations, content and taxonomy data together fairly seamlessly.

Looking at the mockups other APIs which are might be closely related to the Content API might include:
- Recommendations API
- Taxonomy API (company names, sector membership etc)
- Calendar/Events API (upcoming company events, CS events etc)
- Profile API 
- UI API (for page configurations, navigation elements etc)

For now this document focuses mostly on the 'narrow' use cases around Content API:
 - How to pull out specific content fields of "Content" required for different pages.
 - Defining a query format for how client side could define lists of content in various contexts 

There is, however some thoughts around the wider content api questions in the [discusssion](discussion.md) section at the end of this document.

### General claims 

All content responses will be sent using utf-8 encoding.

