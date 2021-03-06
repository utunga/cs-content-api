## Simple Content API

### 1.0 Full Content - Worth Watching {#content_1_0}

The simplest case is when we are simply requesting a list of pre-specified html/content fields which will flow into the new design in pre-agreed spots. This is the case with Worth Watchings. 

The only thing we need to do is specify which block of content we want. 

There are two ways to access content:
- via a content id \(like '206168'\) - if it is known
- via a known 'path' \(like '/about/team'\) - for when we don't know the id

All content can be access by id, but only *some content* also allows access via a known 'path'. In this case, however, we can just specify the content id. 

If we were using pure REST this would be as simple as:
<pre class="noheight"><code>GET /content/206168
</code></pre>

In GraphQL the equivalent is to POST the following to the /content_api/ endpoint:

```
POST
query { content(id:206168) {
  contentId,
  title,
  keyword,
  body
}}
```

Response:
<pre ><code class="prettify_json">
{ 
 "contentId": "206168",
 "templateType": "WorthWatching",
 "title": "U.S. Steel: Hesteel Said to Offer $1.4 bn for USSE",
 "keyword": "U.S. Steel",
 "body": "<p><b>U.S. Steel</b> (Caa1/B): According to Slovak newspaper Hospodarske Noviny, which previously reported on China's Hesteel Group bid for X's Europe unit in January (see <a href=\"/id/203088\">U.S. Steel: Rumored Negotiations for Europe Unit</a> 01-30-17), talks on the sale may be completed as early as this month. Hesteel is said to be offering around $1.4 bn for the integrated steel plant and coke production facilities that form the U.S. Steel Europe (USSE) segment. The Slovak government was also previously said to be interested in a small stake. The USSE segment has annual raw steel production capacity of 5 mn tonnes, and generated $265 mn in EBITDA last year on $2.2 bn in sales according to the company. A $1.4 bn price tag would value the unit at approximately 5.3x 2016 EBITDA. </p>"
}
</code></pre>



### 1.1 Full content - Marketing Home {#content_1_1}

[<img src="images/research_home.png" class="preview">](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226614585)

This is a case where the template won't necessarily know the id of the marketing home content, so would be easier to specify by a known path. (In this case "marketing/research_home")

When we are converting existing written analyst reports to the new system we will want to preserve the list of fields in the existing templates (we are presenting existing content in a new way). In other cases, such as with the new marketing home page we can start fresh, though it means we need to write new content to fit into the new boxes.

In this latter case vShift should specify what fields they desire and we can build authoring templates to match.

It is worth noting, per the above, that \(at least in this straw man proposal\) the content-type is not specified in the request. It is up to the page definitions/views to request the fields they want. The client side 'full content' views may end up having an almost one-to-one correspondence to the content authoring templates. However, because it is not necessary to pass content-type as a parameter, 'duck typing' is allowed in that, for example, if all you want is the  title across a range of templates that will work fine because we know from the schema that this is common. However, if a field is requested that doesnt exist in the serverside templatetype an error would be raised.

Currently we have a fairly large number of different templatetypes defined (see below) but hopefully with a bit of thought and some judicial use of sub-components, it would be possible to narrow this down to a shorter list. Html content will be delivered as json escaped string.

```
POST
{ 
  content(path:"marketing/research_home") 
  {
    title,
    intro,
    sections {
      section_title,
      section_body,
      section_image
    }
  }
}
```

<pre><code class="prettify_json">
{ 
  "data": {
    "title": "The leader in independent research",
    "intro": "<p>Institutional clients across the US, Europe, Middle East, Asia and Australia includes banks, investment advisors, mutual funds, pension managers, insurance companies, hedge funds, private equity ...",
    "sections": [
      {
        "section_title": "Product Feature One",
        "section_body": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ..",
        "section_image": "cdn/img/feature_one.png"
      },
      {
        "section_title": "Product Feature Two",
        "section_body": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ..",
        "section_image": "cdn/img/feature_two.png"
      },
      {
        "section_title": "Product Feature Three",
        "section_body": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ..",
        "section_image": "cdn/img/feature_three.png"
      }
    ]
  }
}
</code></pre>

### 1.2 Full content - Team Bio {#content_1_2}

Another example of content schema, this time based on pre-existing content type.

```POST
{ 
content(path:"/team/simon_adamson")
  {
    title,
    subtitle,
    body
  }
}
```

