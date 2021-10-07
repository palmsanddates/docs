<!-- logo -->

<p align="center">
  <img width="300" src="./logo.png">
</p>

We’re building this product for students and event coordinators, which includes residential assistants and university staff for student life.

## Table of Contents

- [Make Commands](#make-commands)
- [Required Software](#required-software)
- [How to Run](#how-to-run)
- [API Documentation](#api-documentation)
- [Running Tests](#running-tests)

## Makefile Commands

`make build`: Build development server without running the server

`make start`: Start development server at port `5000` for backend and `3000` for frontend.

`make stop`: Stop the running server

`make rm`: Remove all stopped running containers and unused images.

`make rmi`: Remove the the pnd-backend && pnd-frontend images.

## Required Software

- [Docker](https://docs.docker.com/get-docker/)
- [docker-comopse](https://docs.docker.com/compose/install/)

## How to Run

Clone the repo

```zsh
git clone https://github.com/palmsanddates/palmsanddates
```

cd into the directory backend and frontend, and rename `.env.sample` to `.env`

```zsh
cd backend
mv .env.sample .env
cd ..
cd frontend
mv .env.sample .env
```

- To start : Please make a branch out of `development` branch.

  ```terminal command
  git checkout -b yourBranchName development
  ```

- To merge branch: Please have your code reviewed by a teammate and merge to the `development` branch. Notify the git master to merge the update to `main branch`

To start the program, just run `make build` then `make start`.

To terminate the program, press the key `command + C` and run `make stop` in the terminal.

### Backend

**Running on <http://localhost:5000>**

If need to install any new library, make sure you run `make build` to create the most updated image. Below are the instructions:

``` Terminal Command
cd /backend
npm i <newLibrary>
cd .. 
make build
make start
```

### Frontend

**Running on <http://localhost:3000>**

If need to install any new library, make sure you run `make build` to create the most updated image. Below are the instructions:

``` Terminal Command
cd /frontend
npm i <newLibrary>
cd .. 
make build
make start
```

## API Documentation

Base URL

```http
https://api.palmsanddates.com
```

### Get All Events

#### Request

```http
GET https://api.palmsanddates.com/events
```

#### Response

Success status code: `200`

This route returns an array of ALL the event objects.

Example response:

```json
[
  {
    "name": "The POP-UP",
    "creator": "Lauran",
    "bio":"Join CAB at the annual pop-up for an evening filled with music painting, giveaways, food and other fun activities! Supplies are limited. First-come, First-serve.",
    "location":"Anne Hathaway Lawn",
    "time":"Sept 24th 4:00-7PM",
    "department":"Campus Activities Board",
    "event_type":"Campus",
    "budget":"400",
    "expected_attendees":24,
    "flyer_img_url":"http://dummyimage.com/453x419.png/5fa2dd/ffffff",
    "rsvp_url":"www.the-pop-up.com/signup"
  },
  {
    "name": "BOB ROSS Paint Night",
    "creator": "Yin",
    "bio":"Come paint with Student Honors Board from 6:30 to 10PM in the San Marcos Art Studios! Follow a guided Bob Ross video or come up with your vision for your painting and write a thank you card for our healthcare workers. All students welcome!",
    "location":"San Marcos Art Studios",
    "time":"Sept 27th 6:30-10:00PM",
    "department":"Student Honors Board",
    "event_type":"Campus",
    "budget":"100.0",
    "expected_attendees":24,
    "flyer_img_url":"http://dummyimage.com/453x419.png/5fa2dd/ffffff",
    "rsvp_url":"www.bobrosspaintnight.com/signup"
  },
  ...
]
```

Types:

- name: String
- creator: String
- bio: String
- location: String
- time: Datetime
- event_type: Enum
- budget: Float
- expected_attendees: Integer
- flyer_img_url: String
- rsvp_url: String

Error status code: `500`

An unsuccessful request, for any reason (such as the database connection times out, or there's another server-side issue) will result in an error response:

```json
{
    "message": "Connection refused."
}
```

### Get One Events

#### Request

```http
GET https://api.palmsanddates.com/events/:id
```

#### Response

Success status code: `200`

This route should return a single event object by finding the ID in the database

Example response:

```json
[
  {
    "name": "The POP-UP",
    "creator": "Lauran",
    "bio":"Join CAB at the annual pop-up for an evening filled with music painting, giveaways, food and other fun activities! Supplies are limited. First-come, First-serve.",
    "location":"Anne Hathaway Lawn",
    "time":"Sept 24th 4:00-7PM",
    "department":"Campus Activities Board",
    "event_type":"Campus",
    "budget":"400",
    "expected_attendees":24,
    "flyer_img_url":"http://dummyimage.com/453x419.png/5fa2dd/ffffff",
    "rsvp_url":"www.the-pop-up.com/signup"
  }
]
```

Types:

- name: String
- creator: String
- bio: String
- location: String
- time: Datetime
- event_type: Enum
- budget: Float
- expected_attendees: Integer
- flyer_img_url: String
- rsvp_url: String

Error status code: `500`

An unsuccessful request, for any reason (such as the database connection times out, or there's another server-side issue) will result in an error response:

```json
{
    "message": "Connection refused."
}
```

### Create One Event

#### Request

```http
POST https://api.palmsanddates.com/events
```

This should have a request body with the required data to create an event in the database, this can only be done by admin.

Example request body:

```json
[
  {
    "name": "The POP-UP",
    "creator": "Lauran",
    "bio":"Join CAB at the annual pop-up for an evening filled with music painting, giveaways, food and other fun activities! Supplies are limited. First-come, First-serve.",
    "location":"Anne Hathaway Lawn",
    "time":"Sept 24th 4:00-7PM",
    "department":"Campus Activities Board",
    "event_type":"Campus",
    "budget":"400",
    "expected_attendees":24,
    "flyer_img_url":"http://dummyimage.com/453x419.png/5fa2dd/ffffff",
    "rsvp_url":"www.the-pop-up.com/signup"
  }
]
```

Types:

- name: String
- creator: String
- bio: String
- location: String
- time: Datetime
- event_type: Enum
- budget: Float
- expected_attendees: Integer
- flyer_img_url: String
- rsvp_url: String

#### Response

Success status code: `200`

A successful response will send a success message and your new event object.

Example reponse:

```json
  "message": "Event Created successfully!",
  {
    "_id":"615bbaedfc13ae31b4000064",
    "name": "The POP-UP",
    "creator": "Lauran",
    "bio":"Join CAB at the annual pop-up for an evening filled with music painting, giveaways, food and other fun activities! Supplies are limited. First-come, First-serve.",
    "location":"Anne Hathaway Lawn",
    "time":"Sept 24th 4:00-7PM",
    "department":"Campus Activities Board",
    "event_type":"Campus",
    "budget":"400",
    "expected_attendees":24,
    "flyer_img_url":"http://dummyimage.com/453x419.png/5fa2dd/ffffff",
    "rsvp_url":"www.the-pop-up.com/signup"
  }

```

Types:

- message: String
- event: Object
  - _id: String
  - name: String
  - creator: String
  - bio: String
  - location: String
  - time: Datetime
  - event_type: Enum
  - budget: Float
  - expected_attendees: Integer
  - flyer_img_url: String
  - rsvp_url: String

Error status code: `500`

In the event that there is another error due to a failure on the server side, a status code of 500 will be returned, along with a message stating the error.

Example 500 error message:

```json
{
    "err": "[error] 29#29: *17 upstream timed out (110: Operation timed out) while reading response header from upstream, client: 172.18.0.1, server: stockstalker.tk"
}
```

### Update One Event

#### Request

```http
PATCH https://api.palmsanddates.com/events/:id
```

This should update the event with whatever the user provides in the request body (it shouldn't be ALL the data) by fetching the id and manipulating it then saving in db.

Example request body:

```json
[
  {
    "name": "The POP-UP",
    "creator": "Lauran",
    "bio":"Join CAB at the annual pop-up for an evening filled with music painting, giveaways, food and other fun activities! Supplies are limited. First-come, First-serve.",
    "location":"Anne Hathaway Lawn",
    "time":"Sept 24th 4:00-7PM",
    "department":"Campus Activities Board",
    "event_type":"Campus",
    "budget":"400",
    "expected_attendees":24,
    "flyer_img_url":"http://dummyimage.com/453x419.png/5fa2dd/ffffff",
    "rsvp_url":"www.the-pop-up.com/signup"
  }
]
```

Types:

- name: String
- creator: String
- bio: String
- location: String
- time: Datetime
- event_type: Enum
- budget: Float
- expected_attendees: Integer
- flyer_img_url: String
- rsvp_url: String

#### Response

Success status code: `200`

A successful response will send a success message and your new event object.

Example reponse:

```json
  "message": "Event updated successfully!",
  {
    "_id":"615bbaedfc13ae31b4000064",
    "name": "The POP-UP",
    "creator": "Lauran",
    "bio":"Join CAB at the annual pop-up for an evening filled with music painting, giveaways, food and other fun activities! Supplies are limited. First-come, First-serve.",
    "location":"Anne Hathaway Lawn",
    "time":"Sept 24th 4:00-7PM",
    "department":"Campus Activities Board",
    "event_type":"Campus",
    "budget":"400",
    "expected_attendees":24,
    "flyer_img_url":"http://dummyimage.com/453x419.png/5fa2dd/ffffff",
    "rsvp_url":"www.the-pop-up.com/signup"
  }

```

Types:

- message: String
- event: Object
  - _id: String
  - name: String
  - creator: String
  - bio: String
  - location: String
  - time: Datetime
  - event_type: Enum
  - budget: Float
  - expected_attendees: Integer
  - flyer_img_url: String
  - rsvp_url: String

Error status code: `404`

An unsuccessful validation (for example, deleting a event that doesn't exist) will return a 404 status code for "resource not found". An example error response:

```json
{
    "message": "Cannot Find The event"
}
```

Error status code: `500`

In the event that there is another error due to a failure on the server side, a status code of 500 will be returned, along with a message stating the error.

Example 500 error message:

```json
{
    "err": "[error] upstream timed out (110: Operation timed out) while reading response header from upstream"
}
```

### Delete One Event

#### Request

```http
PATCH https://api.palmsanddates.com/events/:id
```

This should delete the event with whatever the user provides in the request body (it shouldn't be ALL the data). You should fetch the event object from the database and delete it.

#### Response

Success status code: `200`

Successful responses will return a message.

```json
{
  "message":"The event has been deleted successfully!"
}
  
Types:
  - message: String

Error status code: `404`

An unsuccessful validation (for example, deleting a event that doesn't exist) will return a 404 status code for "resource not found". An example error response:

```json
{
    "message": "Cannot Find The event"
}
```

### Signing In Admin

This route should get a request body that has the email and password, it then creates a JWT token that expires in a month and it returns it.

#### Request

```html
POST https://api.palmsanddates.com/events/:id
```

The request expects in the body a username and password.

Example request body:

```json
{
    "username": "newuser",
    "password": "password"
}
```

#### Response

Success status code: `200`

A successful response will send a success message to verify your user is now signed in.

Example response:

```json
{
    "message": "Sign in successful!",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6IkZBS0VVU0VSIiwidXNlcklkIjoiNjA1M2JlZTg5YzU3MTcwMTQyMDExYzM2IiwiaWF0IjoxNjE2MTAxMTIzLCJleHAiOjE2MTYxMDQ3MjN9.IzWXlrFS7mQqR652keVEHnR4ayspk5yyyMjRpYTY7gw"
}
```

Types:

- message: String
- token: String

Cannot find user error status code: `401`

In the event that the username entered does not correspond to an existing user, a status code of 401 will be returned, along with an error message like the following:

```json
{
    "message": "User does not exist!"
}
```

Error status code: `500`

In the event that there is another error due to a failure on the server side, a status code of 500 will be returned, along with a message stating the error.

Example 500 error message:

```json
{
    "err": "[error] upstream timed out (110: Operation timed out) while reading response header from upstream"
}
```
