# API Integration

While Savannah provides a number of built-in data sources, your community will likey exist and be active in some systems that it doesn't know about. In these cases Savannah provides an `API Integration` Source type that will enable you to push Member and Conversation data directly into your Savannah community.

## Create an Integration Source

All data imported into Savannah is associated with a `Source` object, and API integrations are no different. In order to add your external system to Savannah you must first create an `API Integration` Source, in the same way as you create other sources.

![Add API Integration Source](./AddSourceMenu.png) ![Add API Integration Source](./AddSourceForm.png)

Your `Source` will be given a unique authorization token that you will use when making calls to the Savannah API. Because each token is associated with a `Source`, any data added to Savannah using that token will be associated with that `Source`.

![Source with Token](./APISourceToken.png)

## API Basics

### Authorization

API calls will need to be authorized using the API token of your `Source`. This is done by placing it in an HTTP request header:

```
Authorization: token f32fde77-ebbb-4799-94f7-065846da88bf
```

### Timestamps

Timestamps will always use the format `YYYY-MM-DDThh:mm[:ss[.uuuuuu]][+HH:MM|-HH:MM|Z]`

### Origin IDs

Savannah's API doesn't expose internal IDs, instead it uses unique identifiers from your external system to lookup internal records. These are referred to as the `origin_id` of the record.

You will need to provide an ID for each `Identity` and `Conversation` that is unique to your system. These IDs should be unique to your integration source, but do not need to be globally unique for your community. For example, you can have an `Identity` with the id `testuser` in your integration source, and also a user with the same identity from a Slack or Github source. 

An `origin_id` can be any string up to 256 characters long. You can use internal ID numbers, unique names or URIs, as long at the resulting string is unique for that data type in your intergration source.

Merging multiple identities into the same `Member` can be done in Savannah the same way it is for non-API sources.

### Repeating API calls

Savannah's APIs are designed to be idempotent. That means that calling the same API with the same data multiple times will not create duplicate data.

As long as you use the same `origin_id` each time, subsequent calls will only update the existing data associated with that ID.

### Create rather than fail

Whenever an API call references an `origin_id` for a record that is not already in Savannah, a new record for that ID will be created with minimal information rather than causing the API call to fail with an error.

You will still need to make additional API calls to fill in the missing data for those newly created records, but you will not be required to do that beforehand.

# Identities

An `Identity` is what associates a `Member` of your community with a `Source`. Members can (and usually do) have more than one `Identity`.

The `Identity` API endpoint is:

```
https://savannahcrm.com/api/v1/identity/
```

![Create an Identity](./IdentityAPI.png)

You can create a new `Identity` by senting a POST message to the `Identity` endpoint. Creating an `Identiy` will also create a `Member` for that `Identity`

You may also set tags on a member by passing an array of tag names to the `tags` field. If a tag by a given name does not already exist, Savannah will automatically create one for you.

```
curl -X POST -d "@-" -H "Content-Type: application/json" -H "Authorization: token f32fde77-ebbb-4799-94f7-065846da88bf" https://savannahcrm.com/api/v1/identity/ <<EOF
{
    "origin_id": "test_user_id",
    "username": "test_user",
    "name": "Test User",
    "email": "test@example.com",
    "avatar": null,
    "tags": ["test", "foo"]
}
EOF
```

If a `Member` with the given `Identity` already exists, this call will update their information.

# Conversations

The `Conversation` API endpoint is:

```
https://savannahcrm.com/api/v1/conversation/
```

![Create a Conversation](./ConversationsAPI.png)

When creating a `Conversation` you will need to provide certain fields in the form of their respective `origin_id`. These records will be created in Savannah if they haven't already been added.

* `speaker`: The id of the person who posted the comment
* `channel`: The id of the channel (however your source defines them) that the conversation happened in
* `participants`: A list of ids for the people who were tagged, replied to, or otherwise were a participant in this conversation.
* `tags`: An array of tag names to be applied to this conversation. If a tag by a given name does not already exist, Savannah will automatically create one for you.

