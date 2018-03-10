# GraphQL
- GraphQL is a more flexible way of querying for data from an API
## Why GraphQL Instead of REST
- It eliminates the need to hit multiple REST endpoints to get data.  Only one query is needed for one endpoint to get multiple pieces of data
- Users can query specific pieces of data (instead of receiving a predetermined set of information and filtering it client-side)
## Three Types of Calls
- Query: a GraphQL call that retrieves information from an application through an API.  Syntactically, starts with the keyword "query" followed by a set of curly braces.  Has a Query Root as its first input field and a list of query parameters.  In the next set of curly braces, the set of information to be returned is listed.  In the following example, the name, email, and birthday of the user with ID "abc123" is requested.

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