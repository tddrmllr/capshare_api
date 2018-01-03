# HTTP Responses
Every request includes an HTTP status code with the result. The status code should examined before the response. In most error cases, the response body will contain an errors hash with more information.

```ruby
# Example 200 response for collection
[
  { date: "2015-12-01", id: 1, shares: 999 },
  { date: "2014-11-07", id: 2, shares: 555 },
]

# Example 200 response for single resource
{ date: "2015-12-01", id: 1, shares: 999 }


# Example 201 response
{ date: "2015-12-01", id: 1, shares: 999 }
```

### Success
Code       | Meaning
---------- | -------
200        | OK -- The request was successful.
201        | Created -- The resource was successfully created.
204        | No Content -- The request was successful and there is no response body.

<aside class="notice">
  For an index resource, the response body will be a JSON array of hashes for objects in the collection. For a single resource or a create, the response body will be a JSON hash of the object.
</aside>

```ruby
# Example 422 response
{
  date: ["can't be blank"],
  authorized_shares: ["must be greater than 0"]
}
```

### Client Error
Code       | Meaning
---------- | -------
403        | Forbidden -- The client is requesting an action or a resource that it does not have privileges for.
422        | Unprocessable Entity -- The request could not be completed because the request was invalid.
