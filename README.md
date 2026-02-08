# FeatureFlagAndRuntimeConfig

Feature flags are conditional code that lets developers turn features on or off based on whatever they want to display the users.

It provides benifits like A/B testing.

We can turn this on or off without deployement and test directly in production.

We can also segment our users based on different attributes.

Feature flags are used to also reduce the risk of deploying to production - <https://github.blog/engineering/infrastructure/ship-code-faster-safer-feature-flags/>

Runtime configs act as a way to inject/provide these values into the production application.'

## Who uses this system?

This system would be used by developers who would want to test different features for their application and also add/remove features when the application is already in production to avoid disruption of services to the user.

## What problem does it solve?

As mentioned in the previous answer and the benifits of feature files, it becomes clear on what problem does it solve.

## What must NEVER go wrong?

Some of the things I can think of to never go wrong would be:
- The runtime config should always have a value to the code using the config.
- The production application must not crash because of any error from our service.
- Our services must be up and running all the time and must never have mismatch to what the application is showing and we are trying to give as value.

## What happens if this service goes down?

There must atleast be a default value that is set to send back to the production website in case the service goes down and it should not be entirely dependent on the service.

In case the service goes down - the application should perform with all the features enabled that were set as default during production.


## Push vs Pull Model to be used for this?

The service we will create will use a push model since the user can toggle a feature on/off using our service and it pushes the value to the production application which changes it, using a pull model from the production application will hog the resources and make it heavy for the application to continuously asking for values from the service.

On second thoughts it can be a push model from the service side and a pull model from the application side, a stronger and final approach needs to be decided.

## Read heavy or write heavy?

The service we design would be read heavy since the application would be using:

```
if config["enable_new_checkout"] == true {
    // new logic
}
```

Hence, the application would be reading the values very frequently.

## Consistency requirement

The service must remain consistent with the application features to show.

Either the service will provide high consistency or eventual consistency, in case we provide high consistency then the service should be strong enough to be available all the time.


