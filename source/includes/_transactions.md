

## Equity Transactions

| Name            | Type               | Description                                             | Qualifiers |
|:----------------|:-------------------|:--------------------------------------------------------|:-----------|
| date            | `Date (YYYY-MM-DD)`| Date when the issuance occurred.                        | Required   |
| note            | `Text`             | Supplementary info about the issuance.                  | Optional   |
| price_per_share | `Decimal`          | Price per share at which the shares were issued.        | Required   |
| shares          | `Decimal`          | Number of shares issued.                                | Required   |
| target_security | `Hash`             | Hash representing security where shares were issued to. | Required   |
| vested          | `Boolean`          | Whether or not the shares are vested (Default: `true`). | Optional   |

**Security Types**  
There are five security types for which shares can be issued:

1. Common Stock
2. Preferred Stock
3. Options
4. Warrants
5. Convertible Notes (Debt)

The creation and retrieval of issuances is different for each of the various security types. The main difference between each (aside from the namespace) is the attributes that are required and allowed for the `target_security` hash.

**Target Security**  
All issuances belong to a security, which is referred to as its "target security." When creating a new issuance, the `target_security` hash must be provided. The attributes required for this hash are listed under each security type below.

## Debt Transactions
