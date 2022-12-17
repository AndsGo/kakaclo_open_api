# Orders Status Json Response

## Waiting to ship Status  <a href="#response-parameter" id="response-parameter"></a>

```json
{
    "code": 10000,
    "message": "success",
    "data": {
        "vo": null,
        "list": [
            {
                "id": "1000000463303",
                "customOrderId": "1003",
                "remark": null,
                "status": "processing",
                "financialStatus": "paid",
                "fulfillmentStatus": "waiting_to_ship",
                "refundStatus": "NULL",
                "purchaseDate": "2022-09-29T03:07:23Z",
                "payDate": "2022-09-29T03:07:27Z",
                "completedDate": "2022-09-29T03:07:27Z",
                "cancelDate": null,
                "refundDate": null,
                "shippingAddress": {
                    "country": "US",
                    "city": "Orleans",
                    "phone": "07 82 20 10 93",
                    "recipient": "Lollia Olena222",
                    "street1": " 7 rue Francois Rabelais",
                    "street2": null,
                    "province": "dsasd",
                    "zip": "11111",
                    "vat": null,
                    "ioss": null
                },
                "warehouseId": 1,
                "finalAmount": 22.2100,
                "freightAmount": 9.1000,
                "subTotalAmount": 13.1100,
                "orderItems": [
                    {
                        "id": "1094207",
                        "itemId": "1077104",
                        "refundStatus": "NULL",
                        "imageUrl": "https://img.kakaclo.com/image%2FFSZW07844%2FFSZW07844_NB_S_NUB%2Fc7f22ba71ef71427d2287cdab3b67703.jpg",
                        "productName": null,
                        "productNum": 1,
                        "skuCode": "FSZW07844_NB_S_NUB",
                        "option1": "{\"name\":\"color\", \"value\":\"Champlain color\"}",
                        "option2": "{\"name\":\"size\", \"value\":\"S\"}",
                        "option3": null,
                        "total": 5.6800,
                        "amount": 5.6800
                    },
                    {
                        "id": "1094224",
                        "itemId": "1077104",
                        "refundStatus": "NULL",
                        "imageUrl": "https://img.kakaclo.com/image%2FAMN01214%2FAMN01214_B_L%2F08e2ee632ea20d8925755d05530abb19.jpg",
                        "productName": null,
                        "productNum": 1,
                        "skuCode": "AMN01214_B_S_AK",
                        "option1": "{\"name\":\"color\",\"value\":\"Black\"}",
                        "option2": "{\"name\":\"size\",\"value\":\"PAT2\"}",
                        "option3": null,
                        "total": 7.4300,
                        "amount": 7.4300
                    }
                ],
                "fulfillments": null,
                "createDate": "2022-09-29T02:57:20Z",
                "modifyDate": "2022-09-29T09:18:22Z"
            }
        ],
        "total": 1,
        "pageNumber": 1,
        "pageSize": 10,
        "totalPageNumber": null,
        "modifyDate": null,
        "nextId": null
    }
}
```



## Partial Shipped Status <a href="#response-parameter" id="response-parameter"></a>

```json
{
    "code": 10000,
    "message": "success",
    "data": {
        "vo": null,
        "list": [
            {
                "id": "1000000387267",
                "customOrderId":"1002",
                "remark": null,
                "status": "processing",
                "financialStatus": "paid",
                "fulfillmentStatus": "partially_shipped",
                "refundStatus": "NULL",
                "purchaseDate": "2022-08-20T07:26:51Z",
                "payDate": "2022-08-20T07:26:54Z",
                "completedDate": "2022-08-20T07:26:54Z",
                "cancelDate": null,
                "refundDate": null,
                "shippingAddress": {
                    "country": "AU",
                    "city": "dasda",
                    "phone": "123456789",
                    "recipient": "test",
                    "street1": "test",
                    "street2": null,
                    "province": "dsad",
                    "zip": "DSDA",
                    "vat": null,
                    "ioss": null
                },
                "warehouseId": 13,
                "finalAmount": 34.2000,
                "freightAmount": 12.9300,
                "subTotalAmount": 21.2700,
                "orderItems": [
                    {
                        "id": "1077104",
                        "itemId": "1077104",
                        "refundStatus": "NULL",
                        "imageUrl": "https://img.kakaclo.com/image%2FFSZW05475%2FFSZW05475_W_S_NUB%2F034de8662a1ad3f607b3c0522cdef229.jpg",
                        "productName": null,
                        "productNum": 2,
                        "skuCode": "FSZW05475_W_S_NUB",
                        "option1": "{\"name\":\"color\", \"value\":\"Raw white off white\"}",
                        "option2": "{\"name\":\"size\", \"value\":\"S\"}",
                        "option3": null,
                        "total": 14.4600,
                        "amount": 7.2300
                    },
                    {
                        "id": "1077105",
                        "itemId": "1077105",
                        "refundStatus": "NULL",
                        "imageUrl": "https://img.kakaclo.com/image%2FFSZW04034%2FFSZW04034_B_S_NUB%2F79d666e1b9f98c42d3d417d04dda9ae8.jpg",
                        "productName": null,
                        "productNum": 1,
                        "skuCode": "FSZW04034_B_XL_NUB",
                        "option1": "{\"name\":\"color\", \"value\":\"Black\"}",
                        "option2": "{\"name\":\"size\", \"value\":\"XL\"}",
                        "option3": null,
                        "total": 6.8100,
                        "amount": 6.8100
                    }
                ],
                "fulfillments": [
                    {
                        "deliveryTime": "2022-08-20T08:16:15Z",
                        "trackingCode": "VR464908390YP",
                        "id": "KA2022082015300120_1",
                        "carrier": "Yanwen",
                        "carrierType": "last",
                        "logisticsSearchUrl": "https://track.yw56.com.cn",
                        "items": [
                            {
                                "id": "1077104",
                                "itemId": "1077104",
                                "refundStatus": "NULL",
                                "imageUrl": "https://img.kakaclo.com/image%2FFSZW05475%2FFSZW05475_W_S_NUB%2F034de8662a1ad3f607b3c0522cdef229.jpg",
                                "productName": null,
                                "productNum": 2,
                                "skuCode": "FSZW05475_W_S_NUB",
                                "option1": "{\"name\":\"color\", \"value\":\"Raw white off white\"}",
                                "option2": "{\"name\":\"size\", \"value\":\"S\"}",
                                "option3": null,
                                "total": 14.4600,
                                "amount": 7.2300
                            }
                        ]
                    }
                ],
                "createDate": "2022-08-20T07:24:50Z",
                "modifyDate": "2022-09-29T09:15:49Z"
            }
        ],
        "total": 1,
        "pageNumber": 1,
        "pageSize": 10,
        "totalPageNumber": null,
        "modifyDate": null,
        "nextId": null
    }
}
```

