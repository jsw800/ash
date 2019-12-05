# Ash

Ash is an Elixir framework designed to work with Phoenix. At it's core is a concept called a `Resource` which enables developers to declaritively define modules of an entity (such as a database table) and in doing so automatically create a public API for that entity that be accessed and transmitted in many forms such as JSONAPI, GraphQL, LiveView, or just within Elixir code elsewhere in a Phoenix app with very little configuration.

Developers shoud be focusing on their core business logic - not boilerplate code such as filtering, pagination, serializing, and sideloading relational data. Yet seemingly everytime a new Phoenix app is created all this concepts need to get reinvented or brought in piecemeal. This takes substantial time and money and is highly inefficient.

Ash builds upon the incredible power of Phoenix and empowers developers to get up and running with a fully functional app in substantially less time, while still being flexible enough to allow customization when it inevitably comes up.

Ash is an open source project, and draws inspiration from similar ideas in other frameworks and concepts. The goal of Ash is to lower the barrier to adopting and using Elixir and Phoenix, and in doing so help these amazing communities attract new develpers, projects, and companies.

## Quick Links
* For Resource DSL documentation, see: [Ash.Resource](Ash.Resource.html)

## TODO LIST (in no order)

* Make our router cabaple of describing its routes in `mix phx.routes` Chris McCord says that we could probably power that, seeing as phoenix controls both APIs, and that capability could be added to `Plug.Router`
* Finish the serializer
* Make primary key type configurable
* Make a DSL for join tables to support complex validation/hooks into how they work, support more than just table names in `join_through`
* DSL level validations! Things like includes validating that their chain exists. All DSL structs should be strictly validated when they are created.
* Especially at compile time, we should *never* ignore or skip invalid options. If an option is present and invalid, an error is raised.
* break up the `Ash` module
* Wire up/formalize the error handling
* Ensure that errors are properly propagated up from the data_layer behaviour, and every operation is allowed to fail
* figure out the ecto schema warning
* all actions need to be performed in a transaction
* document authorization thoroughly. *batch* (default) checks need to return a list of `ids` for which the check passed.
* So many parts of the system are reliant on things having an `id` key explicitly. THis will need to be addressed some day, and will be a huge pain in the ass
* Validate that the user resource has a get action
* `params` should be solidified. Perhaps as a struct. Or perhaps just renamed to `action_params` where it is used.
* Since actions contain rules now, consider making it possible to list each action as its own `do` block, with an internal DSL for configuring the action. (overkill?)
* Validate rules at creation
* Maybe fix the crappy parts of optimal and bring it in for opts validation?
* The ecto internals that live on structs are going to cause problems w/ pluggability of backends, like the `%Ecto.Association.NotLoaded{}`. That backend may need to scrub the ecto specifics off of those structs.
* Add a mixin compatibility checker framework, to allow for mix_ins to declare what features they do/don't support.
  * Have ecto types ask the data layer about the kinds of filtering they can do, and that kind of thing.
* Make `Ash.Type` that is a superset of things like `Ecto.Type`. If we bring in ecto database-less(looking like more and more of a good idea to me) that kind of thing gets easier and we can potentially lean on ecto for type validations well.
* use a process to hold constructed DSL state, and then coalesce it all at the end. This can clean things up, and also allow us to potentially eliminate the registry. This will probably go hand in hand w/ the "capabilities" layer, where the DSL confirms that your data layer is capable of performing everything that your DSL declares
* make ets dep optional
* Bake in descriptions to the DSL
* Contributor guideline and code of conduct
* Do branch analysis of each record after authorizing it, in authorizer
* consider moving `type` and `name` for resources out into json api (or perhaps just `name`) since only json api uses that
* When we support embedding, figure out `embed_as` on `Ash.Type`
* Consider allowing declaring a data layer at the *api* level, or overriding the resource's data layer at the *api* level
* Since actions can return multiple errors, we need a testing utility to unwrap/assert on them
* Flesh out relationship options
* Flesh out field options (sortable, filterable, other behavior?)

