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