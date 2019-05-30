#### 币种基本信息
1. 代码简称: TRX
2. 英文名: TRON
3. 中文名: 波场
4. 市值排名: 11
5. 技术白皮书: https://tron.network/static/doc/white_paper_v_2_0.pdf
6. 总量信息: 1000亿, 不增发, 代币分配方案:40%公开发售，15%私募，35%属于TRON基金会和相关生态系统，剩余10%份额归属早期支持的陪我公司
7. 项目定位: 波场TRON是全球最大的区块链去中心化应用操作系统
8. 代币锁仓: TRON有相关锁仓计划，基金会公布了持币地址，所持代币锁仓至2020年

#### 官方资料
1. 官网: https://tron.network/index?lng=zh
2. 官方区块链浏览器: https://tronscan.org/#/
3. 官方github地址: https://github.com/tronprotocol
4. 官方技术交流群: 微信交流群

#### 技术架构
1. 区块链最新高度: 9675290
2. 出块速度: 3s
3. 区块链容量: 未知
4. 组织模型: 账户模型
5. 共识算法: 改进版的DPOS, 共27个超级节点负责共识与出块
6. Token支持: 支持,TRC-10, TRC-20
7. 节点: 27个超级节点轮流出块
8. SDK: go/java/python/php等均支持

#### API接口
1. 提供: RPC和HTTP接口
2. API服务器列表: https://github.com/tronprotocol/Documentation/blob/master/TRX_CN/Official_Public_Node.md
3. HTTP接口文档: https://github.com/tronprotocol/documentation/blob/master/TRX_CN/Tron-http.md
4. API是否支持RawData: 部分支持

#### 其他信息
1. 节点分为三种
    * 超级节点SuperNode
    * 全节点fullNode
    * 固化节点solidityNode
2. RPC接口默认端口: 50051
3. HTTP接口默认端口
    * fullNode是 8090
    * solidityNode是 8091

### 数据结构和数据解析
1. 交易结构定义: https://github.com/tronprotocol/protocol/blob/master/core/Tron.proto
```
message raw {
    bytes ref_block_bytes = 1;
    int64 ref_block_num = 3;
    bytes ref_block_hash = 4;
    int64 expiration = 8;
    repeated authority auths = 9;
    // data not used
    bytes data = 10;
    //only support size = 1,  repeated list here for extension
    repeated Contract contract = 11;
    // scripts not used
    bytes scripts = 12;
    int64 timestamp = 14;
    int64 fee_limit = 18;
  }
```
2. Transaction交易数据
* 交易ID: `9d67598c8b90336fb876efc7a2b7b78534dab94a802baf481632c17bae11ce2e`
* JSON数据:
```
{
    "ret": [
        {
            "contractRet": "SUCCESS"
        }
    ],
    "signature": [
        "4a05a7fd8e223afc0694ca52f5a292f88117aeaf73b556b56f63568a9903b70f5240e64c217ef841603fd09e4c87b5803aec386d5be115fa7baeb2df6604580301"
    ],
    "txID": "9d67598c8b90336fb876efc7a2b7b78534dab94a802baf481632c17bae11ce2e",
    "raw_data": {
        "contract": [
            {
                "parameter": {
                    "value": {
                        "amount": 99000000,
                        "owner_address": "4179309abcff2cf531070ca9222a1f72c4a5136874",
                        "to_address": "41a2d3cb65d9c05da645a0206304d8ef7d7e67f82c"
                    },
                    "type_url": "type.googleapis.com/protocol.TransferContract"
                },
                "type": "TransferContract"
            }
        ],
        "ref_block_bytes": "24f0",
        "ref_block_hash": "05c43724590c6646",
        "expiration": 1551762696000,
        "timestamp": 1551759039537
    },
    "raw_data_hex": "0a0224f0220805c43724590c664640c0ce8ee2942d5a68080112640a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412330a154179309abcff2cf531070ca9222a1f72c4a5136874121541a2d3cb65d9c05da645a0206304d8ef7d7e67f82c18c0bd9a2f70b1b8afe0942d"
}
```
* rawData
```
0a0224f0220805c43724590c664640c0ce8ee2942d5a68080112640a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412330a154179309abcff2cf531070ca9222a1f72c4a5136874121541a2d3cb65d9c05da645a0206304d8ef7d7e67f82c18c0bd9a2f70b1b8afe0942d
```
* 手动解析
```
0a  // ref_block_bytes-tag
02  // ref_block_bytes-length
24f0  //ref_block_bytes

22  // ref_block_hash-tag
08  // ref_block_hash-length
05c43724590c6646  // ref_block_hash

40  // expiration-tag 
c0ce8ee2942d  // expiration --> 00101101 10010100 11100010 10001110 11001110 11000000 --> 0010110100101001100010000111010011101000000 --> 1551762696000

5a  // contract-tag
68  // contract-length
080112640a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412330a154179309abcff2cf531070ca9222a1f72c4a5136874121541a2d3cb65d9c05da645a0206304d8ef7d7e67f82c18c0bd9a2f

70 // timestamp-tag
b1b8afe0942d  // timestamp --> 00101101 10010100 11100000 10101111 10111000 10110001 --> 0010110100101001100000010111101110000110001 --> 1551759039537
```

* 合约结构定义: https://github.com/tronprotocol/protocol/blob/master/core/Contract.proto

* contract 手动解析
```
08  // ContractType-tag 
01  // ContractType

12  // tag
64  // length

0a  // owner_address-tag
2d  // owner_address-length
747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e7472616374  // owner_address

12  // to_address-tag
33  // to_address-length
0a154179309abcff2cf531070ca9222a1f72c4a5136874121541a2d3cb65d9c05da645a0206304d8ef7d7e67f82c18c0bd9a2f  // to_address
```