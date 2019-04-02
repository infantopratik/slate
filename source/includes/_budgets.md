# Budgets

## Get budgets

```shell
curl -X GET 'https://test.involvio.com/api/v20/groups/1/budgets.json?involv_token=example_involvio_token'
```

> Sample JSON response:

```json
{
  "pagination_data": {
    "total_pages": 1,
    "per_page": 30,
    "total_entries": 3,
    "current_page": 1
  },
  "budgets": [
    {
      "id": 10,
      "name": "Badminton Funds",
      "budget_period": {
        "start_date": "2019-03-01",
        "end_date": "2019-12-01"
      },
      "ref_no": "REF-10",
      "status": "approved",
      "approved_amount": "1000",
      "spent_amount": "200",
      "remaining_amount": "800"
    },
    {
      "id": 5,
      "name": "Chess Funds",
      "budget_period": {
        "start_date": "2019-03-01",
        "end_date": "2019-12-01"
      },
      "ref_no": "REF-5",
      "status": "approved",
      "approved_amount": "1000",
      "spent_amount": "200",
      "remaining_amount": "800"
    },
    {
       "id": 12,
       "name": "Tennis Funds",
       "budget_period": {
         "start_date": "2019-01-01",
         "end_date": "2019-02-28"
       },
       "ref_no": "REF-12",
       "status": "approved",
       "approved_amount": "1000",
       "spent_amount": "200",
       "remaining_amount": "800"
     }
  ]
}
```

This end point returns all the budgets for the campus ordered by locked(unlocked first), budget period start date descending, budget name ascending.

### HTTP Request

`GET {{host}}/api/v20/groups/:group_id/budgets.json`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group for which the budgets need to be fetched
status | no | Filter by budget status
budget_period_id | no | Filter by budget period
page | no | Get budgets for this page
per_page | no | Specifies how many items to be returned for each page

## Show budget

```shell
curl -X GET 'https://test.involvio.com/api/v20/groups/1/budgets/1.json?involv_token=example_involvio_token'
```

> Sample JSON response:

```json
{
  "id": 1,
  "name": "Chess Funds",
  "ref_no": "REF-1",
  "status": "approved",
  "approved_amount": "1000",
  "spent_amount": "200",
  "remaining_amount": "800",
  "budget_type": "Activities Budget",
  "budget_period": {
    "name": "School Year",
    "start_date": "2019-03-01",
    "end_date": "2019-12-01"
  },
  "budget_items": [
    {
      "id": 1,
      "name": "Travel Expenses",
      "approved_amount": 100,
      "spent_amount": 50,
      "remaining_amount": 50
    },
    {
      "id": 2,
      "name": "Food Expenses",
      "approved_amount": 100,
      "spent_amount": 50,
      "remaining_amount": 50
    }
  ]
}
```

This end point returns all the information for the budget.

### HTTP Request

`GET {{host}}/api/v20/groups/:group_id/budgets/:budget_id.json`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group for which the budgets need to be fetched
budget_id | yes | Budget id for which the information needs to be fetched

## Submit Budget

```shell
curl -X PUT \
'https://test.involvio.com/api/v20/groups/1/budgets/1/submit?involv_token=example_involvio_token' \
```

> Sample Success Response

```json
{
  "id": 1,
  "name": "National Chess Tournament(Updated Name)",
  "budget_period": {
    "start_date": "2019-03-01",
    "end_date": "2019-12-01"
  },
  "ref_no": "REF-1",
  "status": "in_review",
  "approved_amount": "0",
  "spent_amount": "0",
  "remaining_amount": "0"
}
```

> Sample Error Response: 422

```json
{
  "errors": "Budget is already submitted."
}
```

This end point submits a budget. It moves the budget from draft status to review status.

### HTTP Request

`PUT {{host}}/api/v20/groups/:group_id/budgets/:budget_id/submit`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group for which the budget needs to be updated
budget_id | yes | Identifier of the budget to be updated

### Status Codes
Status Code | Description
----------- | -----------
200 | When the budget is successfully updated
422 | When there are errors while creating the record(Mostly validation errors)

## Create Budget

```shell
curl -X POST \
'https://test.involvio.com/api/v20/groups/1/budgets?involv_token=example_involvio_token' \
-H "Content-Type: application/json" \
-d '{
  "budget": {
      "name": "National Chess Tournament",
      "budget_type_id": 1,
      "budget_period_id": 1
  }
}'
```

