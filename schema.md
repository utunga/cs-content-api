


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
