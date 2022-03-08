# MQTT 3.1.1 协议

## 确认连接 CONNACK

###  固定报头

**固定位** 10

**剩余长度字段** 固定报头之后的所有字段长度（16进制） XX

### 可变报头

**协议名** 00 04 4D 51 54 54

**协议版本** 04

**连接标志** C2 

**KeepAlive时长** 00 64 (100秒)

### 载荷

长度 + HEX内容

**mqttclientId** xx xx CONTENT={${clientId}|securemode=3,signmethod=hmacsha1|}

**mqttUsername** xx xx CONTENT={￥{DeviceName}&￥{ProductKey}}

**mqttPassword ** xx xx CONTENT={clientId￥{clientId}deviceName￥{devicename}productKey￥{productKey}}，通过DeviceSecret进行hmacsha1加密 地址：http://encode.chahuo.com/

### 应答 - 服务端

20 02 00 00

#### *示例*

``` javascript
{
  "ProductKey": "a1ji0qFv6Jf",
  "DeviceName": "STC15",
  "DeviceSecret": "bc0834e2beeb03d37eeb7361cc387918"
}
```

得到阿里云IOT三元组产品信息后，转换为MQTT连接参数，假设clientId为10001

> mqttclientId = 10001|securemode=3,signmethod=hmacsha1|
>
> mqttUsername = STC15&a1ji0qFv6Jf
>
> mqttPassword = clientId10001deviceNameSTC15productKeya1ji0qFv6Jf
>
> mqttPassword(hmacsha1) = 4756856f5bc65bbbabc7a826d73de282ff87090d

10 70 00 04 4D 51 54 54 04 C2 00 64 00 27 31 30 30 30 31 7C 73 65 63 75 72 65 6D 6F 64 65 3D 33 2C 73 69 67 6E 6D 65 74 68 6F 64 3D 68 6D 61 63 73 68 61 31 7C 00 11 53 54 43 31 35 26 61 31 6A 69 30 71 46 76 36 4A 66 00 28 34 37 35 36 38 35 36 66 35 62 63 36 35 62 62 62 61 62 63 37 61 38 32 36 64 37 33 64 65 32 38 32 66 66 38 37 30 39 30 64

应答为 20 02 00 00



**注意剩余长度超过128后：** <length> + <length/128> 

## 发布消息 PUBLISH (等级0)

###  固定报头

**固定位** 30

**剩余长度字段** 固定报头之后的所有字段长度（16进制） XX

### 可变报头

**TOPIC** xx xx CONTENT

### 载荷

CONTENT(无需长度)

### 示例

TOPIC: /sys/a1ji0qFv6Jf/STC15/thing/event/property/post

PayLoad: {"id":"15","version":"1.0","params":{"Temp": 02,"Hum": 02,"Gas": 02},"method":"thing.event.property.set"}

 30 98 01 00 30 2F 73 79 73 2F 61 31 6A 69 30 71 46 76 36 4A 66 2F 53 54 43 31 35 2F 74 68 69 6E 67 2F 65 76 65 6E 74 2F 70 72 6F 70 65 72 74 79 2F 70 6F 73 74 7B 22 69 64 22 3A 22 31 37 22 2C 22 76 65 72 73 69 6F 6E 22 3A 22 31 2E 30 22 2C 22 70 61 72 61 6D 73 22 3A 7B 22 54 65 6D 70 22 3A 20 36 2C 22 48 75 6D 22 3A 20 36 2C 22 47 61 73 22 3A 20 36 7D 2C 22 6D 65 74 68 6F 64 22 3A 22 74 68 69 6E 67 2E 65 76 65 6E 74 2E 70 72 6F 70 65 72 74 79 2E 73 65 74 22 7D

## 发布消息 PUBLISH (等级1)

###  固定报头

**固定位** 32

**剩余长度字段** 固定报头之后的所有字段长度（16进制） XX

### 可变报头

**TOPIC** xx xx CONTENT

**报文标识符** 00 iD

### 载荷

CONTENT(无需长度)

### 响应 - 服务端

40 02 00 iD

### 失败响应

第一位不是40，下次发布固定报头固定位为3A

### *示例*

> /a1ji0qFv6Jf/STC15/user/temp

32 29 00 1C 2F 61 31 6A 69 30 71 46 76 36 4A 66 2F 53 54 43 31 35 2F 75 73 65 72 2F 74 65 6D 70+CONTENT

## 订阅 SUBSCRIBE

###  固定报头

**固定位** 82

**剩余长度字段** 固定报头之后的所有字段长度（16进制） XX

### 可变报头

00 0A

### 载荷

TOPIC长度 + TOPIC内容HEX

**TOPIC** xx xx 

**QoS** 服务质量等级 00 - 无需认证 01 - 认证一次 02 - 至少认证一次

## 订阅确认 SUBSCRIBE

###  固定报头

**固定位** 90

**剩余长度字段** 固定报头之后的所有字段长度（16进制） 03

### 可变报头

00 XX（ID）

### 载荷

**成功** 服务质量等级 00 - 无需认证 01 - 认证一次 02 - 至少认证一次 （阿里云只回01）

**失败** 08

## 取消订阅 UNSUBSCRIBE

###  固定报头

**固定位** A2

**剩余长度字段** 固定报头之后的所有字段长度（16进制） XX

### 可变报头

00 0A

### 载荷

TOPIC长度 + TOPIC内容HEX

**TOPIC** xx xx 

## 取消订阅确认 SUBSCRIBE

###  固定报头

**固定位** B0

**剩余长度字段** 固定报头之后的所有字段长度（16进制） 02

### 可变报头

00 XX（ID）

## 确认存活 PING

C0 00

**响应** D0 00

## 断开 DISCONNECT 

E0 00

## 消息获取

TOPIC： sys/a1ji0qFv6Jf/STC15/thing/event/property/post

PayLoad： {"method":"thing.service.property.set","id":"934414241","params":{"Light":1},"version":"1.0.0"}

30 92 01 

00 31 2F 73 79 73 2F 61 31 6A 69 30 71 46 76 36 4A 66 2F 53 54 43 31 35 2F 74 68 69 6E 67 2F 73 65 72 76 69 63 65 2F 70 72 6F 70 65 72 74 79 2F 73 65 74 

7B 22 6D 65 74 68 6F 64 22 3A 22 74 68 69 6E 67 2E 73 65 72 76 69 63 65 2E 70 72 6F 70 65 72 74 79 2E 73 65 74 22 2C 22 69 64 22 3A 22 39 33 34 34 31 34 32 34 31 22 2C 22 70 61 72 61 6D 73 22 3A 7B 22 4C 69 67 68 74 22 3A 31 7D 2C 22 76 65 72 73 69 6F 6E 22 3A 22 31 2E 30 2E 30 22 7D 