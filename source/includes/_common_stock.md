# Common Stock

Resources for modifying and retrieving common stock securities.

## List Common Stock

> Example array of common stock objects

```ruby
# GET /captables/1/equity/common/stocks.json

[
  {
    as_converted_shares: 20000.0,
    captable_id: 1,
    created_at: 1498523610,
    date: "2017-01-01",
    equity_plan_id: nil,
    federal_exemption: "",
    id: 1,
    invested_capital: 0.2,
    legend: "",
    name: "CS-1",
    price_per_share: 0.00001,
    security_class_id: 2,
    shareholder_id: 4,
    shares_outstanding: 20000.0,
    state_exemption: "",
    updated_at: 1498523610,
    vesting_plan_id: nil,
  },
  {
    as_converted_shares: 20000.0,
    captable_id: 1,
    created_at: 1498523610,
    date: "2017-01-01",
    equity_plan_id: nil,
    federal_exemption: "",
    id: 2,
    invested_capital: 0.2,
    legend: "",
    name: "CS-2",
    price_per_share: 0.00001,
    security_class_id: 2,
    shareholder_id: 5,
    shares_outstanding: 20000.0,
    state_exemption: "",
    updated_at: 1498523610,
    vesting_plan_id: nil,
  }
]
```

List all common stock securities for a cap table.

`GET /captables/:captable_id/equity/common/stocks.json`  

### Additional query parameters

| Parameter         | Type                 | Description                                                    |
|:------------------|:---------------------|:---------------------------------------------------------------|
| security_class_id | <code>Integer</code> | Only return records belonging to the specified security class. |
| shareholder_id    | <code>Integer</code> | Only return records belonging to the specified shareholder.    |

## Retrieve Common Stock

> Example common stock object

```ruby
# GET /captables/1/equity/common/stocks/1.json
{
  as_converted_shares: 20000.0,
  captable_id: 1,
  created_at: 1498523610,
  date: "2017-01-01",
  equity_plan_id: nil,
  federal_exemption: "",
  id: 1,
  invested_capital: 0.2,
  legend: "",
  name: "CS-1",
  price_per_share: 0.00001,
  security_class_id: 2,
  shareholder_id: 5,
  shares_outstanding: 20000.0,
  state_exemption: "",
  updated_at: 1498523610,
  vesting_plan_id: nil,
}
```

Retrieve a single common stock security.  

`GET /captables/:captable_id/equity/common/stocks/:id.json`  

## Create Common Stock

> Example stock object for create

```ruby
{
  stock: {
    date: "2017-01-01",
    legend: "",
    name: "CS-1",
    security_class_id: 2,
    shareholder_id: 5,
  }
}
```

Create a new common stock security.  

`POST /captables/:captable_id/equity/common/stocks.json`  

**Attributes**  
Expects a `stock` object containing the attributes for the new record.

| Name                   | Type                | Description                                                                | Qualifiers                            |
|:-----------------------|:--------------------|:---------------------------------------------------------------------------|:--------------------------------------|
| 83b_election_file_date | `Date (YYYY-MM-DD)` | Date the shareholder filed for 83(b) election.                             | Optional                              |
| date                   | `Date (YYYY-MM-DD)` | Date when the stock was created.                                           | Required                              |
| equity_plan_id         | `Integer`           | ID of the equity plan under which the security was issued.                 | Optional                              |
| federal_exemption      | `String`            | Statute under which the security is exempted from federal registration.    | Optional                              |
| legend                 | `String`            | Statement noting restrictions on the sale or transfer of the stock.        | Optional                              |
| name                   | `String`            | Name of the stock security (e.g., "CS-1").                                 | Required                              |
| security_class_id      | `Integer`           | Security class under which the security was created.                       | Required                              |
| shareholder_id         | `Integer`           | ID of the shareholder who owns the security.                               | Required                              |
| state_exemption        | `String`            | Statute under which the security is exempted from state registration.      | Optional                              |
| vesting_plan_id        | `Integer`           | ID of the vesting plan applied to the security.                            | Optional                              |
| vesting_start_date     | `Date (YYYY-MM-DD)` | Date on which vesting begins.                                              | Required if `vesting_plan_id` present |

<aside class="notice">
  The stock security by itself does not have any shares. An issuance must be created to provide shares to the security. This can be done separately using the <a href="#issuances">issuances</a> resource, or by including the attributes below as part of the stock object attributes.
</aside>

**Additional Attributes**  
Provide both these attributes to automatically create an issuance along with the security.

| Name            | Type      | Description                                  | Qualifiers |
|:----------------|:----------|:---------------------------------------------|:-----------|
| price_per_share | `Decimal` | Price per share at which shares were issued. | Optional   |
| shares          | `Decimal` | Number of shares issued.                     | Required   |
