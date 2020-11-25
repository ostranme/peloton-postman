# Peloton Postman :bicyclist:

> :warning: **NOTE:** :warning:
>
> This repo is purely a pet project to understand my own Peloton data and should NOT be considered official. It was more of an exercise to understand Peloton's APIs and to document my findings.

The Peloton Postman collection is a set of pre-configured REST API and GraphQL requests and environment that will make it easy for you to get started with the (unofficial/unsupported) Peloton APIs and try out API requests through the popular Postman REST client.

Please note: some URLs are privileged, meaning you must have a valid Peloton account to authenticate to obtain a session ID which then gets sent in future requests.

## Usage

1. Download or clone repository.
2. Import collections and environment json files into Postman (alternatively click the "Run in Postman" buttons next to each section).
3. Update `Peloton` environment with your user credentials and preferred variables.

### Configure Environment Variables

When you download and install the latest version of the Postman collections, you also download and import the respective environment along with the environment variables.

Once your environment is imported, next you need to set your Peloton account specific values.

Some of the important variables that you need to set are as follows:

| Environment Variable | Value                                                       |
| -------------------- | ----------------------------------------------------------- |
| base_url             | https://api.peloton.com                                     |
| graphql_url          | https://gql-graphql-gateway.prod.k8s.onepeloton.com/graphql |
| username_or_email    | YOUR_PELOTON_USERNAME_OR_EMAIL                              |
| password             | YOUR_PELOTON_PASSWORD                                       |

> **NOTE:** In order to get the postman requests to work, you must replace all instances of the {base_url}, {graphql}, {username_or_email}, and {password} variables within the collection and use your own Peloton credentials. The Peloton Postman collection will require a valid peloton_session_id Cookie to make some privileged API calls. Check out the Authentication section for more details.

## Authentication

The Peloton API uses session based authentication with cookies. The server will create a session for the user after the user logs in. The session id is then stored as your `peloton_session_id` cookie on the user’s browser. While the user stays logged in, the cookie would be sent along with every subsequent request.

Additionally you may need a `Peloton-Platform: web` request header for some requests (I still don't know why some routes require this and others don't).

## REST APIs

The collection contained in this repository are organized under this scheme:

