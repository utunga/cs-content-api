##### **Graph QL** {#cs-content-api-spec}

This proposal is just a straw man for further discussion. 

However amongst other things, it suggests we consider GraphQL instead of a more standard REST interface for the Content API. This suggestion is made partly because, in alignment with Joe's analysis in Word, somewhat complex query logic may be required in some cases and it feels like POSTing those queries would be easier/more powerful. 

To get a quick introduction to GraphQL it may be helpful to read this [introduction to GraphQL](https://facebook.github.io/react/blog/2015/05/01/graphql-introduction.html).

**Graph QL Demo**

A more 'hands on' demo of GraphQL as applied to this use case has been set up a [here](https://console.graph.cool/Quick GraphQL/playground). This allows the use of live GraphQL queries against some of our data.

* Login as '**mthompson@creditsights.com**' with password '**graphcoolql**'. 
* Click on 'playground' link
* Try copying and pasting the following into the 'query' box (on left) and hitting play

```
# European (TMT or Automotive) Tearsheets 
query { allContents (
  filter: {
    AND: [
      { contentType: "FundamentalsTearsheet" }
      { tags_some: { tagId: "region/europe" } },
      { OR : [ { tags_some: { tagId: "sector/tmt" } },
               { tags_some: { tagId: "sector/automotive" } }]}
      ]
  },
  first: 2,
  orderBy: publishDate_DESC)
  {
  title,
  contentId,
  publishDate,
  contentType,
  # try uncommenting this..
  #tags {
  #  tagId,
  #  name
  #}
  }
}
```

Of course this is just a quick demo with limited data and doesn't actually implement the full content spec suggested below. That said it'd be great if this document could eventually incorporate 'live endpoints' so that the reader could experiment with different queries, directly inline.


