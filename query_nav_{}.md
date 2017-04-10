##### query nav {} {#query-nav}

0.0 Primary Navigation

Because of close relationship to the view model binding this area needs a lot of input from vShift. For instance nav items, often include routing configuration such as view names or other component configuration. In the below there is just a simple &#039;view&#039; paramater with name of the template.

In this proposal the &#039;view&#039; specified will in turn know to request certain fields from, for example, the &#039;fullContent&#039; query (see below). But there are other ways we could do this. Best to discuss with from client side developers on how they want to handle this.

&#039;Subnav&#039; on an element simply indicates that items on this list should be rendered as pop-out or drop down or however desired as a &#039;sub&#039; nav. It is assumed that the &quot;id&quot; field could be used to pull certain nav elements (such as &#039;login&#039;) out of the main display list and into other places on the page.

```

query nav(currentPath: "/", isPrimary: true) {
    path,
    name,
    subnav,
    id
  }

```

```

{

"data":
[
  {
    "path": "/research",
    "id": "research",
    "name": "Research",
    "view": "marketing_index_template"
  },
  {
    "path": "/rp",
    "id": "rp",
    "name": "Risk Products",
    "view": "marketing_index_template"
  },
  {
    "name": "About Us",
    "subnav": [
      {
        "path": "/about_us",
        "tab":  "company",
        "name": "Our Company",
        "view": "marketing_one_page_template"
      },
      {
        "path": "/about_us",
        "tab":  "products",
        "name": "Our Products",
        "view": "marketing_one_page_template"
      },
      {
        "path": "/about_us",
        "tab":  "team",
        "name": "Our Team",
        "view": "marketing_one_page_template"
      },
      {
        "path": "/about_us",
        "tab":  "careers",
        "name": "Careers",
        "view": "marketing_one_page_template"
      },
      {
        "path": "/news",
        "name": "News",
        "view": "marketing_news_template"
      },
      {
        "path": "/contact",
        "name": "Contact Us",
        "view": "marketing_contact_template"
      }
    ]
  },
  {
    "path": "/free_trial",
    "id": "free_trial",
    "name": "Free Trial",
    "view": "free_trial_template"
  },
  {
    "path": "/log_in",
    "id": "log_in",
    "name": "Log In",
    "view": "log_in_template"
  }
]}

```

0.1 Secondary Navigation

Similar api to primary navigation but an alternative list for rendering elsewhere. Can be context dependent - current path is passed in.

All navigation elements may be rendered as &#039;tabs&#039; within the current page, or alternatively they can be links that feel like loading whole new &#039;pages&#039;. This behavior is specified by adding &#039;tab&#039; property which the view engine can handle appropriately. There is no reason for there to be a correspondence between behavior as &#039;tabs&#039; and the location of navigation - that&#039;s up to the view to implement, so &#039;tab&#039; is just a simple informational property as far as the API is concerned.

```

query nav(currentPath: "/", isPrimary: false) {
  path,
  tab,
  name,
  view
}

```

```

{ 
  "data": [
    {
      "path": "/about_us",
      "tab":  true,
      "name": "Our Company",
      "view": "marketing_one_page_template"
    },
    {
      "path": "/about_us",
      "tab":  true,
      "name": "Our Products",
      "view": "marketing_one_page_template"
    },
    {
      "path": "/about_us",
      "tab":  true,
      "name": "Our Team",
      "view": "marketing_one_page_template"
    },
    {
      "path": "/about_us",
      "tab":  true,
      "name": "Careers",
      "view": "marketing_one_page_template"
    },
    {
      "path": "/news",
      "tab" : false,
      "name": "News",
      "view": "marketing_news_template"
    },
    {
      "path": "/contact",
      "tab" : false,
      "name": "Contact Us",
      "view": "marketing_contact_template"
    }
  ]
}

```