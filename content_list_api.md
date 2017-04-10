## Content List API {#content-list-api}

Logic for creating lists of content on home pages.

###  2.0 An example of a more complex query {#content_2_0}

It seems like a good idea to start with a more complex query, this one pulled from an example in Joe's analysis to date (in fact the following query does a little more than that). This query finds the most recent "Market Update" from _either_ TMT-Europe _OR_ TMT-Automotive. NB this query runs directly on the demo site. 

``` 
query { allContents (
  filter: {
    AND: [
      { tags_some: { tagId: "region/europe" } },
      {
        OR : [ { tags_some: { tagId: "sector/tmt" } },
               { tags_some: { tagId: "sector/automotive" } }
      ]}
      { contentType_ends_with: "MarketUpdates" }  
      ]
  },
  first: 1,
  orderBy: publishDate_DESC)
  {
  title,
  contentId,
  contentType 
  }
}
```

This can be run on the demo server, and gives this result:

<pre><code class="prettify_json">
{
  "data": {
    "allContents": [
      {
        "title": "Euro TMT Market Updates: The Netherlands",
        "contentId": 199378,
        "contentType": "EuroTMTMarketUpdates"
      }
    ]
  }
}
</code></pre>



###  2.1 European High Yield - Market Overview - Recently published {#content_2_1}

For left column on [Euro HY / Marketview mockup](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226614980)

Note the use of:
* _types) property to specify the allowed contentType \(respects content type hierachy\)
* _filter_ property with boolean logic on tags \(including 'not' logic via 'tags\_none'\)

