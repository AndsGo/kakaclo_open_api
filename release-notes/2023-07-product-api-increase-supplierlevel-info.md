---
description: product api increase supplierLevel info
---

# 2023-07 product api increase supplierLevel info

The Product API response adds a "[supplierLevel ](../admin-api/api-reference/products.md#response-parameter)" field, which currently contains 4 levels "",A, B, and C。A, B, and C grade suppliers have already connected to my inventory management API, and the inventory information is relatively accurate and real-time

1. A-level suppliers: The total inventory per SPU is above 300, and per SKU is typically above 100.
2. B-level suppliers: The total inventory per SPU is above 150, and per SKU is typically above 50.
3. C-level suppliers: The total inventory per SPU is below 100, and per SKU is typically between 10 and 50.
4. ""-level suppliers: Such suppliers have not yet connected to our api system, and the inventory may not be accurate in real time.
