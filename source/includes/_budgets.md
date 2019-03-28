# Budgets

## List of budgets

```shell
curl -X GET 'http://test.involvio.com/api/v20/groups/1/budgets.json?involv_token=example_involvio_token'
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
      "status": "approved",
      "approved_amount": "1000",
      "spent_amount": "200",
      "remaining_amount": "800"
    }
  ]
}
```

This end point returns all the budgets for the campus.

### HTTP Request

`GET http://test.involvio.com/api/v20/groups/:group_id/budgets.json`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group for which the budgets need to be fetched
status | no | Filter by budget status
budget_period_id | no | Filter by budget period

## List of budget types

```shell
curl -X GET 'http://test.involvio.com/api/v20/budget_types.json?involv_token=example_involvio_token'
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

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token

## List of budget periods

```shell
curl -X GET 'http://test.involvio.com/api/v20/budget_periods.json?involv_token=example_involvio_token'
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

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token

## List of budget categories

```shell
curl -X GET 'http://test.involvio.com/api/v20/budget_categories.json?involv_token=example_involvio_token'
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

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token

## List of line item types

```shell
curl -X GET 'http://test.involvio.com/api/v20/budget_categories/1/line_item_types.json?involv_token=example_involvio_token'
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

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
budget_category_id | yes | Budget category id for which the line item types need to fetched

## Show budget

```shell
curl -X GET 'http://test.involvio.com/api/v20/groups/1/budgets/1.json?involv_token=example_involvio_token'
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
  "approved_amount": "1000",
  "spent_amount": "200",
  "remaining_amount": "800"
}
```

This end point returns all the information for the budget.

### HTTP Request

`GET http://test.involvio.com/api/v20/groups/:group_id/budgets/:budget_id.json`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group for which the budgets need to be fetched
budget_id | yes | Budget id for which the information needs to be fetched

## Delete budget

```shell
curl -X DELETE 'http://test.involvio.com/api/v20/groups/1/budgets/1?involv_token=example_involvio_token'
```

This end point deletes the budget.

### HTTP Request

`DELETE http://test.involvio.com/api/v20/groups/:group_id/budgets/:budget_id.json`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group for which the budgets need to be fetched
budget_id | yes | Identifier of the budget which needs to be deleted

### Status Codes
Status Code | Description
----------- | -----------
204 | When the budget is successfully deleted
404 | When the budget with the budget_id is not found

## Create Line Item

```shell
curl -X POST \
'http://test.involvio.com/api/v20/groups/1/budget_items/1/line_items?involv_token=example_involvio_token' \
-H "Content-Type: application/json" \
-d '{
  "line_item": {
      "description": "Office to Airport",
      "amount": 100,
      "budget_item_id": 1,
      "line_item_type_id": 1
  }
}'
```

> Sample Success Response

```json
{
  "id": 1,
  "description": "Office to Airport",
  "amount": 100,
  "budget_item_id": 1,
  "line_item_type_id": 1
}
```

> Sample Error Response: 400

```json
{
  "errors": "One/all of the required parameters are missing."
}
```

> Sample Error Response: 422

```json
{
  "errors": "Amount cannot be greater than $1000."
}
```

This end point creates a line item for a particular budget item.

### HTTP Request

`POST http://test.involvio.com/api/v20/groups/:group_id/budget_items/:budget_item_id/line_item.json`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group for which the budgets need to be fetched
description | yes | Description of the line item
amount | yes | Amount to be budgeted for this line item
budget_item_id | yes | Identifier of the budget item for which the line item has to be created
line_item_type_id | yes | Identifier of the line type for which the line item has to be created

### Status Codes
Status Code | Description
----------- | -----------
201 | When the line item is successfully created
400 | When the required parameters are not sent
422 | When there are errors while creating the record(Mostly validation errors)

## Delete Line Item

```shell
curl -X DELETE \
'http://test.involvio.com/api/v20/groups/1/budgets/1/budget_items/1/line_items/1?involv_token=example_involvio_token'
```

This end point deletes a line item.

### HTTP Request

`DELETE http://test.involvio.com/api/v20/groups/:group_id/budgets/:budget_id/budget_items/:budget_item_id/line_items/:line_item_id`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group for which the the line item belongs
budget_id | yes | Identifier of the budget for which the the line item belongs
budget_item_id | yes | Identifier of the budget item for which the the line item belongs
line_item_id | yes | Identifier of the line item which needs to be deleted

### Status Codes
Status Code | Description
----------- | -----------
204 | When the line item is successfully deleted
404 | When the line item with the line_item_id is not found

## Create Budget Item

```shell
curl -X POST \
'http://test.involvio.com/api/v20/groups/1/budgets/1/budget_items?involv_token=example_involvio_token' \
-H "Content-Type: application/json" \
-d '{
  "budget_item": {
      "name": "Travel Expenses",
      "budget_category_id": 1,
  }
}'
```

> Sample Success Response

```json
{
  "id": 1,
  "name": "Travel Expenses",
}
```

> Sample Error Response: 400

```json
{
  "errors": "One/all of the required parameters are missing."
}
```

> Sample Error Response: 422

```json
{
  "errors": "Name too long."
}
```

This end point creates a budget item for a particular budget.

### HTTP Request

`POST http://test.involvio.com/api/v20/groups/:group_id/budgets/:budget_id/budget_items`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group for which the budget belongs
budget_id | yes | Identifier of the budget for which the budget item needs to be created
name | yes | Name of the budget item
budget_category_id | yes | Identifier of the budget category

### Status Codes
Status Code | Description
----------- | -----------
201 | When the budget item is successfully created
400 | When the required parameters are not sent
422 | When there are errors while creating the record(Mostly validation errors)

## Delete Budget Item

```shell
curl -X DELETE \
'http://test.involvio.com/api/v20/groups/1/budgets/1/budget_items/1?involv_token=example_involvio_token'
```

This end point deletes the budget.

### HTTP Request

`DELETE http://test.involvio.com/api/v20/groups/:group_id/budgets/:budget_id/budget_items/:budget_item_id`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group for which the budget item belongs to
budget_id | yes | Identifier of the budget for which the budget item belongs to
budget_item_id | yes | Identifier of the budget item to be deleted

### Status Codes
Status Code | Description
----------- | -----------
204 | When the budget item is successfully deleted
404 | When the budget item with the budget_item_id is not found
