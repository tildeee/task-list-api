# Wave 5: Creating a Second Model

## Goal

Our task list API should be able to work with an entity called `Goal`.

Goals are entities that describe a task a user wants to complete. They contain a:

- title to name the goal
- description to hold details about the goal

Our goal for this wave is to be able to create, read, update, and delete different goals.

# Requirements

## Goal Model

There should be a `Goal` model that lives in `app/models/goal.py`.

Goals should contain these attributes. Feel free to change the name of the `goal_id` column if you would like. **The tests require the title column to be named exactly** as `title`.

- `goal_id`: a primary key for each goal
- `title`: text to name the goal

### Tips

- Don't forget to run:
  - `flask db migrate` every time there's a change in models, in order to generate migrations
  - `flask db upgrade` to run all generated migrations

## CRUD for Goals

The following are required routes for wave 5. Feel free to implement the routes in any order within this wave.

### Tips

- Pay attention to the exact shape of the expected JSON. Double-check nested data structures and the names of the keys for any mispellings.
- Use the tests in `tests/test_wave_05.py` to guide your implementation.
- You may feel that there are missing tests and missing edge cases considered in this wave. This is intentional.
  - You have fulfilled wave 5 requirements if all of the wave 5 tests pass.
  - You are free to add additional features, as long as the wave 5 tests still pass. However, we recommend that you consider the future waves, first.
- Some tests use a fixture named `one_goal` that is defined in `tests/conftest.py`. This fixture saves a specific goal to the test database.

### Create a Goal: Valid Goal

As a client, I want to be able to make a `POST` request to `/goals` with the following HTTP request body

```json
{
  "title": "My New Goal"
}
```

and get this response:

`201 CREATED`

```json
{
  "goal": {
    "id": 1,
    "title": "My New Goal"
  }
}
```

so that I know I successfully created a goal that is saved in the database.

### Get Goals: Getting Saved Goals

As a client, I want to be able to make a `GET` request to `/goals` when there is at least one saved goal and get this response:

`200 OK`

```json
[
  {
    "id": 1,
    "title": "Example Goal Title 1"
  },
  {
    "id": 2,
    "title": "Example Goal Title 2"
  }
]
```

### Get Goals: No Saved Goals

As a client, I want to be able to make a `GET` request to `/goals` when there are zero saved goals and get this response:

`200 OK`

```json
[]
```

### Get One Goal: One Saved Goal

As a client, I want to be able to make a `GET` request to `/goals/1` when there is at least one saved goal and get this response:

`200 OK`

```json
{
  "goal": {
    "id": 1,
    "title": "Build a habit of going outside daily"
  }
}
```

### Get One Goal: No Matching Goal

As a client, I want to be able to make a `GET` request to `/goals/1` when there are no matching goals and get this response:

`404 Not Found`

No response body.

### Update Goal

As a client, I want to be able to make a `PUT` request to `/goals/1` when there is at least one saved goal with this request body:

```json
{
  "title": "Updated Goal Title"
}
```

and get this response:

`200 OK`

```json
{
  "goal": {
    "id": 1,
    "title": "Updated Goal Title"
  }
}
```

### Update Goal: No Matching Goal

As a client, I want to be able to make a `PUT` request to `/goals/1` when there are no matching goals with this request body:

```json
{
  "title": "Updated Goal Title"
}
```

and get this response:

`404 Not Found`

No response body

### Delete Goal: Deleting a Goal

As a client, I want to be able to make a `DELETE` request to `/goals/1` when there is at least one saved goal and get this response:

`200 OK`

```json
{
  "details": "Goal 1 \"Build a habit of going outside daily\" successfully deleted"
}
```

### Delete Goal: No Matching Goal

As a client, I want to be able to make a `DELETE` request to `/goals/1` when there are no matching goals and get this response:

`404 Not Found`

No response body.

### Create a Goal: Invalid Goal With Missing Title

As a client, I want to be able to make a `POST` request to `/goals` with the following HTTP request body

```json
{}
```

and get this response:

`400 Bad Request`

```json
{
  "details": "Invalid data"
}
```

so that I know I did not create a Goal that is saved in the database.
