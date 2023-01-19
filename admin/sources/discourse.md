# Discourse Source

In order to add your Discourse instance as a source in Savannah you must first create an API key using the Discourse admin. If you do not have administrative access to your Discourse, you will need to request that this API key be created for you.

When creating an API key you will be asked if you want to create an `All Users` key or a `Single User` key. In order to track any available categories in Savannah you will need to use the `All Users` key.

Once you have an API key you can add your Discourse source. If you created an `All Users` API key, use `system` for the Discourse Username, otherwise use the username of the user the `Single User` API key was created for.

![Add Discourse Source](/images/sources/AddDiscourse.png)

## Channels

You will be able to track any of your public Discourse categories as a channel in Savannah, and any private categories that your API key has access to.

> If you use sub-categories in Discourse, these must be tracked separately from the parent category, due to the way Discourse exposes them in their API.