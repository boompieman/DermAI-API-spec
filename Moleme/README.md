# Moleme-API-spec

### Host Name

https://moleapi.dermai.com.tw/api/{version}

### API Version

v1

### example

https://moleapi.dermai.com.tw/api/v1

----

### Upload Image API

purpose for detacting if a mole in a picture

* **End Point:** `/Upload`

* **Method:** `POST`

* **Request Headers:**

| Field | Type | Description |
| :---: | :---: | :---: |
| Content-Type | String | Only accept `application/json`. |
| x-access-token | String | Provided by `DermAI`, please ask. |

* **Request Body**

| Field | Type | Description |
| :---: | :---: | :---: |
| image | String | Only accept `image_url` or `base64data` |

* **Request Body Example:**

```
{
    "image": "https://devel.dermai.com.tw/static/data/U4879646ee62667fa5faac183e2d3d1c1-fl_4y97x-201910290924.jpg"
}
```

or

```
{
    "image": "1emdiaueiwq...(base64data)"
}
```

* **Success Response: 200**

| Field | Type | Description |
| :---: | :---: | :--- |
| CheckImageHaveSkinScore | Double | The confidential score to detact if there is a mole in picture |
| ImageSizeScore | Double | The confidential score to check if image size is enough to detact a mole, more than 1 means it's enough |
| Message | String | |
| Reject | Bool | return `true` or `false`, if true, then suggest user to take/upload another picture  |
| X | Int | x-axis of the mole |
| Y | Int | y-axis of the mole |

```
{
    "CheckImageHaveSkinScore": 0.9969918727874756,
    "ImageSizeScore": 5.325,
    "Message": "",
    "Reject": false,
    "X": 437,
    "Y": 901
}
```

----

### Get Risk Result API

purpose for getting result of a mole risk

* **End Point:** `/GetRisk`

* **Method:** `POST`

* **Request Headers:**

| Field | Type | Description |
| :---: | :---: | :---: |
| Content-Type | String | Only accept `application/json`. |
| x-access-token | String | Provided by `DermAI`, please ask. |

* **Request Body**

| Field | Type | Description |
| :---: | :---: | :---: |
| image_crop | String | naming rule is `{original_image}_crop`, and size is only accept `300*300` |
| gender | String | Only accept `男性` or `女性` or `不想回答`|
| age | String | Only accept `20歲以下` or `21~40歲` or `40~65歲` or `66歲以上`|
| mole_size | String | Only accept `yes` or `no`|
| period | String | Only accept `1年以上` or `1個月～1年` or `1個月內` or `不記得`|
| change | String | Only accept `有變化` or `無變化` or `不記得`|
| fbid(Optional) | String | user id |
| fbnm(Optional) | String | user name |

* **Request Body Example:**

```
{
    "image_crop": "https://devel.dermai.com.tw/static/data/U4879646ee62667fa5faac183e2d3d1c1-fl_4y97x-201910290924_crop.jpg",
    "gender": "男性",
    "age": "40~65歲",
    "mole_size": "yes",
    "period": "1年以上",
    "change": "無變化",
    "fbid": "12345",
    "fbnm": "test"
}

or

{
    "image_crop": "1emdiaueiwq...(base64data)",
    "gender": "男性",
    "age": "40~65歲",
    "mole_size": "yes",
    "period": "1年以上",
    "change": "無變化",
    "fbid": "12345",
    "fbnm": "test"
}


```

* **Success Response: 200**

| Field | Type | Description |
| :---: | :---: | :--- |
| CheckBlurScore | Double | The confidential score for dpi if it can be used |
| CheckImageHaveMoleScore | Double | The confidential score to detact if there is a mole in picture |
| Message | String | |
| Reject | Bool | only return `true` or `false`, if true, then suggest user to take/upload another picture  |
| RiskLevel | String | only return `Higher` or `lower` to suggest user the mole is in hight risk or not |
| RiskScore | Double | The risk score of the mole  |

```
{
    "CheckBlurScore": 40.78396741810663,
    "CheckImageHaveMoleScore": 0.9970205426216125,
    "Message": "",
    "Reject": false,
    "RiskLevel": "Higher",
    "RiskScore": 0.9663519859313965
}
```