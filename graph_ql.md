##### **Graph QL** {#cs-content-api-spec}

This proposal is just a straw man for further discussion. However amongst other things, it suggests using GraphQL instead of more standard REST for the Content API. This suggestion is made, partly because, in alignment with Joe's analysis in Word, somewhat complex query logic may be required in some cases. 

To get a quick introduction to GraphQL it may be helpful to read this [introduction to GraphQL](https://facebook.github.io/react/blog/2015/05/01/graphql-introduction.html).

**Graph QL Demo**

To get a more 'hands on' understanding of GraphQL as applied to this use case I have set up a [demo site with live GraphQL queries using some of our data](https://console.graph.cool/Quick GraphQL/playground). 

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

_Of course is just a quick demo with limited data and doesn't actually implement the full content spec suggested below. That said it'd be great if this document could eventually incorporate 'live endpoints' so that the reader could experiment with different queries, directly inline.

