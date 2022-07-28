---
Stage: Accepted
Start Date: 2022-07-28
Release Date: Unreleased
Release Versions:
  ember-source: vX.Y.Z
  ember-data: vX.Y.Z
Relevant Team(s): Ember.js
RFC PR: 
---

<!--- 
Directions for above: 

Stage: Leave as is
Start Date: Fill in with today's date, YYYY-MM-DD
Release Date: Leave as is
Release Versions: Leave as is
Relevant Team(s): Fill this in with the [team(s)](README.md#relevant-teams) to which this RFC applies
RFC PR: Fill this in with the URL for the Proposal RFC PR
-->

# <RFC title>

## Summary

When invoking a component with the component helper:

```hbs
{{component 'my-component' reallyImportantArgument=this.foo disabled=false}}
```

there is no way to distinguish between arguments and atrributes. The latter param, disabled, will be passed
as an argument instead of attribute. One workaround is to use the let helper and use angle bracket syntax. However, this does not work when you want to yield a "preconfigured" component, e.g.

```hbs
{{yield (hash
  MyComponent=(component 'my-component' reallyImportantArgument=this.foo disabled=false)
)}}
```
This RFC proposes to use a new keyword: html-attributes to make the distinction. 

```hbs
{{yield (hash
  MyComponent=(component 'my-component' (html-attributes disabled=false) reallyImportantArgument=this.foo)
)}}
```

## Motivation

This feature would provide a way to pass html attributes like "class" to a yielded component. 

## Detailed design

> This is the bulk of the RFC.

> Explain the design in enough detail for somebody
familiar with the framework to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

## How we teach this

> What names and terminology work best for these concepts and why? How is this
idea best presented? As a continuation of existing Ember patterns, or as a
wholly new one?

> Would the acceptance of this proposal mean the Ember guides must be
re-organized or altered? Does it change how Ember is taught to new users
at any level?

> How should this feature be introduced and taught to existing Ember
users?

## Drawbacks

> Why should we *not* do this? Please consider the impact on teaching Ember,
on the integration of this feature with other existing and planned features,
on the impact of the API churn on existing apps, etc.

> There are tradeoffs to choosing any path, please attempt to identify them here.

## Alternatives

> What other designs have been considered? What is the impact of not doing this?

https://github.com/emberjs/rfcs/issues/497

Without this feature, when ember users need to yield a component and add a "class" attribute, 
they can workaround by creating a wrapping component that adds the styles, and use the component helper to 
invoke the wrapper. This is cumbersome because we then have components created for the sole purpose of adding a html attribute.

> This section could also include prior art, that is, how other frameworks in the same domain have solved this problem.

## Unresolved questions

> Optional, but suggested for first drafts. What parts of the design are still
TBD?
