# AwesomeTickets API

<!-- MarkdownTOC -->

- [返回状态说明](#返回状态说明)
- [获取电影信息](#获取电影信息)
- [获取正在上映电影列表](#获取正在上映电影列表)
- [获取即将上映电影列表](#获取即将上映电影列表)
- [获取首页大尺寸海报](#获取首页大尺寸海报)

<!-- /MarkdownTOC -->

<a name="返回状态说明"></a>
## 返回状态说明

AwesomeTickets API 通过 HTTP Status Code 来说明 API 请求是否成功，下面的表格中展示了可能的 HTTP Status Code 以及其含义：

| Code | Content | Description |
|------|---------|-------------|
|200|OK|请求成功|
|400|BAD REQUEST|请求的地址不存在或者包含不支持的参数|
|403|FORBIDDEN|被禁止访问|
|404|NOT FOUND|请求的资源不存在|
|500|INTERNAL SERVER ERROR|内部错误|

<a name="获取电影信息"></a>
## 获取电影信息

Request URL:

```
GET /resource/movie/:id
```

Response Properties:

| Property | Description | Type |
|----------|-------------|------|
|id|电影id|int|
|title|标题|string|
|pubdate|上映日期（年/月/日）|string|
|length|时长（分钟）|int|
|rating|评分|float|
|posterSmall|海报（小尺寸）URL|string|
|posterLarge|海报（大尺寸）URL|string|
|country|制片国家|string|
|movieStatus|上映状态（正在上映->"on"，即将上映->"soon"）|string|
|movieType|类型（"2D"，"3D"，"3D IMAX"）|string|
|movieStyle|题材|string array|

Response Example:

```json
{
    "id": "170458",
    "title": "美女与野兽",
    "pubdate": "2017-03-17",
    "length": 130,
    "rating": 8.2,
    "posterSmall": "http://xxx.com/image1.png",
    "posterLarge": "http://xxx.com/image2.png",
    "country": "美国",
    "movieStatus": "on",
    "movieType": "3D IMAX",
    "movieStyle": ["爱情", "奇幻", "歌舞"]
}
```

<a name="获取正在上映电影列表"></a>
## 获取正在上映电影列表

Request URL:

```
GET /resource/movie/on_show
```

Response Properties:

| Property | Description | Type |
|----------|-------------|------|
|count|电影数量|int|
|movies|电影 id 数组|int array|

Response Example:

```json
{
    "count": 3,
    "movies": [146522, 246653, 397864]
}
```

<a name="获取即将上映电影列表"></a>
## 获取即将上映电影列表

Request URL:

```
GET /resource/movie/coming_soon
```

Response Properties:

| Property | Description | Type |
|----------|-------------|------|
|count|电影数量|int|
|movies|电影 id 数组|int array|

Response Example:

```json
{
    "count": 2,
    "movies": [132546, 289765]
}
```

<a name="获取首页大尺寸海报"></a>
## 获取首页大尺寸海报

Request URL:

```
GET /resource/movie/popular?count=XXX
```

Request Parameters:

| Param | Description | Default |
|-------|-------------|---------|
|count|海报数量|3|

Response Properties:

| Property | Description | Type |
|----------|-------------|------|
|count|海报数量|int|
|subjects|（电影id，海报链接）二元组数组|array|

Response Example:

```json
{
    "count": 3,
    "subjects": [
        {
            "id": 154685,
            "posterURL": "http://xxx.com/image1.png"
        },
        {
            "id": 164597,
            "posterURL": "http://xxx.com/image2.png"
        },
        {
            "id": 197682,
            "posterURL": "http://xxx.com/image3.png"
        }
    ]
}
```