Savannah will create a `Connection` record between the `speaker` and any `particpants` in the conversation.

```
curl -X POST -d "@-" -H "Content-Type: application/json" -H "Authorization: token f32fde77-ebbb-4799-94f7-065846da88bf" https://savannahcrm.com/api/v1/conversation/ <<EOF
{
    "origin_id": "conversation_id",
    "speaker": "test_user",
    "channel": "example_channel",
    "timestamp": "2020-09-20T15:12:26",
    "content": "Some test conversation text",
    "location": "https://example.com/conversations/conversation_id/test_conversation",
    "participants": [
        "test_user_x"
    ],
    "tags": ["test", "foo"]
}
EOF
```

# Contributions

The `Contribution` API endpoint is:

```
https://savannahcrm.com/api/v1/contribution/
```

![Create a Contribution](./ContributionsAPI.png)

When creating a `Contribution` you will need to provide certain fields in the form of their respective `origin_id`. These records will be created in Savannah if they haven't already been added.

* `author`: The id of the person who made the contribution
* `channel`: The id of the channel (however your source defines them) that the contribution was made in

You must also provide a `contribution_type` string to that identifies the kind of contribution this is. This string does not need to be an `origin_id` from your source.

If the `Contribution` you area adding is associated with an existing `Conversation`, you can provide the `origin_id` of the `Conversation` as the `conversation` parameter, otherwise leave it as `null`.

```
curl -X POST -d "@-" -H "Content-Type: application/json" -H "Authorization: token f32fde77-ebbb-4799-94f7-065846da88bf" https://savannahcrm.com/api/v1/contribution/ <<EOF
{
    "origin_id": "contribution_id",
    "author": "test_user",
    "contribution_type": "API Push",
    "channel": "example_channel",
    "timestamp": "2020-10-02T15:12:26",
    "title": "Contribution via API",
    "location": "https://example.com/conversations/contribution_id/test_contribution",
    "conversation": "conversation_id"
}
```

# Events

The `Event` API endpoint is:

```
https://savannahcrm.com/api/v1/event/
```

![Create an Event](./EventsAPI.png)

When creating an `Event` you will need provide a `channel` under your your API Integration source where it will be listed. If a `channel` with the given name does not exist, Savannah will create one for you.

```
curl -X POST -d "@-" -H "Content-Type: application/json" -H "Authorization: token f32fde77-ebbb-4799-94f7-065846da88bf" https://savannahcrm.com/api/v1/event/ <<EOF
{
    "origin_id": "my-company-conference-2021",
    "channel": "DevConf",
    "start_timestamp": "2020-06-23T12:00:00",
    "end_timestamp": "2020-06-24T16:00:00",
    "title": "MyCompany DevConf 2020",
    "description": "Our 3rd annual developer conference",
    "location": "https://example.com/events/devconf/2021",
    "tag": "conference"
}
```

You may optionally pass a list of member `origin_id`s to this endpoint using the `attendees` property. This is useful if you have already added the members to Savannah and know the entire list of attendees when calling this endoint. 

However, more often than not you will want to create the `Event` record first, and then iteratively add each attendee with their full details. For this, use the `EventAttendance` endpoint below.

## Event Attendees

The `EventAttendance` API endpoint is:

```
https://savannahcrm.com/api/v1/event/{event_id}/attendee/
```

You can optionally add members as attendees of your event. The `EventAttendee` endpoint is identical to the `Identity` endpoint, except that members will be marked as having attended the event specified in the URL. Event attendance will set a Member's first and last seen dates the same way conversations and contributions will.

If a member with  a matching `origin_id` does not exist, Savannah will create one for you.


```
curl -X POST -d "@-" -H "Content-Type: application/json" -H "Authorization: token f32fde77-ebbb-4799-94f7-065846da88bf" https://savannahcrm.com/api/v1/event/my-company-conference-2021/attendee/ <<EOF
{
    "origin_id": "test_user_id",
    "username": "test_user",
    "name": "Test User",
    "email": "test@example.com",
    "avatar": null,
    "tags": ["test", "foo"]
}
EOF
```