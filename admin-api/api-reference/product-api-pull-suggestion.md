# Product API pull suggestion

## Product Stock relationship

<figure><img src="../../.gitbook/assets/file.drawing (2).svg" alt=""><figcaption></figcaption></figure>

The return value of the Product API includes stock (the sum of all sku stocks under spu), skuList, and skuList includes sku, stock (the sum of the stocks of all sku warehouses). The Stock API returns the specific inventory data of the warehouse corresponding to the sku. Therefore, by obtaining the return data of Stock Api, the total inventory of sku can be obtained, and then the inventory of spu can be obtaine

## Pull process suggestion

It is recommended that you refer to the following process for programming

<figure><img src="../../.gitbook/assets/file.drawing.svg" alt=""><figcaption></figcaption></figure>

Step 1. Obtained by "dateStartTime", "dateEndTime" call "product API" to pull product information.&#x20;

Step 2. After processing the product response data, store it in the database "product" table and "sku" table respectively, and the "product" table and "sku" table are related by the spu or kkProductId field.

Step 1 to Step 2 until the "dateEndTime" in Step 1 reaches the end of the current time.

Step 3. Obtained by "dateStartTime", "dateEndTime" call "Stock API" to pull stock information.

Step 4. Store the stock data in the database stock table.

Step 5.  Sum the warehouse inventory of sku to obtain the current total inventory of sku, and update it to the sku data table

Step 6.  Obtain the spu through the sku, sum the sku inventory of the spu, get the current total inventory of the spu, and then update it to the product data table

Step 3 to Step 6 until the "dateEndTime" in Step 3 reaches the end of the current time.

Through the above steps, you can basically think that the data in the product, sku, and stock tables in your database are real-time. You can get spuStatus, skuStatus, stock information from product table and sku table.

{% hint style="info" %}
You can select an appropriate step size when obtaining through "dateStartTime" and "dateEndTime", and "dateEndTime" cannot be greater than the current time. "dateStartTime" is suggested to be the "dateEndTime" of the last pull.&#x20;

The pull cycle is recommended to be every 2-5 minutes.
{% endhint %}
