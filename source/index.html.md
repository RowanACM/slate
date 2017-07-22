---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
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

> The above command returns JSON structured like this:

```json
{
  "status": "OK",
  "message": "You signed up for committees [general, app]"
}
```


<aside class="warning">You can find the full list of committee names at the bottom of this page</aside>

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


### HTTP Request

`DELETE https://rowanacm.org/prod/get-user-info`

### URL Parameters

Parameter | Required | Description
--------- | ----------- | -------------
token | true | Your firebase login token

