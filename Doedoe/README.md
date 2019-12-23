# DoeDoe-API-spec

### Host Name

https://dodoapi.dermai.com.tw

### API Version

0.1

----

### Get Risk Result API

purpose for getting result of a mole risk

* **End Point:** `/predict`

* **Method:** `POST`

* **Request Headers:**

| Field | Type | Description |
| :---: | :---: | :---: |
| Content-Type | String | Only accept `application/json`. |

* **Request Body**

| Field | Type | Description |
| :---: | :---: | :---: |
| image_crop | String | naming rule is `{original_image}_crop`, and size is only accept `300*300` |
| sex | String | Only accept `男性` or `女性` or `不想回答`|
| age | String | Only accept `14歲以下` or `15~25歲` or `26~50歲	` or `51歲以上` |
| period | String | Only accept `三個月以上` or `三個月以下` |
| compress | String | Only accept `有` or `無` |
| product | String | Only accept `有，使用醫師開立的外用藥` or `有，藥局自行購買的外用藥` or `有，藥局自行購買的外用藥` or `無`|
| drug | String | Only accept `有` or `無` |
| menstruation | String | Only accept `有` or `無(包含男性和無月經者)` |
| fbid(Optional) | String | user id |
| fbnm(Optional) | String | user name |

* **Request Body Example:**

```
{
    "image_crop": "https://dodo.ic-hit.net/static/data/U1d5f092e04d4a742266e69415d90f793-c12u14cr-201912180144_crop.jpg",
    "sex": "男性",
    "age": "15~25歲",
    "compress": "有",
    "period": "三個月以上",
    "product": "無",
    "drug": "無",
    "menstruation": "無(包含男性和無月經者)"
}


or

{
    "image_crop": "1emdiaueiwq...(base64data)",
    "sex": "男性",
    "age": "15~25歲",
    "compress": "有",
    "period": "三個月以上",
    "product": "無",
    "drug": "無",
    "menstruation": "無(包含男性和無月經者)"
}


```

* **Success Response: 200**

| Field | Type | Description |
| :---: | :---: | :--- |
| | list | The first element is score, and the second is result. For result, 0 equals to lower and 1 equals to higher |

```
[
    0.3046926977390285,
    0
]

```