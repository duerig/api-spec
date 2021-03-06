---
title: "Channel Muting"
---

# Channel Muting

* TOC
{:toc}

## Get current user's muted Channels

Retrieve a list of the channels the current user has muted. A user cannot be [auto-subscribed](/docs/basics/messaging/#subscriptions) to muted channels.

This endpoint is **not** paginated and does **not** respond to the [general channel parameters](/docs/resources/channel/#general-parameters).

<%= migration_warning ['response_envelope'] %>

<%= endpoint "GET", "users/me/channels/muted", "User", "public_messages</code> or <code>messages"%>

#### Example

> GET https://alpha-api.app.net/stream/0/users/me/channels/muted

~~~ js
{
    "data": [
        {
            "counts": {
                "messages": 42
            },
            "has_unread": true,
            "id": "1",
            "owner": {
                ...
            },
            "readers": {
                "any_user": false,
                "immutable": true,
                "public": false,
                "user_ids": [],
                "you": true
            },
            "type": "net.app.core.pm",
            "writers": {
                "any_user": false,
                "immutable": true,
                "public": false,
                "user_ids": [
                    "1",
                ],
                "you": true
            },
            "you_can_edit": false,
            "you_muted": true,
            "you_subscribed": true
        },
        ...
    ],
    "meta": {
        "code": 200,
    }
}
~~~

## Mute a Channel

Mute a Channel. If a user doesn't want to see a channel until there is a new message, they should [unsubscribe from the channel](/docs/resources/channel/subscriptions/#unsubscribe-from-a-channel) instead of muting it. If a user mutes a channel, they will automatically be unsubscribed from it and cannot be [auto-subscribed](/docs/basics/messaging/#subscriptions) to it.

<%= general_params_note_for "channel" %>

<%= migration_warning ['response_envelope'] %>

<%= endpoint "POST", "channels/[channel_id]/mute", "User", "public_messages</code> or <code>messages"%>

<%= url_params [
    ["channel_id", "The id of the Channel to mute."]
]%>

#### Example

> POST https://alpha-api.app.net/stream/0/channels/1/mute

~~~ js
{
    "data": {
        "counts": {
            "messages": 42
        },
        "has_unread": false,
        "id": "1",
        "owner": {
            ...
        },
        "readers": {
            "any_user": false,
            "immutable": false,
            "public": false,
            "user_ids": [],
            "you": true
        },
        "type": "com.example",
        "writers": {
            "any_user": false,
            "immutable": false,
            "public": false,
            "user_ids": [
                "1"
            ],
            "you": true
        },
        "you_can_edit": true,
        "you_muted": true,
        "you_subscribed": false
    },
    "meta": {
        "code": 200
    }
}
~~~

## Unmute a Channel

Unmute a Channel. This allows you to be resubscribed to the channel (but it does not happen automatically).

<%= general_params_note_for "channel" %>

<%= migration_warning ['response_envelope'] %>

<%= endpoint "DELETE", "channels/[channel_id]/mute", "User", "public_messages</code> or <code>messages"%>

<%= url_params [
    ["channel_id", "The id of the Channel to unmute."]
]%>

#### Example

> DELETE https://alpha-api.app.net/stream/0/channels/1/mute

~~~ js
{
    "data": {
        "counts": {
            "messages": 42
        },
        "has_unread": false,
        "id": "1",
        "owner": {
            ...
        },
        "readers": {
            "any_user": false,
            "immutable": false,
            "public": false,
            "user_ids": [],
            "you": true
        },
        "type": "com.example",
        "writers": {
            "any_user": false,
            "immutable": false,
            "public": false,
            "user_ids": [
                "1"
            ],
            "you": true
        },
        "you_can_edit": true,
        "you_muted": false,
        "you_subscribed": false
    },
    "meta": {
        "code": 200
    }
}
~~~