##### CS Content API Spec {#cs-content-api-spec}

{VERY MUCH DRAFT ONLY}

**Graph QL**

This proposal is just a straw man for further discussion. Amongst other things, it suggests using GraphQL instead of more standard REST for the Content API. This is partly because, per Joe&#039;s initial analysis, somewhat complex query logic may be required in some cases. It may be helpful to read this [introduction to GraphQL](https://facebook.github.io/react/blog/2015/05/01/graphql-introduction.html).

**Graph QL Demo**

To give a more &#039;hands on&#039; understanding of GraphQL I have set up a [demo site with live GraphQL queries using our data](https://console.graph.cool/Quick%20GraphQL/playground). Login as &#039;**mthompson@creditsights.com**&#039; with password &#039;**graphcoolql**&#039;. After you login

*   Click on &#039;playground&#039;*   Try copying and pasting the following into the left hand box and hitting &#039;play&#039;

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

_Of course is just a quick demo with limited data and doesn&#039;t actually implement the full content spec suggested below. That said it&#039;d be great if this document could eventually incorporate &#039;live endpoints&#039; so that the reader could experiment with different queries as specified, directly inline._

The top part of this page specifies API usage, at the bottom a start on the schema of the various response types is specified.

All content responses will be sent using utf-8 encoding.

At this point a straw man proposal is offered here. In particular

*   GraphQL instead of REST Resource based API*   Identification of tags via their short identifier - &quot;region/asia/&quot; instead of DisplayName (&quot;Asia&quot;) or Id (12345)*   Typing of tags only if requested.*   More complex logic supported in content queries via a GraphQL filter function that supports {AND, OR, NOT} semantics.