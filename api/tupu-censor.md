

#  图普内容审核

**POST http://api.uai.ucloud.cn/tupu/censor**

**Signature使用参数**

- Url: 请求参数Url, 若请求参数无Url,则不加入此参数
- ResourceId: header参数ResourceId
- PublicKey： header参数PublicKey
- Timestamp： header参数Timestamp


生成Signature签名算法流程包括四步：  
（1）将请求参数按照名进行升序排列；  
（2）构造被签名参数串；  
（3）计算签名；  
（4）使用签名组合HTTP请求。  

*具体内容请参考签名文档：https://docs.ucloud.cn/api/summary/signature*

**Header参数**

| 字段名 | 字段类型 | 说明 | 是否必须 |
| ------ | -------- | ---- | -------- |
| Signature | String | 签名 | 是 |
| PublicKey | String | 公钥 | 是 |
| ResourceId | String | 资源ID | 是 |
| Timestamp | Int | 当前unix时间戳 | 是 |

**请求参数（Multipart/Form-data）**

| 字段名 | 字段类型 | 说明 | 是否必须 |
| ------ | -------- | ---- | -------- |
| ProductNames  | String  | 请求的产品（产品名称, 多个以逗号隔开）例如"tupu_porn,tupu_terror,tupu_politics"，可选范围包括tupu_porn 色情识别、tupu_terror 暴恐识别、tupu_politics 敏感人物识别               | 是     |
| Method  | String  | 请求方式，可选方式： url - 传入图片url, file - 传入图片二进制  | 是     |
| Url     | String  | 图片url                                     | 否     |
| Image   | Binary  | 图片文件                                      | 否     |

**响应参数（JSON）**

| 字段名 | 字段类型 | 说明 |
| ------ | -------- | ---- |
| RetCode | Int | 返回码 |
| Message | String | 返回信息 |
| Timestamp | Int | 当前unix时间戳 |
| Results | TupuResult | 鉴别结果 |

**TupuResult**

| 字段名 | 字段类型 | 说明 |
| ------ | -------- | ---- |
| Porn        | TupuPornResult  | 色情识别结果  |
| Terror      | TupuTerrorResult  | 暴恐识别结果  |
| Politician  | []TupuPoliticsResult  | 敏感人物识别结果  |

**TupuPornResult**

| 字段名 | 字段类型 | 说明 |
| ------ | -------- | ---- |
| Label | int | 0-色情 1-性感 2-正常 |
| Review | bool | 是否需要人工review true/false |

**TupuTerrorResult**

| 字段名 | 字段类型 | 说明 |
| ------ | -------- | ---- |
| Label | int | 0-正常 1-特殊着装人物 2-特殊符号 3-武器或持武器者 4-血腥场景 5-暴乱场景 6-战争场景 |
| Review | bool | 是否需要人工review true/false |

**TupuPoliticsResult**

| 字段名 | 字段类型 | 说明 |
| ------ | -------- | ---- |
| Label | int | 0-政治人物 2-非政治人物 3-无人脸 |
| Review | bool | 是否需要人工review true/false |
| FacePosition | [][]int | 人脸框四点位置，顺序为左上，右上，右下，左下，顺时针，横坐标为宽的比例，纵坐标为高的比例，例：[0.57 0.2768595041322314] [0.7175 0.2768595041322314] [0.7175 0.5206611570247934] [0.57 0.5206611570247934]，无人脸时此字段为空 |