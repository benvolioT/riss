# Composite Resources

## Problem

You want to know whether your service should combine resources to form a new composite resource.

## Discussion

Combine information from other resources is often useful. It limits client-server interactions, and gathers together related information into a single identifiable resource.

## Guidelines

1.  Consider client usage patterns, the likelihood of reuse, and performance and latency needs, and if these factors suggest it, form a new resource that aggregates other resources to reduce the number of client/server round trips.

2.  Composite representations should reuse existing XML or JSON schemas extending existing schemas where necessary.

3.  Composed elements should include HATEOAS links, including self references, so that clients can perform operations against the underlying resources as desired.  

## Standards

None.

## Recipes

None.

## Examples

Consider the following existing resources:

1.  https://example.com/tickets?account-number=123

2. https://example.com/invoices?account-number=123

A reasonable composite service might be:

https://example.com/accounts/123

Where the respresentation of this resource embeds the resources from (1) and (2) respectively:

    {
      "_links": {
        "self": {
          "href": "https://example.com/accounts/123"
        }
      }
    },
    "_embedded": {
      "tickets": [
        "_links": {
          "self": {
            "href": "https://example.com/tickets?account-number=123"
          }
        }
        ...
      ],
      "invoices": [
        "_links": {
          "self": {
            "href": "https://example.com/invoices?account-number=123"
          }
        }
        ...
      ]
    }

## Frequently Asked Questions

*Where should a composition be hosted: in a separate service or as a new capability on one of the composed services?*

Either way is acceptable. Use a separate task service if the composition is complex or involves operations that don't fit within the functional scope of an existing service. If, however, the composition extends an entity that is clearly within the scope of one service, it may be appropriate to add a capability to that service to provide the composition.


## References

1.  RESTful Web Services Cookbook, Subbu Allamaraju. [2.4 When to Combine Resources into Composites](http://search.safaribooksonline.com/9780596809140/recipe-when-to-combine-resources-into-composites), via Safari.
