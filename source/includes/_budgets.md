# Budgets

## List of budgets

```shell
curl -X GET "http://test.involvio.com/api/v20/budgets.json?involv_token=example_involvio_token"
```

> Sample JSON response:

```json
{
  "budgets": [
    {
      "id": 1,
      "name": "Chess Funds",
      "budget_period": {
        "start_date": "2019-03-01",
        "end_date": "2019-12-01"
      },
      "ref_no": "REF-1",
      "status": "approved"
    }
  ]
}
```

This end point returns all the budgets for the campus.

### HTTP Request

`GET http://test.involvio.com/api/v20/budgets.json`

### Query Parameters

Parameter | Optional | Description
--------- | -------- | -----------
involv_token | no | Involvio access token
status | yes | Filter by budget status
budget_period_id | yes | Filter by budget period

## List of budget types

```shell
curl -X GET "http://test.involvio.com/api/v20/budget_types.json?involv_token=example_involvio_token"
```

> Sample JSON response:

```json
{
  "budget_types": [
    {
      "id": 1,
      "name": "Athletics Special Allocation"
    },
    {
      "id": 2,
      "name": "Greek Special Allocation"
     }
  ]
}
```

This end point returns all the budget types for the campus.

### HTTP Request

`GET http://test.involvio.com/api/v20/budget_types.json`

### Query Parameters

Parameter | Optional | Description
--------- | -------- | -----------
involv_token | no | Involvio access token

## List of budget periods

```shell
curl -X GET "http://test.involvio.com/api/v20/budget_periods.json?involv_token=example_involvio_token"
```

> Sample JSON response:

```json
{
  "budget_periods": [
    {
      "id": 1,
      "name": "Winter Budget",
      "start_date": "2019-03-01",
      "end_date": "2019-07-01"
    },
    {
      "id": 2,
      "name": "Fall Budget",
      "start_date": "2019-08-01",
      "end_date": "2019-12-01"
    },
  ]
}
```

This end point returns all the budget periods for the campus.

### HTTP Request

`GET http://test.involvio.com/api/v20/budget_periods.json`

### Query Parameters

Parameter | Optional | Description
--------- | -------- | -----------
involv_token | no | Involvio access token

## List of budget categories

```shell
curl -X GET "http://test.involvio.com/api/v20/budget_categories.json?involv_token=example_involvio_token"
```

> Sample JSON response:

```json
{
  "budget_categories": [
    {
      "id": 1,
      "name": "Travel",
    },
    {
      "id": 2,
      "name": "Education",
    },
  ]
}
```

This end point returns all the budget categories for the campus.

### HTTP Request

`GET http://test.involvio.com/api/v20/budget_categories.json`

### Query Parameters

Parameter | Optional | Description
--------- | -------- | -----------
involv_token | no | Involvio access token

## List of line item types

```shell
curl -X GET "http://test.involvio.com/api/v20/budget_categories/1/line_item_types.json?involv_token=example_involvio_token"
```

> Sample JSON response:

```json
{
  "line_item_types": [
    {
      "id": 1,
      "name": "Plane Tickets",
    },
    {
      "id": 2,
      "name": "Cab",
    },
  ]
}
```

This end point returns all the line item types for a particular budget category.

### HTTP Request

`GET http://test.involvio.com/api/v20/budget_categories/:budget_category_id/line_item_types.json`

### Query Parameters

Parameter | Optional | Description
--------- | -------- | -----------
involv_token | no | Involvio access token
budget_category_id | no | Budget category id for which the line item types need to fetched

## Show budget

```shell
curl -X GET "http://test.involvio.com/api/v20/budgets/1.json?involv_token=example_involvio_token"
```

> Sample JSON response:

```json
{
  "id": 1,
  "name": "Chess Funds",
  "budget_period": {
    "start_date": "2019-03-01",
    "end_date": "2019-12-01"
  },
  "ref_no": "REF-1",
  "status": "approved"
}
```

This end point returns all the information for the budget.

### HTTP Request

`GET http://test.involvio.com/api/v20/budgets/:budget_id.json`

### Query Parameters

Parameter | Optional | Description
--------- | -------- | -----------
involv_token | no | Involvio access token
budget_id | no | Budget id for which the information needs to be fetched
