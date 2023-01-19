# Sources

Savannah CRM is a data-driven platform, using information from your community to power insights and recommendations for Community Managers. To get this data from your community you will need to connect it to one or more `Sources` where your community activity happens.

Savannah comes with support for a number of popular community platforms which can be quickly and easily added as a source. For everything else, there's an [API](api.md) you can use to make that connection yourself.

## Built-in connectors

| Source                             | What is reads |
|:-----------------------------------|:------------------|
| [Slack](slack.md)                  | Chat activity in your Slack Channels |
| [Discourse](discourse.md)          | Topics and Posts in your Discourse Categories |
| [Discord](discord.md)              | Chat activity in your Discord Channels |
| [Github](github.md)                | Issues,Pull requests, and their comments |
| [Gitlab](gitlab.md)                | Issues, Merge Requests requests, and their comments |
| [Salesforce (SFDC)](salesforce.md) | Name and Account |
| [Stack Exchange](stackexchange.md) | Questions, Answers and Comments |
| [Blog](rss.md)                     | Articles and Comments in an RSS feed |


# Channels

Sources connect Savannah to your community platforms, but data is only imported from the `Channels` that you choose to track. This gives you full control over where Savannah is getting data about your community.

Each Source will provide you with a list of Available Channels, based on the kind of data that is available from that specific Source. You can track as many of as few channels as you like.

## Channel Tags

Each tracked Channel can optionally be given a Savannah `Tag`. If a Channel has a Tag associated with it, any `Contribution` made against that channel will automatically be given the same Tag. Otherwise Tags will only be assigned to Contributions based on keyword matching of their contents.