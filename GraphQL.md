# GraphQL
GraphQL is a more flexible and efficient (in terms of data and speed) way of querying for data from an API.
## Why GraphQL Instead of REST
- It eliminates the need to hit multiple REST endpoints to get data.  Only one query is needed for a single endpoint to get multiple pieces of data; this eliminates the combined latency involved with multiple HTTP requests executed serially.
- Users can query specific fields of data (instead of receiving a predetermined set of information and filtering it client-side) from the API.
## Three Types of Calls
- Query: a GraphQL call that retrieves information from an application through an API.  Syntactically, it starts with the keyword "query" followed by a set of curly braces.  Then, there is a Query Root as its first input field and a list of query parameters.  In the next set of curly braces, the set of information to be returned is listed.  In the following example, the name, email, and birthday of the user with ID "abc123" is requested.

    ```javascript
    query{
        user(id:"abc123"){
            name
            email
            birthday
        }
    }
    ``` 

- Mutation: a GraphQL call that updates information in an application's database through an API
- Subscriptions


## A More Complex Query
```javascript
{
  shop { //shop represents a collection of the general settings and information about the shop
    name //gets the name of the shop
    products(first:2){ // yields a ProductConnection to the first two products.  The connection points to the products graph
      edges{ // traverses edges of products graph
        node{ // gets each node to return
          title // get the title of each node
          images(first:1){ // yields an ImageConnection for the returned product node which points to a graph of images
           	edges{
                node{
                  src // only get the src field for each image node
                }
              } 
          }
          variants(first:1){ //yields a variantsConnection pointing to a graph of variants for that specific product (defined by the product node)
            edges{
              node{
                id //gets ID for the specific variant node
              }
            }
          }
        }
      }
    }
  }
}
```
This query returns the following:
```javascript
{
  "data": {
    "shop": {
      "name": "graphql",
      "products": {
        "edges": [
          {
            "node": {
              "id": "Z2lkOi8vc2hvcGlmeS9Qcm9kdWN0Lzk4OTUyNzYwOTk=",
              "title": "Snare Boot",
              "images": {
                "edges": [
                  {
                    "node": {
                      "src": "https://cdn.shopify.com/s/files/1/1312/0893/products/001_grande_89f870ed-dc56-4990-9aa5-4f11ddf13108.jpg?v=1491918957"
                    }
                  }
                ]
              }
            }
          },
          {
            "node": {
              "id": "Z2lkOi8vc2hvcGlmeS9Qcm9kdWN0Lzk4OTUyNzkwNDM=",
              "title": "Neptune Boot",
              "images": {
                "edges": [
                  {
                    "node": {
                      "src": "https://cdn.shopify.com/s/files/1/1312/0893/products/001_f5b2f018-5434-446e-912c-10484293c134.jpg?v=1491850944"
                    }
                  }
                ]
              }
            }
          }
        ]
      }
    }
  }
}
```
Note: the schema of the returned data matches the schema of the GraphQL query.