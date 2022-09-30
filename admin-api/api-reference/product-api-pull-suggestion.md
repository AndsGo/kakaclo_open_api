# Product API pull suggestion

## Product Stock relationship

<figure><img src="../../.gitbook/assets/file.drawing.svg" alt=""><figcaption></figcaption></figure>

The return value of the Product API includes stock (the sum of all sku stocks under spu), skuList, and skuList includes sku, stock (the sum of the stocks of all sku warehouses). The Stock API returns the specific inventory data of the warehouse corresponding to the sku. Therefore, by obtaining the return data of Stock Api, the total inventory of sku can be obtained, and then the inventory of spu can be obtaine

