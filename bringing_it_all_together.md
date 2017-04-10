##### Bringing it all together {#bringing-it-all-together}

Hints on how to leverage GraphQL

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