- [REST APIs](#rest-apis)
  - [Auth API](#auth-api)
  - [eCommerce API](#ecommerce-api)
  - [Instructor API](#instructor-api)
  - [Ride / Class API](#ride-/-class-api)
  - [User API](#user-api)
  - [Workout API](#workout-api)

> :lock: = Privileged Endpoints

### Auth API

- **Login** - Create a valid user session with Peloton user credentials (username/password)
- **Logout** - Terminate a specific user session
- **Check Session** - Check current user session (based off `peloton_session_id` Cookie)

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/57328243f42c253c1048)

### eCommerce API

- **Peloton Plans** - Request a list of available Peloton plans (trials, memberships)
- **Peloton Stores** - Request a list of available Peloton stores
- **Peloton Bike Reviews** - Request Peloton bike reviews
- **Peloton Account Order History :lock:** - Request your Peloton user account order history
- **Peloton Account Payment Info :lock:** - Request your Peloton user account payment info details

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/dce5e57f8f2116d03e27)

### Instructor API

- **All Instructors** - Request all Peloton instructors
- **Instructor by Id** - Request Peloton instructor details by Id

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/ba7dc5dff85313e5c2bf)

### Ride / Class API

- **Ride Metadata Mappings** - Request ride metadata mappings details
- **Archived Rides** - Request archived rides
- **Live Rides** - Request live rides
- **Ride by Id** - Request ride info by id
- **Ride Details** - Request ride details
- **Ride Filters** - Request ride filters
- **Ride Recent Following Workouts :lock:** - Request recent following users
- **Class Categories** - Request Peloton class categories
- **Favorite Class :lock:** - Favorite/bookmark a Peloton class
- **Unfavorite Class :lock:** - Unfavorite/unbookmark a Peloton class
- **Reserve Live Class :lock:** - Reserve an upcoming live Peloton class
- **Unreserve Live Class :lock:** - Remove reservation from an upcoming live Peloton class

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/7fbe9df35c2e20de26d6)

### User API

- **Me :lock:** - Request the current logged in user details
- **User by Id** - Request user details by user id
- **User by Username** - Request user details by Peloton username
- **User Workouts :lock:** - Request a list of a user's workouts
- **User Workout History :lock:** - Download your workout history in CSV format
- **User Overview :lock:** - Request user workout overview details (workout counts, achievements, personal records, steaks)
- **User Subscriptions :lock:** - Request your Peloton user account subscription details
- **User Subscription Transactions :lock:** - Request your Peloton user subscription transactions (billing)
- **User Achievements :lock:** - Request user achievement details
- **User Challenges :lock:** - Request user challenges details (past, current, upcoming)
- **User Followers :lock:** - Request user followers details
- **User Following :lock:** - Request user following details
- **User Search :lock:** - Search for Peloton users by username
- **User Settings :lock:** - Request user settings details
- **User Referral History :lock:** - Request user referral history
- **User Calendar Activity :lock:** - Request user calendar activity
- **User Relationships :lock:** - Follow/Unfollow a specific Peloton user by id
- **Update User Profile :lock:** - Update your Peloton user profile info
- **Update User Settings :lock:** - Update your Peloton user settings info (Privacy, Notifications, Connected Networks, Display Preferences, Content Preferences)

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/9a2a890f2070928e52db)

### Workout API

- **User Workouts :lock:** - Request a list of a user's workouts
- **Workout by Id** - Request workout details by id
- **Workout Performance Graph** - Request workout performance graph details (summaries, metrics)
- **Delete Workout :lock:** - Remove/delete Peloton workout from user's workout history

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/f27132f0c9e8ddffa725)

## Classes vs Rides vs Workouts

1. **Classes**, no matter the workout type (strength, yoga, cycling, etc.) seem to be considered a "ride" (Ex: Strength, Yoga, Meditation are still consider rides when using the `/rides` resource).
2. **Rides** are the classes that you can take with Peloton, not necessarily what you have taken/completed.
3. **Workouts** are classes/rides you have taken/completed.

## GraphQL API

Peloton appears to use GraphQL to support their tags functionality. Below are the available queries using the GraphQL API endpoint.

[![Run in Postman](https://run.pstmn.io/button.svg)](https://app.getpostman.com/run-collection/74337aa08297636d2466)

The GraphQL endpoint still requires an authenticated user to login to produce a `peloton_session_id` Cookie.

- [GraphQL APIs](#graphql-api)
  - [Querying Tags](#querying-tags)
  - [Mutations](#mutations)
  - [Pagination](#graphql-pagination)

> :lock: = Privileged Queries / Mutations

### Querying Tags

Perform read operations and retrieve data on Peloton tags (Ex: #PelotonDads, #PelotonDevs).

- **MyTags :lock:** - Request your tags
- **PrimaryTag :lock:** - Request your primary tag
- **SearchTag :lock:** - Search for tags
- **TagBrowseCategory :lock:** - Request tag info by category
- **TagBrowseCategoryDisplayNames :lock:** - Request tag category display names
- **TagDetail :lock:** - Request tag details

### Mutations

Perform mutations to change data on Peloton tags.

- **AddTagToUser :lock:** - Add Peloton tag to your user account
- **RemoveTagFromUser :lock:** - Remove tag from your user account
- **SetTagAsPrimary :lock:** - Set tag as your primary tag

### QraphQL Pagination

If a resource has a lot of data, more than likely the response will have a `pageInfo` object that contains metadata you'll need to continue paginating:

- `endCursor` - returns a non-null opaque string as a marker to the last items in the collection of results returned from the query.
- `hasNextPage` boolean field to help identify if there are more pages/results to query from the collection.

```json
"pageInfo": {
    "endCursor": "MTk==",
    "hasNextPage": true
}
```

On the subsequent request you can pass a graphql `after` variable/cursor argument to tell the API, “here’s where I left off last time, get me the next X number of items."

```json
{
  "after": "MTk=="
}
```
