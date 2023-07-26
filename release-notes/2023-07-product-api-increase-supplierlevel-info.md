---
description: product api increase supplierLevel info
---

# 2023-07 product api increase supplierLevel info

The Product API adds a "[supplierLevel ](../admin-api/api-reference/products.md#response-parameter)" field, which currently contains 3 levels A, B, and C

1. A-level suppliers: The total inventory per SPU is above 300, and per SKU is typically above 100.
2. B-level suppliers: The total inventory per SPU is above 150, and per SKU is typically above 50.
3. C-level suppliers: The total inventory per SPU is below 100, and per SKU is typically between 10 and 50.