> Sample Success Response

```json
{
  "id": 1,
  "name": "National Chess Tournament",
  "budget_period": {
    "start_date": "2019-03-01",
    "end_date": "2019-12-01"
  },
  "ref_no": "REF-1",
  "status": "in_review",
  "approved_amount": "0",
  "spent_amount": "0",
  "remaining_amount": "0"
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
  "errors": "Budget period is locked."
}
```

This end point creates a budget for the specified group.

### HTTP Request

`POST {{host}}/api/v20/groups/:group_id/budgets`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
name | yes | Name of the budget
group_id | yes | Identifier of the group for which the budget needs to be created
budget_period_id | yes | Identifier of the budget period for which the budget needs to created
budget_type_id | yes | Identifier of the budget type, the budget to be created should belong to

### Status Codes
Status Code | Description
----------- | -----------
201 | When the budget is successfully created
400 | When the required parameters are not sent
422 | When there are errors while creating the record(Mostly validation errors)

## Update Budget

```shell
curl -X PUT \
'https://test.involvio.com/api/v20/groups/1/budgets/1?involv_token=example_involvio_token' \
-H "Content-Type: application/json" \
-d '{
  "budget": {
      "name": "National Chess Tournament(Updated Name)",
      "budget_period_id": 1
  }
}'
```

> Sample Success Response

```json
{
  "id": 1,
  "name": "National Chess Tournament(Updated Name)",
  "budget_period": {
    "start_date": "2019-03-01",
    "end_date": "2019-12-01"
  },
  "ref_no": "REF-1",
  "status": "in_review",
  "approved_amount": "0",
  "spent_amount": "0",
  "remaining_amount": "0"
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
  "errors": "Budget period is locked."
}
```

This end point updates a budget.

### HTTP Request

`PUT {{host}}/api/v20/groups/:group_id/budgets/:budget_id`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group for which the budget needs to be updated
budget_id | yes | Identifier of the budget to be updated
name | no | Name of the budget
budget_period_id | no | Identifier of the budget period for which the budget needs to created

### Status Codes
Status Code | Description
----------- | -----------
201 | When the budget is successfully created
400 | When the required parameters are not sent
422 | When there are errors while creating the record(Mostly validation errors)

## Delete budget

```shell
curl -X DELETE 'https://test.involvio.com/api/v20/groups/1/budgets/1?involv_token=example_involvio_token'
```

This end point deletes the budget.

### HTTP Request

`DELETE {{host}}/api/v20/groups/:group_id/budgets/:budget_id.json`

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

# Budget Types

## Get budget types

```shell
curl -X GET 'https://test.involvio.com/api/v20/budget_types.json?involv_token=example_involvio_token'
```

> Sample JSON response:

```json
{
  "pagination_data": {
    "total_pages": 1,
    "per_page": 30,
    "total_entries": 1,
    "current_page": 1
  },
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

`GET {{host}}/api/v20/budget_types.json`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
page | no | Get budgets for this page
per_page | no | Specifies how many items to be returned for each page

# Budget Periods

## Get budget periods

```shell
curl -X GET 'https://test.involvio.com/api/v20/budget_periods.json?involv_token=example_involvio_token'
```

> Sample JSON response:

```json
{
  "pagination_data": {
    "total_pages": 1,
    "per_page": 30,
    "total_entries": 1,
    "current_page": 1
  },
  "budget_periods": [
    {
      "id": 1,
      "name": "Winter Budget",
      "start_date": "2019-03-01",
      "end_date": "2019-07-01",
      "locked": true
    },
    {
      "id": 2,
      "name": "Fall Budget",
      "start_date": "2019-08-01",
      "end_date": "2019-12-01",
      "locked": false
    }
  ]
}
```

This end point returns all the budget periods for the campus.

### HTTP Request

`GET {{host}}/api/v20/budget_periods.json`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
locked | no | Filter budget periods by locked(true or false)
page | no | Get budgets for this page
per_page | no | Specifies how many items to be returned for each page

# Budget Items

## Get budget items

```shell
curl -X GET 'https://test.involvio.com/api/v20/groups/1/budgets/1/budget_items.json?involv_token=example_involvio_token'
```

> Sample JSON response:

```json
{
  "pagination_data": {
    "total_pages": 1,
    "per_page": 30,
    "total_entries": 1,
    "current_page": 1
  },
  "budget_items": [
    {
      "id": 1,
      "name": "Travel Expenses",
      "approved_amount": 100,
      "spent_amount": 50,
      "remaining_amount": 50
    },
    {
      "id": 2,
      "name": "Food Expenses",
      "approved_amount": 100,
      "spent_amount": 50,
      "remaining_amount": 50
    }
  ]
}
```

This end point returns all the budget items for a particular budget.

### HTTP Request

`GET {{host}}/api/v20/groups/:group_id/budgets/:budget_id/budget_items.json`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group to which the budget belongs
budget_id | yes | Identifier of the budget for which the budget items to be fetched
page | no | Get budgets for this page
per_page | no | Specifies how many items to be returned for each page

## Create Budget Item

```shell
curl -X POST \
'https://test.involvio.com/api/v20/groups/1/budgets/1/budget_items?involv_token=example_involvio_token' \
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
  "approved_amount": 0,
  "spent_amount": 0,
  "remaining_amount": 0
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

