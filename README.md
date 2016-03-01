# Ember-cli-multi-store-service

This is a fairly simple Ember CLI addon for managing multiple Ember Data stores. Normally one store is all that an application needs, but sometimes life throws you curve balls.

## Why would I need multiple stores?

- Loading fixture data in an easy to swap out area
- Managing the state of multiple isolated databases
- Working with historical data snapshots
- Crazy situations I've never thought of

## Are there any rules I need to follow to use this?

Not too many, but I have a few recommendations based on experience using multiple stores:

- Stop using the injected store.
    - Either pass down the store that you want to use explicitly as an attr, or inject this service (`service:multi-store`) and grab the store you need by name as needed.
- Seriously, don't inject the store into anything else like adapters or serializers
    - At this point the store that you use will pass itself to adapters and serializers, build them in a stateless fashion that only use the correct store passed in.
    - Each store from this service has a `name` attribute to be used for directing requests as needed at call time.
- Use this in moderation
    - I know I'm not selling this well, but it should really only be useful when you need total data isolation and/or expect to see multiple conflicting versions of the same objects (same id and type).

## How does this play with the Ember Inspector?

Not too bad, at least as far as I've tested it. There is a `switchInspectorStore()` method on the service that will let you change which store you're viewing information on. You'll have to change views away from the data section to see the change as it's not dynamically watching for the store change. This also uses an undocumented and private API for the inspector. Don't be surprised if it stops working. Instead just open a new issue and I'll take a look at it

## How about some usage documentation?

I'll do that soon enough.