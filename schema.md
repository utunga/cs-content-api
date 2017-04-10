##### Schema {#schema}

JSON Responses should correspond to elements from this schema

```

type Content {
  contentId: Int
  contentType: String
  createdAt: DateTime!
  id: ID!
  publishDate: DateTime
  summary: String
  tags: [Tag!]! @relation(name: "ContentTags")
  teaser: String
  templateType: String
  title: String
  updatedAt: DateTime!
  viewsLast24Hrs: Int
  viewsLast7Days: Int
}

-- subclasses of Content so should have all those properties as well

type WorthWatchingContent {
  body: String
  keyword: String
  title: String
}

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

-- recommendation weighting can be 'overweight', 'marketweight' or 'underweight'

type Recommendation {
  createdAt: DateTime!
  id: ID!
  updatedAt: DateTime!
  recommendationOn: Tag 
  weighting: String  
}

type Event {
  createdAt: DateTime!
  id: ID!
  updatedAt: DateTime!
  recommendationOn: Tag 
  weighting: String  
}

```

<footer>

footer

</footer>

**Illegal HTML tag removed :** $(&quot;.prettyify&quot;).each( function() { var json = JSON.parse($(this).text()); $(this).html(library.json.prettyPrint(json)); });