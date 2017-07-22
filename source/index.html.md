---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Rowan ACM API! You can use our API to access information about ACM.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

Most resources require an API key. We are using the Firebase Auth Tokens. You can find more information on the [firebase documentation](https://firebase.google.com/docs/auth/admin/verify-id-tokens#retrieve_id_tokens_on_clients)

<aside class="notice">
We plan on converting to standard API Keys in the future. If you want to help, let us know!
</aside>

# Methods

## Sign in to the meeting

> Returns JSON structured like this:

```json
[
  {
    "message": "You signed in to the meeting",
    "status": "OK",
    "response_code": 200
  }
]
```

You can only sign in while the meeting is in progress

### HTTP Request

`GET http://api.rowanacm.org/prod/sign-in`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
token | true | Your Firebase auth token


<aside class="warning">
Remember — your auth token is different than your uid
</aside>

## Choose/change your committee

Don't like your committee? No problem

> The above command returns JSON structured like this:

```json
{
  "status": "OK",
  "message": "You signed up for committees [general, app]"
}
```

The committee names are general, app, ai, web, robotics, and game.


<aside class="notice">If you want to leave a committee without choosing a new one, set your committee to general</aside>

### HTTP Request

`GET http://api.rowanacm.org/prod/set-committees`

### URL Parameters

Parameter | Required | Description
--------- | ----------- | ------------
token | true | Your firebase auth token
committees | true | A comma separated list of committee names

## Get user info

> The above command returns JSON structured like this:

```json
{
    "phone_number": null,
    "uid": "abc123",
    "member_since": "September 2016",
    "committee_string": "App Committee",
    "profile_picture": "https://avatars.slack-edge.com/mypicture.jpg",
    "is_admin": false,
    "github_username": "JohnSmith",
    "committee_list": [
        "app"
    ],
    "name": "John Smith",
    "slack_username": "johnsmith",
    "on_slack": true,
    "is_eboard": false,
    "todo_list": [
        {
            "text": "Attend your first meeting",
            "completed": true
        },
        {
            "text": "Sign in to the meeting",
            "completed": true
        },
        {
            "text": "Sign up for Slack",
            "completed": true
        },
        {
            "text": "Choose a committee",
            "completed": true
        },
        {
            "text": "Join our Github organization",
            "completed": true
        }
    ],
    "meeting_count": 10,
    "on_github": true,
    "rowan_email": "smithj0@students.rowan.edu"
}
```

<aside class="notice">We are not currently collecting your phone number. The field is there if we decide to use it in the future.</aside>



### HTTP Request

`DELETE https://rowanacm.org/prod/get-user-info`

### URL Parameters

Parameter | Required | Description
--------- | ----------- | -------------
token | true | Your firebase login token


## Get announcements

> Returns JSON structured like this:

```json
[
    {
        "snippet": "Considering that it's July, I'd doubt you thought that was was a meeting today. But if you weren't sure, there's not.",
        "timestamp": 1500647954,
        "committee_id": "general",
        "committee": "General",
        "author": "Tyler",
        "url": null,
        "text": "Considering that it's July, I'd doubt you thought that was was a meeting today. But if you weren't sure, there's not.",
        "title": "No meeting today",
        "icon": "https://firebasestorage.googleapis.com/myimage.png"
    },
    {
        "snippet": "Hey everyone, I just wanted to give everyone a heads up that back to the boro applications are due April 9th",
        "timestamp": 1491426391,
        "committee_id": "robotics",
        "committee": "Robotics Committee",
        "author": "John",
        "url": null,
        "text": "Hey everyone, I just wanted to give everyone a heads up that back to the boro applications are due April 9th",
        "title": "Back To The Boro Reminder",
        "icon": "https://firebasestorage.googleapis.com/myimage.png"
    },
    {
        "snippet": "We just passed 100 followers on Twitter! Unfortunately that's in base 2. Help us get up to 1000 by following us @RowanACM",
        "timestamp": 1487393994,
        "committee_id": "general",
        "committee": "General",
        "author": null,
        "url": "https://twitter.com/rowanacm",
        "text": "We just passed 100 followers on Twitter! Unfortunately that's in base 2. Help us get up to 1000 by following us @RowanACM",
        "title": "Follow @RowanACM on Twitter!",
        "icon": "https://firebasestorage.googleapis.com/myimage.png"
    }
]
```

Get a list of ACM announcements sorted in chronological order

### HTTP Request

`GET http://api.rowanacm.org/prod/get-announcements`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
limit | false | Limit the number of responses (COMING SOON)
filter | false | Filter announcements based on committee (COMING SOON)



## Post announcements

> Returns JSON structured like this:

```json
{
  "status": "OK",
  "message": "Announcement posted"
}
```

You must be an admin to post an announcement

### HTTP Request

`GET http://api.rowanacm.org/prod/post-announcement`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
token | true | Firebase auth token
title | true | Title of the announcement
body | true | Announcement text
committee | false | Default: General
also_post_on_slack | false | Default: False