<pre><code class="prettify_json">
{ 
  "data": {
    "title": "Simon Adamson",
    "subtitle": "CEO of CreditSights Ltd / Senior Analyst - European Banks",
    "body": "<p>As head of the company's European business unit, Simon is also a member of the firm's Executive Committee and is on the CreditSights, Inc. Board of Directors. He joined CreditSights as Senior European Financial Analyst in 2003.</p><p> Prior to that he was a Managing Director, Head of European High Grade Research and Senior European Bank analyst at Deutsche Bank (1996-2003). Simon worked at rating agency IBCA, now part of FitchRatings, from 1987 to 1996 where in addition to covering banks in various European countries he was an Executive Committee member. Simon started his career in 1983 at Midland Bank's International Division, spending four years there in a variety of roles. He read Modern Languages at Sidney Sussex College, Cambridge University, graduating in 1983.</p>"
  }
}
</code></pre>

### 1.3 Content Element - Request Free Trial {#content_1_3}

As far as the API is concerned, html content for sub components rendered within other pages is no different than "full content" API requests. The only indication that content is shared across multiple pages might be the path used to store them \("/element/" in this case\).

One rule we should stick to is that all texft content should be stored in a template of some kind so that it can be updated by CS staff. This should include all text without exception.

```
{
  content(path:"/element/free_trial") {
    title,
    intro,
    buttonText,
  }
}
```

<pre><code class="prettify_json">
{ 
  "data": {
    "title": "Request a Free Trial",
    "intro": "Creditsights offers free trials to individuals in qualified institutions. At this time, we do not offer individual reports, products or services for the retail investor.",
    "buttonText": "Request a Trial"
  }
}
</code></pre>

### 1.4 Full Content - Analysis {#content_1_4}

[<img src="images/analysis_content.png" class="preview">](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226615100)

- Some discussion will be needed around embedded images and links. The suggestion here is to just embed these as simple references in the html returned. 
- Also, the current rendering of inline images supports an 'align left/align right' behavior. It may be important to preserve this behviour in some form in the new layout - specified in the below with a class="align\_left" attribute. 
- Finally there is also some special behavior around hiding or showing of the 'executive summary' section for analysis that we should discuss.


<div class="clear" ></div>

```
{
  content(id:206035) {
    contentId,
    title,
    summary,
    shortBullets,
    bullets,
    recommendationTitle,
    recommendation,
    metrics,
    metricsTitle,
    ratingsComment,
    ratingsCommentTitle,
    body
  }
}
```

