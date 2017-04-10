##### query contentList {} {#query-contentlist}

logic for populating home pages

2.0 European High Yield - Market Overview - Recently published

For left column on [Euro HY / Marketview mockup](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226614980)

Note the use of

*   **types** property to specify the allowed contentType (respects content type hierachy)*   **filter** property with boolean logic on tags (including &#039;not&#039; logic via &#039;tags_none&#039;)

Worth noting that the boolean logic in the filter query is &#039;well defined&#039; but not part of the GraphQL spec per se. We would have to implement this behavior ourselves. (It is also implemented in graph.cool [demo](https://console.graph.cool/Quick%20GraphQL/playground))

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

```

{
  "data": {
    "allContents": [
      {
        "title": "HY Note: EA Partners I & II",
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

```

2.1 European High Yield - Market Overview - Highlights

For central column on [Euro HY / Marketview mockup](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226614980)

Same as last query but filtered by &#039;highlights&#039; feedtag, and slightly different content types

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

```

{
  "data": {
    "allContents": [
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

```

2.2 European High Yield - Market Overview - Sector Analysis and Reports

For central column on [Euro HY / Marketview mockup](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226614980)

Note the ability to specify &#039;focus:true&#039; at a lower level in the query.

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

```

{
  "data": {
    "allContents": [
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

```

2.3 European High Yield - Highlights - Most Read

For left column on [Euro HY / Highlights mockup](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226614985)

Similar to last query but sorted by ViewsLast24Hrs

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

```

{
  "data": {
    "allContents": [
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

```