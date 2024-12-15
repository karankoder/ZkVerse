# Shopify Order Verification: Proof of Purchases for Validating Customer Claims

## Overview

This project integrates Shopify's public APIs into the zkPass ecosystem to provide **verifiable proof of purchases** while preserving user privacy. This can be utilized for verifying customer claims, ensuring authenticity in returns, or loyalty program participation.

## Problem Statement

Verifying purchase authenticity often requires sharing extensive transactional data or sensitive order details. Our schema leverages zero-knowledge proofs to validate specific purchases without exposing unrelated or private information.

## Features

- Verifies specific order details, such as order ID or product name.
- Ensures privacy with zkTLS and zero-knowledge proofs.
- Compatible with Shopify's public APIs for seamless integration.

## Use Case

E-commerce platforms, return processing teams, and loyalty programs can validate customer claims of purchases or product ownership without compromising sensitive order data.

## Integration Details

### Data Source

**Shopify**: The integration uses Shopify's publicly accessible APIs to fetch customer order details.

### API Details

- **Endpoint**: `https://{store_name}.myshopify.com/admin/api/2024-01/orders.json`
- **Data Points**:
  - Order ID
  - Product Title
  - Customer Email

### Schema Configuration

```json
{
  "issuer": "Shopify",
  "desc": "Verify Shopify orders to validate purchases or claims without exposing full transaction details.",
  "website": "https://shopify.dev/api",
  "APIs": [
    {
      "host": "{store_name}.myshopify.com",
      "intercept": {
        "url": "/admin/api/2024-01/orders.json",
        "method": "GET",
        "query": [
          {
            "status": "any",
            "verify": true
          }
        ],
        "header": [
          {
            "X-Shopify-Access-Token": "<ACCESS_TOKEN>",
            "verify": true
          }
        ]
      },
      "assert": [
        {
          "key": "orders|0|id",
          "value": "<ORDER_ID>",
          "operation": "="
        },
        {
          "key": "orders|0|line_items|0|title",
          "value": "<PRODUCT_TITLE>",
          "operation": "contains"
        }
      ],
      "nullifier": "orders|0|id"
    }
  ],
  "HRCondition": ["Order ID and Product Title Matched for Verification"],
  "tips": {
    "message": "Enter your Shopify store name and access token to retrieve and verify order details."
  }
}
```

## Workflow

1. **User Authentication**: Users provide their Shopify store name and access token to fetch order data.
2. **Data Interception**: The schema uses Shopify's API to retrieve the user's order details.
3. **Zero-Knowledge Verification**: zkPass verifies specific order information (e.g., order ID and product name) without exposing sensitive data.
4. **Validation**: The verified proof is used for claim validation, loyalty programs, or other use cases.

## Resources

- [Shopify API Documentation](https://shopify.dev/api)
- [zkPass Developer Guide](https://zkpass.org/developer-guide)
- [Zero-Knowledge Proofs Overview](https://zkpass.org/zkp-overview)

## **Contact**

For inquiries or feedback, feel free to reach out:

**Team Name:** zkVerse
**Project Lead:** Karan Kumar Das  
**Email:** karankr.das.cse22@iitbhu.ac.in