<pre><code class="prettify_json">
{
    "contentId": 206035,
    "title": "Unipol: FY16 Capital Not Yet Optimised",
    "summary": "Unipol released relatively good FY16 earnings driven by a good underwriting profitability level in P&amp;C. We think there is value in investing in its 5.75% €750 mn perpetual surbordinated bond that trades with a Z-spread of 559.6 bp.",
    "shortBullets": [
      "While there is no doubt that Unipol Gruppo benefits from a strong franchise in Italy, the group remains exposed to Italian risk from both a business and an asset allocation perspective.",
      "Unipol Gruppo reported relatively good FY16 earnings despite the increase in claims (+3 pp YoY) and challenging market conditions in Life that drove to a 17.6% decline in Life premiums to €6,294 mn.",
      "Unipol's capital structure under Solvency II is not yet optimised; we find that the group suffers from a relatively lean capital based as the group reported a Solvency II margin of 141% (standard formula).",
      "Compared with Groupama's recently issued bullet subordinated bond (6% €650 mn), we prefer Unipol Sai's 5.75% €750 mn perpetual subordinated bond that currently trades with a Z-spread of 559.6 bp."
    ],
    "bullets": "<ul><li><strong>While there is no doubt that Unipol Gruppo benefits from a strong franchise in Italy, the group remains exposed to Italian risk from both a business and an asset allocation perspective.</strong></li><li><strong>Unipol Gruppo reported relatively good FY16 earnings despite the increase in claims (+3 pp YoY) and challenging market conditions in Life that drove to a 17.6% decline in Life premiums to €6,294 mn.</strong> The P&amp;C line of business did relatively well with a combined ratio of 95.6%. The risk profile of the bank did not improve materially due to the importance of the non-performing loan portfolio and the high cost-to-income ratio.</li><li><strong>Unipol's capital structure under Solvency II is not yet optimised; we find that the group suffers from a relatively lean capital based as the group reported a Solvency II margin of 141% (standard formula).</strong></li><li><strong>Compared with Groupama's recently issued bullet subordinated bond (6% €650 mn), we prefer Unipol Sai's 5.75% €750 mn perpetual subordinated bond that currently trades with a Z-spread of 559.6 bp.</strong> Between the two senior bonds issued by Unipol Gruppo, the ultimate holding company, we prefer the bond that presents the shorter duration because of the uncertainties linked to the current unoptimised capital position under Solvency II.</li></ul>",
    "recommendationTitle": "Relative Value",
    "recommendation": "<p>We have a Market perform recommendation for both Unipol and Groupama. Unipol Sai's outstanding subordinated bond (5.75% €750 mn Perpetual bond with a first call date on 18/6/2024) trades with a Z-spread of 559.6 bp (G-spread of 612.6 bp). We believe that he bond is likely to be called at its first call date in 2024; it remains Unipol Sai's key outstanding bond in the market. If the issuer does not call it back at its first call date, this may deteriorate the issuer's access to capital market prospectively. Consequently, we think it is in the best interest of Unipol Sai to call it. Compared with Groupama's recent 10-year bullet subordinated bond issuance (6% €650 mn issued on 17/1/2017) that trades with a Z-spread of 456.8 bp (G-spread of 401.5 bp), we find that Unipol's trade wide. The spread difference can be explained by the fact that Unipol Sai fully carries the Italian risk as it operates in Italy solely while Groupama's key market is France with a limited exposure to Italy. Additionally, Groupama's 6% xxx bond is bullet while Unipol Sai's 5.75% €750 mn is perpetual. Between the two bonds mentioned above, we would rather invest in Unipol considering its current spread level despite a relatively fragile risk profile as reflected in its Solvency II margin (172%).</p><p>Regarding Unipol Sai's two additional subordinated bonds (FRN €300 mn issued on 31/5/2001 and maturing on 15/6/2021 and FRN €300 mn issued on 24/7/2003 and maturing on 28/7/2023) that currently trade with a yield of 2.38% and 2.44% respectively, we do not think that the issuer will exercise the call option this year. In our latest article that focused on whether European issuers will exercise their call options in 2017 (see Euro Insurers: Will They Call Their Bonds In 2017?), we highlighted our views that these two bond would not be called in 2017 as they have not been called since the first call dates. We think that the rationale is based on the fact that they were marketed to retail investors who seem to be less concerned about extension risk.</p><p>Finally, the ultimate holding company, Unipol Gruppo, issued two senior bonds. The 3% €1 bn senior unsecured bond issued in 2015 with a maturity on 18/3/2025 currently trades with a Z-spread of 250 bp (G-spread of 302.6 bp). The bond was issued with a spread of 240 bp and is rated Ba2 and BB+ by Moody's and Fitch respectively. The additional 4.375% €500 mn bond issued on 27/2/2014 (maturity: 5/3/2021) currently trades with a Z-spread of 179 bp (G-spread of 244.6 bp). The bond was issued with a spread of 315 bp and is rated Ba2 and BB+ by Moody's and Fitch respectively. At the current Solvency II margin of 172% at Unipol Sai level, we believe that the risk of a non-payment of dividends to the holding company is relatively low in the short-to-medium term. Nevertheless, from a relative value perspective, we would rather favour the shorter duration as the issuer has not yet indicated its intentions on how to optimise its capital structure under Solvency II.</p>",
    "metrics": "",
    "metricsTitle": "",
    "ratingsComment": "",
    "ratingsCommentTitle": "",
    "body": "<p><img class=\"align_left\" src=\"/resources/490412/Unipol%202.png\" />There is no doubt that Unipol (the group) enjoys a strong franchise in Italy but suffers somehow from (i) a limited risk diversification considering the importance of the Non-Life  line of business (Motor accounted for 57% of premiums in P&amp;C in 2016) and (ii) the significant exposure towards Italian risk from both a business and investment perspective. Our opinion is nevertheless nuanced by the importance of the Motor line of business that reduces the volatility of its performance as a consequence of the size of the portfolio and independence of risks. In Life, Unipol remains a key player in Italy with a 6.5% market share in 2015 and premiums of €6,294 mn in 2016.</p> <p>Unipol benefits form a strong retail network with 3,000 agencies in Italy (20,000 agents). In P&amp;C, we challenge Unipol's multi-channel strategy as we believe it might become obsolete in the short-to-medium term. Indeed, Generali and Axa tend to maximise their supply to their personal lines of business through internet as they increase the agents' time to their Commercial and Corporate lines of business. In Life, we believe that Unipol will remain a relatively small player considering its limited bank network (4,800 banking branches) compared with Intesa for example. <img class=\"align_right\" style=\"font-size: 14px; background-color: rgb(255, 255, 255);\" src=\"/resources/490410/Unipol1.png\" /></p><p>Unipol group structure is made of a group holding, Unipol Gruppo Finanziario, and a a sub-group holding/operating entity, Unipol Sai, which is essentially made of the P&amp;C and Life activities. Both Unipol Gruppo Finanziario and Unipol Sai are exposed to the problematic bank subsidiary, Unipol Banca. Bonds are issued through these three entities. The senior unsecured bonds tend to be issued through the holding company, Unipol Gruppo Finanziario, while the subordinated debt are issued at the sub holding/operating entity, Unipol Sai. We do not cover the bonds issued at the bank level considering their relatively small sizes; they tend to be placed to retail investors. Considering the relatively weak quality of the loan portfolio, the relatively high cost-income ratio and the absence of a formal guarantee from both the Unipol Gruppo Finanziario and Unipol Sai, we would not recommend investing in the debt issued by Unipol Banca.</p> <p>We have to admit that we have been quite...&lt;snip></p>"
}
</code></pre>