Worth noting that the boolean logic in the filter query is 'well defined' but not part of the GraphQL spec per se. We would have to implement this behavior ourselves. \(It is also implemented in graph.cool [demo](https://console.graph.cool/Quick GraphQL/playground)\)

```
query { contentList (
  first: 20,
  orderBy: publishDate_DESC,
  types: ["analysis", "reports", "worthwatching"],
  filter: {
    AND: [
      { tags_some: { tagId: "tag/high_yield" } },
      { tags_some: { tagId: "region/asia" } },
      { tags_none: { tagId: "tag/emerging_markets" } }
    ]
  })
  {
  title,
  contentType,
  publishDate
}}

---

Or, to use directly in demo:

query { allContents (
  filter: {
    AND: [
      { tags_some: { tagId: "tag/high_yield" } },
      { tags_some: { tagId: "region/europe" } },
      { tags_none: { tagId: "tag/emerging_markets" } }
    ]
  },
  first: 20,
  orderBy: publishDate_DESC)
  {
  title,
  contentId,
  contentType
  }
}
```

<pre><code class="prettify_json">
{
  "data": {
    "contentList": [
      {
        "title": "HY Note: EA Partners I &amp; II",
        "contentId": 199150,
        "contentType": "HighYieldNotes"
      },     
      {
        "title": "4Q16 European Quarterly Credit Market Monitor",
        "contentId": 199982,
        "contentType": "EuroQuarterlyCreditMonitor"
      },
      {
        "title": "Iceland Foods F2Q17: Return to Growth - Buy",
        "contentId": 199989,
        "contentType": "EarningsNote"
      },
      {
        "title": "HY Note: Ladbrokes Markets Bonds for Coral Merger",
        "contentId": 199955,
        "contentType": "HighYieldNotes"
      },
      {
        "title": "Codere: Price Talk Emerges for USD/EUR Notes",
        "contentId": 199956,
        "contentType": "WorthWatching"
      },
      {
        "title": "Cemex 3Q16: Deleveraging Accelerates, Stay O/P",
        "contentId": 199947,
        "contentType": "EarningsNote"
      },
      {
        "title": "ECB Corporate Purchases: Week to Oct 28",
        "contentId": 199910,
        "contentType": "ECBCorporatePurchases"
      },
      {
        "title": "CNHI 3Q16: Margins Improve, Down-cycle Continues",
        "contentId": 199948,
        "contentType": "EarningsNote"
      },
      {
        "title": "CNHI 3Q16: Margins Improve, Down-cycle Continues",
        "contentId": 199948,
        "contentType": "EarningsNote"
      },
      {
        "title": "Sterling Spreads: Week Ended, October 28, 2016",
        "contentId": 199881,
        "contentType": "SterlingSpreads"
      },
      {
        "title": "Euro Spreads: Week Ended, October 28, 2016",
        "contentId": 199877,
        "contentType": "EuroSpreads"
      },
      {
        "title": "Piaggio 3Q16 Positive Trend in 2W Recovery",
        "contentId": 199860,
        "contentType": "WorthWatching"
      },
      {
        "title": "Cellnex 3Q16: ECB Eligibility is a Key Priority",
        "contentId": 199861,
        "contentType": "EarningsNote"
      },
      {
        "title": "Rexel 3Q16: Copper-Bottomed?",
        "contentId": 199858,
        "contentType": "EarningsNote"
      },
      {
        "title": "Global Ship Lease 3Q16: Tick Tick Tick ...",
        "contentId": 199853,
        "contentType": "EarningsNote"
      },
      {
        "title": "Euro Financial Movers: The Trading Games",
        "contentId": 199765,
        "contentType": "euroFinancialMovers"
      },
      {
        "title": "The Navigator Company: 3Q16 Review",
        "contentId": 199774,
        "contentType": "WorthWatching"
      },
      {
        "title": "BUT SAS: New €380 mn SSNs Price @ 5.5%",
        "contentId": 199714,
        "contentType": "WorthWatching"
      },
      {
        "title": "Elis: 3Q16 – Troubles in France Weigh on Margins",
        "contentId": 199767,
        "contentType": "WorthWatching"
      },
      {
        "title": "Areva: Guides Up 2016 Cash Flow",
        "contentId": 199769,
        "contentType": "WorthWatching"
      }
    ]
  }
}
</code></pre>

### 2.2 European High Yield - Market Overview - Highlights {#content_2_2}

For central column on [Euro HY / Marketview mockup](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226614980)

Same as last query but filtered by 'highlights' feedtag, and slightly different content types

```
query { contentList (
  first: 5,
  orderBy: publishDate_DESC,
  types: ["analysis", "reports"],
  filter: {
    AND: [
      { tags_some: { tagId: "tag/high_yield" } },
      { tags_some: { tagId: "region/europe" } },
      { tags_some: { tagId: "feedtag/european_subscriber_highlight" } }
    ]
  })
  {
  title,
  contentType,
  publishDate
}}
```

<pre><code class="prettify_json">
{
  "data": {
    "contentList": [
      {
        "title": "CNHI 3Q16: Margins Improve, Down-cycle Continues",
        "contentId": 199948,
        "contentType": "EarningsNote"
      },
      {
        "title": "Sterling Spreads: Week Ended, October 28, 2016",
        "contentId": 199881,
        "contentType": "SterlingSpreads"
      },
      {
        "title": "Euro Spreads: Week Ended, October 28, 2016",
        "contentId": 199877,
        "contentType": "EuroSpreads"
      },
      {
        "title": "Global Ship Lease 3Q16: Tick Tick Tick ...",
        "contentId": 199853,
        "contentType": "EarningsNote"
      },
      {
        "title": "Euro Financial Movers: The Trading Games",
        "contentId": 199765,
        "contentType": "euroFinancialMovers"
      }
    ]
  }
}
</code></pre>

### 2.3 European High Yield - Market Overview - Sector Analysis and Reports {#content_2_3}

For central column on [Euro HY / Marketview mockup](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226614980)

Note the ability to specify 'focus:true' at a lower level in the query.

```
query { contentList (
  first: 5,
  orderBy: publishDate_DESC,
  types: ["sectorAnalysis", "sectorReport"],
  filter: {
    AND: [
      { tags_some: { tagId: "tag/high_yield" } },
      { tags_some: { tagId: "region/europe", focus:true } }
   }
    ]
  })
  {
  title,
  contentType,
  publishDate
}}
```

<pre><code class="prettify_json">
{
  "data": {
    "contentList": [
      {
        "title": "4Q16 European Quarterly Credit Market Monitor",
        "contentId": 199982,
        "contentType": "EuroQuarterlyCreditMonitor"
      },
      {
        "title": "ECB Corporate Purchases: Week to Oct 28",
        "contentId": 199910,
        "contentType": "ECBCorporatePurchases"
      },
      {
        "title": "Euro Financial Movers: The Trading Games",
        "contentId": 199765,
        "contentType": "euroFinancialMovers"
      },
      {
        "title": "ECB Corporate Bond Purchases - Week to Oct 21",
        "contentId": 199473,
        "contentType": "StrategyComment"
      },
      {
        "title": "Euro Financial Movers: Season of Mists and Mergers",
        "contentId": 198879,
        "contentType": "euroFinancialMovers"
      }
    ]
  }
}
</code></pre>

### 2.4 European High Yield - Highlights - Most Read {#content_2_4}

For left column on [Euro HY / Highlights mockup](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226614985)

This is similar to the last query but sorted by ViewsLast24Hrs

```
query { contentList (
  first: 5,
  orderBy: viewsLast24Hrs_DESC,
  types: ["analysis", "reports"],
  filter: {
    AND: [
      { tags_some: { tagId: "tag/high_yield" } },
      { tags_some: { tagId: "region/europe" } },
      { tags_some: { tagId: "feedtag/european_subscriber_highlight" } }
    ]
  })
  {
  title,
  contentType,
  publishDate
}}
```

<pre><code class="prettify_json">
{
  "data": {
    "contentList": [
      {
        "title": "CNHI 3Q16: Margins Improve, Down-cycle Continues",
        "contentId": 199948,
        "contentType": "EarningsNote"
      },
      {
        "title": "Sterling Spreads: Week Ended, October 28, 2016",
        "contentId": 199881,
        "contentType": "SterlingSpreads"
      },
      {
        "title": "Euro Spreads: Week Ended, October 28, 2016",
        "contentId": 199877,
        "contentType": "EuroSpreads"
      },
      {
        "title": "Global Ship Lease 3Q16: Tick Tick Tick ...",
        "contentId": 199853,
        "contentType": "EarningsNote"
      },
      {
        "title": "Euro Financial Movers: The Trading Games",
        "contentId": 199765,
        "contentType": "euroFinancialMovers"
      }
    ]
  }
}
</code></pre>

### Content List Schema {#content_list_schema}

JSON Responses should correspond to elements from this schema

<pre><code class="lang-json noheight">
type Content {
  contentId: Int
  contentType: String
  templateType: String
  title: String
  summary: String
  createdAt: DateTime!
  id: ID!
  publishDate: DateTime
  summary: String
  tags: [Tag!]!
  updatedAt: DateTime!
  viewsLast24Hrs: Int
  viewsLast7Days: Int
}
</code></pre>

<pre><code class="lang-json noheight">
type Tag {
  content: Content @relation(name: "ContentTags")
  createdAt: DateTime!
  focus: Boolean
  id: ID!
  name: String
  tagId: String
  type: String
  updatedAt: DateTime!
}
</code></pre>

It can be thought of as a list of Content objecs, each with a flattened list of tags on them. Like this:

<pre><code class="lang-json noheight">
[
  {
    "contentId": 200000,
    "contentType": "WorthWatching",
    "publishDate": "2016-11-01T21:31:27Z",
    "title": "Shell: Strong 3Q16 Beat, Healthy Momentum",
    "summary": "Shell (Aa2/A/AA-): On the 1 November 2016 Shell released its 3Q16/9M16 results with earnings coming out significantly above analysts' estimates driving a healthy increase in share price (c. +4%). These results show that as the BG acquisition i ..",
    "tags": [
      {
        "id": 18569506,
        "type": "Company",
        "focus": true,
        "tagId": "company/royal_dutchshell",
        "name": "Royal Dutchshell Group"
      },
      {
        "id": 18571333,
        "type": "Tag",
        "focus": true,
        "tagId": "tag/earnings",
        "name": "Earnings"
      },
      {
        "id": 18569515,
        "type": "Sector",
        "focus": false,
        "tagId": "sector/energy",
        "name": "Energy"
      },
      {
        "id": 18569518,
        "type": "Country",
        "focus": false,
        "tagId": "country/netherlands",
        "name": "Netherlands"
      },
      {
        "id": 18569530,
        "type": "Tag",
        "focus": false,
        "tagId": "tag/investment_grade",
        "name": "Investment Grade"
      },
      {
        "id": 18569533,
        "type": "GhostTag",
        "focus": false,
        "tagId": "ghosttag/corporates",
        "name": "Corporates"
      },
      {
        "id": 18569512,
        "type": "Sector",
        "focus": false,
        "tagId": "sector/oil_gas",
        "name": "Oil and Gas"
      },
      {
        "id": 18569521,
        "type": "Region",
        "focus": false,
        "tagId": "region/europe",
        "name": "Europe"
      }
    ]
  },
</code></pre>