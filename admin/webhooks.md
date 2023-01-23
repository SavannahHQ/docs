# Webhooks

> WARNING: Webhooks are a beta feature and subject to change. To start using them contact info@savannahhq.com

Webhooks allow you to send data to an external system whenever something changes within Savannah.

## Events

Every event is given a heirarchical name that identifies the reason for the event and the data that will be associated with it.

When subscribing to events you can subscribe to the full event name (such as `Member.changed`) or all events in a heirarchy (such as `Member.*`).

### Member

Member events are triggered whenever a Member profile is created, modified, or deleted. 
The event name will be `Member.created`, `Member.changed` or `Member.deleted` respectively.

The payload for this event will always be the Member's profile data:
```
{
    "event": {
        "id": "0b221da1-89b8-4b17-95dd-bdd91398a364", 
        "hook": "3350fc24-ebb4-4d27-a9e4-2ca33994b092", 
        "name": "Member.updated", 
        "target": "https://yourhostname.com/webhook_handler", 
        "signature": "3zEgRNAs/KsbPP1VrVUhZwCWBvntmMGVtgKDYGYZXKU="
    }, 
    "data": {
        "id": 19413, 
        "name": "Example User", 
        "email": "example@test.com", 
        "role": "Community", 
        "company": "Faceless Corp", 
        "tags": ["customer", "ambassador"]
    }
}
```

### EngagementLevel

EngagementLevel events are triggered whenever a Member's engagement level changes is a project.
Event names will be either `EngagementLevel.up` or `EngagementLevel.down` depending on whether there has been an increase or decrease in the member's engagement level in that project.

The payload for this event will contain the project, new and previous levels:
```
{
    "event": {
        "id": "29011008-b537-4951-a84c-b4f9c3d1ce4c", 
        "hook": "38cc41fa-9863-426a-afcc-117d26dc6d7c", 
        "name": "EngagementLevel.up", 
        "target": "https://yourhostname.com/webhook_handler", 
        "signature": "W+A7enQIGBAJ013a9yMf49OTxuWcHJoNjQaE6OIpFck="
    }, 
    "data": {
        "project": {
            "id": 45, 
            "name": "Telegraf", 
            "default_project": false
        }, 
        "member": {
            "id": 19413, 
            "name": "Example User", 
            "email": "example@test.com", 
            "role": "Community", 
            "company": "Faceless Corp", 
            "tags": ["customer", "ambassador"]
        }, 
        "level": "Contributor", 
        "previously": "Participant"
    }
}
```

## Authentication

You can verify that an event is coming from Savannah CRM using the `signature` data provided in every webhook call. 

The signature an HMAC digest of the `data` portion of the JSON payload, encoded as a string, and your webhook's secret key.