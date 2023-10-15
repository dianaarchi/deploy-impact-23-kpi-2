# deploy-impact-23-kpi-2

## Getting Started

We are using PostgreSQL as Database. If you don't have it locally, please install it from https://www.postgresql.org/download/

### macOS

**In your Terminal**

`$ cd backend` Navigates to the Backend Directory

`$ python3 -m venv venv` Sets Up your Virtual Environment

`$ source venv/bin/activate` Activates your Virtual Environment

`$ pip install -r requirements.txt` Installs dependencies

`$ psql < seed.sql` Sets Up and Seeds your Database

`$ python3 app.py` Runs the server

## API Reference

#### Login User

```http
  POST /login
```

| JSON             | Type     | Description          | Response                                 |
| :--------------- | :------- | :------------------- | :--------------------------------------- |
| `email` Required | `string` | User's Email Address | User details as Dictionary and jwt token |

#### Logout User

```http
  POST /logout
```

| JSON | Type | Description        | Response        |
| :--- | :--- | :----------------- | --------------- |
| -    | -    | Revokes jwt token. | Success message |

#### Get User

```http
  GET /users/<int:user_id>
```

| Parameter     | Type  | Description | Response                               |
| :------------ | :---- | :---------- | :------------------------------------- |
| `id` Required | `int` | Id of user  | Details about the user as a dictionary |

#### Get Users

```http
  GET /users
```

| Parameter | Type | Description   | Response           |
| :-------- | :--- | :------------ | :----------------- |
| -         | -    | Get all users | List of all users. |

#### Get Circle

```http
  GET /circles/<int:circle_id>
```

| Parameter | Type  | Description                             | Response                               |
| :-------- | :---- | :-------------------------------------- | :------------------------------------- |
| `id`      | `int` | Fetches details about a specific circle | Details about a circle as a dictionary |

#### Add Circle

```http
  POST /circles
```

| JSON            | Type     | Description | Response        |
| :-------------- | :------- | :---------- | :-------------- |
| `name` Required | `string` | Name        | Success message |

#### Get Circles

```http
  GET /circles
```

| JSON | Type | Description               | Response                            |
| :--- | :--- | :------------------------ | :---------------------------------- |
| -    | -    | Get a list of all circles | A list of all circles as dictionary |

#### Add KPI

```http
  POST /kpis/add
```

| JSON                         | Type     | Description                    | Response        |
| :--------------------------- | :------- | :----------------------------- | :-------------- |
| `name` **Required**          | `string` | Name                           | Success Message |
| `circle_id` **Required**     | `int`    | circle ID                      |
| `periodicity` **Required**   | `enum`   | yearly, quarterly, monthly     |
| `unit` **Required**          | `enum`   | chf, percentage, amount, score |
| `initial_value` **Required** | `float`  | Starting Value                 |
| `target_value` **Required**  | `float`  | Value to Reach                 |
| `active`                     | bool     | true or false                  |

#### Edit KPI

```http
  PUT /kpis/<int:kpi_id>/edit
```

| JSON                         | Type     | Description                    | Response        |
| :--------------------------- | :------- | :----------------------------- | :-------------- |
| `name` **Required**          | `string` | Name                           | Success message |
| `circle_id` **Required**     | `int`    | circle ID - Parameter          |
| `periodicity` **Required**   | `enum`   | yearly, quarterly, monthly     |
| `unit` **Required**          | `enum`   | chf, percentage, amount, score |
| `initial_value` **Required** | `float`  | Starting Value                 |
| `target_value` **Required**  | `float`  | Value to Reach                 |
| `active`                     | `bool`   | True or False                  |

#### Get KPI

```http
  GET /kpis/<int:kpi_id>
```

| Parameter | Type  | Description     | Response                   |
| :-------- | :---- | :-------------- | :------------------------- |
| `id`      | `int` | Get Kpi details | Return KPI as a dictionary |

#### Get KPIs

```http
  GET /kpis
```

| Parameter | Type | Description             | Response                       |
| :-------- | :--- | :---------------------- | :----------------------------- |
| -         | -    | Get details about a KPI | List of all Kpis as dictionary |

#### Add a KPI Value

```http
  Post /kpi_values/add
```

| JSON                        | Type  | Description                          | Response        |
| :-------------------------- | :---- | :----------------------------------- | :-------------- |
| `user_id`                   | `int` | Retrieved from jwt token             | Success message |
| `kpi   _id` **Required**    | `int` | kpi_id                               |
| `period_year` **Required**  | `int` | Year when the kpi value applies      |
| `period_month` **Required** | `int` | id. Month when the kpi value applies |

#### Edit a KPI Value

```http
  PUT /kpi_values/<int:kpi_value_id>/edit
```

| JSON                   | Type    | Description                   | Response        |
| :--------------------- | :------ | :---------------------------- | :-------------- |
| `user_id` **Required** | `int`   | Id - Retrieved from jwt token | Success message |
| `value` **Required**   | `float` | Updates KPI value             |

#### Get KPI Values

```http
  GET /kpi_values
```

| Parameter | Type | Description                                              | Response                               |
| :-------- | :--- | :------------------------------------------------------- | :------------------------------------- |
| -         | -    | Get KPI Values - Supports Filtering Period and Circle Id | A list of all KPI values as dictionary |

#### Get Change Log for KPI Values

```http
  GET /kpi_values/change_log
```

| Parameter                 | Type     | Description            | Response                                                                                     |
| :------------------------ | :------- | :--------------------- | :------------------------------------------------------------------------------------------- |
| `circle_id` **Required**  | `int`    | Circle id              | Kpi_Values.value, Kpi.name, User.display_name, Change_Log.activity, Change_Log.registered_at |
| `from_year` **Required**  | `string` | Filtering "from year"  |
| `from_month` **Required** | `string` | Filtering "from month" |
| `to_year` **Required**    | `string` | Filtering "to year"    |
| `to_month` **Required**   | `string` | Filtering "to month"   |

Note: This endpoint supports filtering by "circle_id" and "period"

#### Get Mini Change Log When Editing KPI Values

```http
  GET /kpi_values/<int:kpi_values_id>/change_log
```

| Parameter                    | Type  | Description                      | Response                      |
| :--------------------------- | :---- | :------------------------------- | :---------------------------- |
| `kpi_values_id` **Required** | `int` | Fetches recent 3 change log rows | Recent 3 rows as a dictionary |

## Running Tests

To run tests, run the following command

```Terminal

```

`$ cd backend`

`$ python -m pytest`