`POST {{host}}/api/v20/groups/:group_id/budgets/:budget_id/budget_items`

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
'https://test.involvio.com/api/v20/groups/1/budgets/1/budget_items/1?involv_token=example_involvio_token'
```

This end point deletes the budget.

### HTTP Request

`DELETE {{host}}/api/v20/groups/:group_id/budgets/:budget_id/budget_items/:budget_item_id`

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

# Budget Categories

## Get budget categories

```shell
curl -X GET 'https://test.involvio.com/api/v20/budget_categories.json?involv_token=example_involvio_token'
```

> Sample JSON response:

```json
{
  "pagination_data": {
    "total_pages": 1,
    "per_page": 30,
    "total_entries": 1,
    "current_page": 1
  },
  "budget_categories": [
    {
      "id": 1,
      "name": "Travel",
      "line_item_types": [
        {
          "id": 1,
          "name": "Plane Tickets"
        },
        {
          "id": 2,
          "name": "Cab"
        }
      ]
    },
    {
      "id": 2,
      "name": "Education",
      "line_item_types": [
        {
          "id": 1,
          "name": "Plane Tickets"
        },
        {
          "id": 2,
          "name": "Cab"
        }
      ]
    }
  ]
}
```

This end point returns all the budget categories for the campus.

### HTTP Request

`GET {{host}}/api/v20/budget_categories.json`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
page | no | Get budgets for this page
per_page | no | Specifies how many items to be returned for each page

# Line Items

## Get line items

```shell
curl -X GET 'https://test.involvio.com/api/v20/groups/1/budgets/1/budget_items/1/line_items.json?involv_token=example_involvio_token'
```

> Sample JSON response:

```json
{
  "pagination_data": {
    "total_pages": 1,
    "per_page": 30,
    "total_entries": 1,
    "current_page": 1
  },
  "line_items": [
    {
      "id": 1,
      "description": "Office to Airport",
      "amount": 100,
      "budget_item_id": 1,
      "line_item_type_id": 1
    }
  ]
}
```

This end point returns all the line items for a particular budget item.

### HTTP Request

`GET {{host}}/api/v20/groups/:group_id/budgets/:budget_id/budget_items/:budget_item_id/line_items.json`

### Parameters

Parameter | Required | Description
--------- | -------- | -----------
involv_token | yes | Involvio access token
group_id | yes | Identifier of the group to which the budget belongs
budget_id | yes | Identifier of the budget for which the budget items to be fetched
budget_item_id | yes | Identifier of the group for which the line items needs to be fetched
page | no | Get budgets for this page
per_page | no | Specifies how many items to be returned for each page

## Create Line Item

```shell
curl -X POST \
'https://test.involvio.com/api/v20/groups/1/budget_items/1/line_items?involv_token=example_involvio_token' \
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

`POST {{host}}/api/v20/groups/:group_id/budget_items/:budget_item_id/line_item.json`

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
'https://test.involvio.com/api/v20/groups/1/budgets/1/budget_items/1/line_items/1?involv_token=example_involvio_token'
```

This end point deletes a line item.

### HTTP Request

`DELETE {{host}}/api/v20/groups/:group_id/budgets/:budget_id/budget_items/:budget_item_id/line_items/:line_item_id`

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
