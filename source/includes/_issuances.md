# Issuances

<aside class="notice">
  Issuances are nested under two namespaces: <code>equity</code> and <code>debt</code>. Equity issuances record the issuance of shares to an equity security (common stock, preferred stock, option or warrant). Debt issuances record the issuance of principal for a convertible note. Make sure to use the correct namespace when modifying and retrieving records.
</aside>

## List Issuances

> Example array of issuances

```ruby
# GET /captables/1/equity/issuances.json

[
  {
    captable_id: 1,
    created_at: 1498523610,
    date: "2015-12-14",
    id: 1,
    invested_capital: 10000.0
    note: nil,
    price_per_share: 2.0,
    shares: 5000.0,
    target_security_id: 3,
    updated_at: 1498523610,
  },
  {
    captable_id: 1,
    created_at: 14985236495,
    date: "2015-12-14",
    id: 1,
    invested_capital: 10000.0
    note: nil,
    price_per_share: 2.0,
    shares: 10000.0,
    target_security_id: 4,
    updated_at: 14985236234,
  }
]
```

**Equity**  
List all equity issuances for the cap table.  

`GET /captables/:captable_id/equity/issuances.json`  

**Debt**  
List all debt issuances for the cap table.  

`GET /captables/:captable_id/debt/issuances.json`  

### Additional query parameters

| Parameter       | Type                 | Description                                                 |
|:----------------|:---------------------|:------------------------------------------------------------|
| security_id     | <code>Integer</code> | Only return records belonging to the specified security.    |
| shareholder_id  | <code>Integer</code> | Only return records belonging to the specified shareholder. |


## Retrieve Issuance

> Example issuance object

```ruby
# GET /captables/1/equity/issuances/1.json

{
  captable_id: 1,
  created_at: 1498523610,
  date: "2015-12-14",
  id: 1,
  invested_capital: 10000.0,
  note: nil,
  price_per_share: 2.0,
  shares: 5000.0,
  target_security_id: 3,
  updated_at: 1498523610,
}
```

### Equity
Retrieve a single equity issuance.  

`GET /captables/:captable_id/equity/issuances/:id.json`  

### Debt
Retrieve a single debt issuance.  

`GET /captables/:captable_id/debt/issuances/:id.json`  

## Create Issuance

<aside class="notice">
  In order to create issuances, you must provide a <code>:target_security_id</code>. To get this ID, you can either retrieve an existing security or create a new security. See the <a href="#securities">Securities</a> section for more details.
</aside>

> Example equity issuance object for create

```ruby
{
  issuance: {
    date: "2015-12-14",
    price_per_share: 1.0,
    shares: 3000.0,
    target_security_id: 1,
  }
}
```

### Equity
Create a new equity issuance.  

`POST /captables/:captable_id/equity/issuances.json`

**Issuance Attributes**  
Expects an `issuance` object containing the attributes for the new record.

| Name               | Type               | Description                                             | Qualifiers |
|:-------------------|:-------------------|:--------------------------------------------------------|:-----------|
| date               | `Date (YYYY-MM-DD)`| Date when the issuance occurred.                        | Required   |
| note               | `Text`             | Supplementary info about the issuance.                  | Optional   |
| price_per_share    | `Decimal`          | Price per share at which the shares were issued.        | Required   |
| shares             | `Decimal`          | Number of shares issued.                                | Required   |
| target_security_id | `Integer`          | Security for which shares were issued.                  | Required   |
| vested             | `Boolean`          | Whether or not the shares are vested (Default: `true`). | Optional   |

> Example debt issuance object for create

```ruby
{
  issuance: {
    date: "2015-12-14",
    invested_capital: 3000.0,
    target_security_id: 1,
  }
}
```

### Debt
Create a new debt issuance.  

`POST /captables/:captable_id/debt/issuances.json`

**Issuance Attributes**  
Expects an `issuance` object containing the attributes for the new record.

| Name               | Type               | Description                                             | Qualifiers |
|:-------------------|:-------------------|:--------------------------------------------------------|:-----------|
| date               | `Date (YYYY-MM-DD)`| Date when the issuance occurred.                        | Required   |
| note               | `Text`             | Supplementary info about the issuance.                  | Optional   |
| invested_capital   | `Decimal`          | Amount invested and added to principal balance.         | Required   |
| target_security_id | `Integer`          | Security for which shares were issued.                  | Required   |

## Update Issuance

> Example equity issuance object for update

```ruby
{
  issuance: {
    date: "2015-12-20",
  }
}
```

### Equity
Update an existing equity issuance.  

`PUT /captables/:captable_id/equity/issuances/:id.json`  

**Attributes**  
Expects an `issuance` object containing the new attributes for the record.

| Name               | Type               | Description                                             |
|:-------------------|:-------------------|:--------------------------------------------------------|
| date               | `Date (YYYY-MM-DD)`| Date when the issuance occurred.                        |
| note               | `Text`             | Supplementary info about the issuance.                  |
| price_per_share    | `Decimal`          | Price per share at which the shares were issued.        |
| shares             | `Decimal`          | Number of shares issued.                                |
| target_security_id | `Integer`          | Security for which shares were issued.                  |
| vested             | `Boolean`          | Whether or not the shares are vested (Default: `true`). |

> Example debt issuance object for update

```ruby
{
  issuance: {
    invested_capital: 4000.0,
  }
}
```

### Debt
Update an existing debt issuance.  

`PUT /captables/:captable_id/debt/issuances/:id.json`  

**Attributes**  
Expects an `issuance` object containing the new attributes for the record.

| Name               | Type               | Description                                             |
|:-------------------|:-------------------|:--------------------------------------------------------|
| date               | `Date (YYYY-MM-DD)`| Date when the issuance occurred.                        |
| note               | `Text`             | Supplementary info about the issuance.                  |
| principal          | `Decimal`          | Amount added to the principal balance.                  |
| target_security_id | `Integer`          | Security for which shares were issued.                  |

## Delete Issuance
Deletes an existing issuance.  

`DELETE /captables/:captable_id/issuances/:id.json`