## Shipped Status <a href="#response-parameter" id="response-parameter"></a>

```json
{
    "code": 10000,
    "message": "success",
    "data": {
        "vo": null,
        "list": [
            {
                "id": "1000000462144",
                "customOrderId": "1001",
                "remark": null,
                "status": "processing",
                "financialStatus": "paid",
                "fulfillmentStatus": "fully_shipped",
                "refundStatus": "NULL",
                "purchaseDate": "2022-09-28T03:32:17Z",
                "payDate": "2022-09-28T03:32:23Z",
                "completedDate": "2022-09-28T03:32:23Z",
                "cancelDate": null,
                "refundDate": null,
                "shippingAddress": {
                    "country": "VE",
                    "city": "Orleans",
                    "phone": "07 82 20 10 93",
                    "recipient": "Lollia Olena222",
                    "street1": " 7 rue Francois Rabelais",
                    "street2": null,
                    "province": "dddssssd",
                    "zip": "11111",
                    "vat": null,
                    "ioss": null
                },
                "warehouseId": 1,
                "finalAmount": 35.9800,
                "freightAmount": 22.8700,
                "subTotalAmount": 13.1100,
                "orderItems": [
                    {
                        "id": "1094003",
                        "itemId": "1094003",
                        "refundStatus": "NULL",
                        "imageUrl": "https://img.kakaclo.com/image%2FAMN01214%2FAMN01214_B_L%2F08e2ee632ea20d8925755d05530abb19.jpg",
                        "productName": null,
                        "productNum": 1,
                        "skuCode": "AMN01214_B_S_AK",
                        "option1": "{\"name\":\"color\",\"value\":\"Black\"}",
                        "option2": "{\"name\":\"size\",\"value\":\"PAT2\"}",
                        "option3": null,
                        "total": 7.4300,
                        "amount": 7.4300
                    },
                    {
                        "id": "1094004",
                        "itemId": "1094003",
                        "refundStatus": "NULL",
                        "imageUrl": "https://img.kakaclo.com/image%2FFSZW07844%2FFSZW07844_NB_S_NUB%2Fc7f22ba71ef71427d2287cdab3b67703.jpg",
                        "productName": null,
                        "productNum": 1,
                        "skuCode": "FSZW07844_NB_S_NUB",
                        "option1": "{\"name\":\"color\", \"value\":\"Champlain color\"}",
                        "option2": "{\"name\":\"size\", \"value\":\"S\"}",
                        "option3": null,
                        "total": 5.6800,
                        "amount": 5.6800
                    }
                ],
                "fulfillments": [
                    {
                        "deliveryTime": "2022-09-29T03:25:02Z",
                        "trackingCode": "WNBAA0202970436YQ",
                        "id": "KA2022092811300049_1",
                        "status": "shipped",
                        "carrier": "wandexpress",
                        "carrierType": "last",
                        "logisticsSearchUrl": "https://t.17track.net/en?v=2#nums=WNBAA0202970436YQ",
                        "items": [
                            {
                                "id": "1094004",
                                "itemId": "1094003",
                                "refundStatus": "NULL",
                                "imageUrl": "https://img.kakaclo.com/image%2FFSZW07844%2FFSZW07844_NB_S_NUB%2Fc7f22ba71ef71427d2287cdab3b67703.jpg",
                                "productName": null,
                                "productNum": 1,
                                "skuCode": "FSZW07844_NB_S_NUB",
                                "option1": "{\"name\":\"color\", \"value\":\"Champlain color\"}",
                                "option2": "{\"name\":\"size\", \"value\":\"S\"}",
                                "option3": null,
                                "total": 5.6800,
                                "amount": 5.6800
                            },
                            {
                                "id": "1094003",
                                "itemId": "1094003",
                                "refundStatus": "NULL",
                                "imageUrl": "https://img.kakaclo.com/image%2FAMN01214%2FAMN01214_B_L%2F08e2ee632ea20d8925755d05530abb19.jpg",
                                "productName": null,
                                "productNum": 1,
                                "skuCode": "AMN01214_B_S_AK",
                                "option1": "{\"name\":\"color\",\"value\":\"Black\"}",
                                "option2": "{\"name\":\"size\",\"value\":\"PAT2\"}",
                                "option3": null,
                                "total": 7.4300,
                                "amount": 7.4300
                            }
                        ]
                    }
                ],
                "createDate": "2022-09-28T03:22:16Z",
                "modifyDate": "2022-09-29T08:27:21Z"
            }
        ],
        "total": 1,
        "pageNumber": 1,
        "pageSize": 10,
        "totalPageNumber": null,
        "modifyDate": null,
        "nextId": null
    }
}
```

