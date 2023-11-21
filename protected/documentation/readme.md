Todo:

# Subscriber Configuration

- allow additional service-configuration on the link between rules and subscribers
	- currently the subscriber _can_ be hard coupled to the signal type
	- that means if we want to do the same action in different contexts, we might need to duplicate quite a bit of configuration
	- we could however allow you to override (or append) to the configuration when coupling the subscriber to the rule

This makes the solution complexer however and it is not entirely clear if this will be necessary.
If so, we can still add this in the future.

# Signal Duplication

Sometimes the same signal can be sent multiple times before an action is taken.
We can allow signals to be triggered once triggering a breaker. It will only retrigger if the breaker is reset.
For example we could allow you to target an identifier within the signal (like exactly once) and make sure we only retrigger the signal if certain conditions are met.

Type id + the id should be sufficient to categorize a signal. The id can be a concatenated field (use eval again)
Ideally we can do a custom check? This would require a spec though..

# Signal metadata

We have added basic metadata like correlationId etc. Currently it can only be filled in by the one triggering the signal.
Perhaps we can extract such information from the signal itself via rules or subscribers?

# Properties

In a rule you can decide to extract some properties from a signal, this allows for later statistics to be drawn from the signals.
You can set a basic rule that extracts the properties and build child rules to actually notify if that is necessary.
The property key is repeated rather than foreign keyed to allow for easy removal of rule properties.

# Definitions

For different tenants/customers/... we might want to allow them to configure their own rules. We create the definitions to centralize the logic of the rule, allowing it to be applied multiple times in multiple contexts.
For example a base rule could be => tenantId == "..." with customer-defined child rules based on the definitions.

## Templates

Definitions are usually coupled to a data type (because so are rules). Templates are then a way to standardize the mapping to subscribers based on the given rule definition. It is again the idea to give customers a way to control this themselves without having to configure the nitty gritty details.
The customer can then say "if this occurs" (the definition), "then send a mail" (the template)

Both templates and definitions have translatable title fields