# Budgets

## List all budgets

```shell
curl -X GET "http://test.involvio.com/api/v20/budgets.json?involv_token=example_involvio_token"
```

> The above command returns JSON structured like this:

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