### 1.5 Restricted Content - Analysis as anonymous {#content_1_5}


[<img src="images/analysis_limited.png" class="preview">](https://projects.invisionapp.com/share/3AB3R5F4S#/screens/226614609)

Access to content will be restricted according to the claims present in the auth token at the API level \(as well as, presumably, in the rendering layer\). For anonymous level access, regardless of what is requested, only title and teaser (aka summary) is returned. 

<div class="clear"></div>

```
    query content(id:206035) {
      contentId,
      title,
      summary,
      shortBullets,
      bullets,
      recommendationTitle,
      recommendation,
      metrics,
      metricsTitle,
      ratingsComment,
      ratingsCommentTitle,
      body
    }
```

<pre><code class="prettify_json">
{
    "contentId": 206035,
    "title": "Unipol: FY16 Capital Not Yet Optimised",
    "summary": "Unipol released relatively good FY16 earnings driven by a good underwriting profitability level in P&amp;C. We think there is value in investing in its 5.75% €750 mn perpetual surbordinated bond that trades with a Z-spread of 559.6 bp.",
    "shortBullets": [],
    "bullets": "",
    "recommendationTitle": "",
    "recommendation": "",
    "metrics": "",
    "metricsTitle": "",
    "ratingsComment": "",
    "ratingsCommentTitle": "",
    "body": ""
}
</code></pre>

### 1.6 Review of various content schemas {#content_1_6}

There are 48 templates in the old site, most of which we will just abandon, but a few we will want to port across. Per the discussion above, we will want to preserve the schema of written analyst content but can specify new schema for the new sections. A quick review of the two categories, relative to existing 'template types' follows.

**Consider keeping content in some form - porting across**

<pre><code class="prettify_json">
{
  "Analyst written articles": [
    "AnalysisTemplate (see above)",
    "WWTemplate (see above)",
    "MCTemplate",
    "ArticleTemplate",
    "TearsheetTemplate",
    "FundamentalsTearsheetTemplate",
    "PrivateWealthSheetTemplate",
    "FundPrivateWealthSheetTemplate",
    "CREWealthSheetTemplate",
    "SingleColSheetTemplate",
    "SingleColTearsheetTemplate",
    "UnchainedTearsheetTemplate"
  ],
  "Other written content": [
    "StaffProfileTemplate (see above)",
    "ContactTemplate",
    "LegalPageTemplate"
  ]
}
</code></pre>

**Assume this content can be ignored - not relevant to new design**

<pre class="noheight"><code class="prettify_json">
{
  "Home Page Templates": [
    "EuroMarketsTemplate",
    "StaticPageTemplate",
    "MarketingHomeTemplate",
    "HighYieldTemplate",
    "MarketViewsTemplate",
    "ForgotPasswordTemplate",
    "MunicipalsTemplate",
    "EmergingMarketsTemplate",
    "RatingsHomeTemplate",
    "SectorHomeTemplate",
    "SectorPerformanceTemplate",
    "TearsheetsTemplate",
    "HYHomeTemplate",
    "EuroHYHomeTemplate",
    "ResearchHomeTemplate",
    "SovereignsTemplate",
    "StrategyTemplate"
  ],
  "Misc Content": [
    "NewSubWelcomeTemplate",
    "AnnouncementsTemplate",
    "OneColStaticPageTemplate",
    "OurTeamTemplate",
    "ProductMarketingTemplate",
    "TopReadArticlesTemplate",
    "TourPageTemplate",
    "TwoColStaticPageTemplate"
  ],
  "Misc / Admin ": [
    "BoilerplateTemplate",
    "CustomDealBoilerplateTemplate",
    "ChangeStaffPasswordTemplate",
    "MyAccountTemplate",
    "RequestAccessTemplate"
  ],
  "Email Templates": [
    "EmailHeadingArticleTemplate",
    "DailyCommentTemplate",
    "EmailTemplate"
  ]
}
</code></pre>


### 1.7 Content Schema {#content_1_7}

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

*Subclasses of Content have all the properties above as well as ..*

<pre class="noheight"><code class="lang-json">
type WorthWatchingContent {
    keyword: String
    body: String
}
</code></pre>

<pre class="noheight"><code class="lang-json">
type AnalysisContent {
    shortBullets: String
    bullets: String
    recommendationTitle: String
    recommendation: String
    metrics: String
    metricsTitle: String
    ratingsComment: String
    ratingsCommentTitle: String
    body: String
}
</code></pre>

<pre class="noheight"><code class="lang-json">
type TeamBio {
    subtitle: String
    body: String
}
</code></pre>







