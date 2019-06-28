### 币种基本信息
1. 代码简称: IOTA
2. 英文名: MIOTA
3. 中文名: 埃欧塔
4. 市值排名: 17
5. 白皮书: https://assets.ctfassets.net/r1dr6vzfxhev/2t4uxvsIqk0EUau6g2sw0g/45eae33637ca92f85dd9f4a3a218e1ec/iota1_4_3.pdf
6. 总量信息: 2779530283277761(可能因为计量单位的问题,也有发行量为: 2779530283),不增发
7. 项目定位: IOTA是一种新型的数字加密货币，专注于解决机器与机器（M2M）之间的交易问题

### 官方资料
1. 官网: https://www.iota.org/
2. 区块链浏览器1: https://iotasear.ch/  (似乎已经停更)
3. 区块链浏览器2: https://thetangle.org/
4. 官方github地址: https://github.com/iotaledger
5. 官方技术交流群: 暂无
6. 可用节点列表: https://iota.dance/

### 测试网络
1. 区块链浏览器: https://devnet.thetangle.org/
2. 测试网节点node: https://nodes.devnet.iota.org:443
3. 测试网水龙头: https://faucet.devnet.iota.org/

### 技术架构
1. 主链最新高度: 1093682(2019年6月28日)
2. 主链出块速度: 待查
3. 区块链容量: 未知
4. 组织模型: UTXO模型
5. 共识算法: pow
6. Token支持: 不支持
7. 节点: 自行搭建节点

### API接口
1. 节点提供RestfuL-JSON API
2. API地址: https://docs.iota.org/docs/iri/0.1/references/api-reference
3. API是否支持RawData: 未知

#### 其他信息
1. IOTA节点搭建文章1: https://www.iotachina.com/conglingkaishishezhivps-iotawanzhengjiedian.html
2. IOTA节点搭建文章2: http://www.iotachina.com/vultrvpsiotanodecarriotafield.html
3. 邻居网址1: http://field.carriota.com/
4. 邻居网址2: http://field.deviota.com/
6. 发现和更新邻居: https://github.com/SemkoDev/field.cli
7. 获取节点信息
```
curl -s http://localhost:14265 -X POST -H 'X-IOTA-API-Version: 1' -H 'Content-Type: application/json' -d '{"command": "getNodeInfo"}' | jq
```

### 数据结构和数据解析
