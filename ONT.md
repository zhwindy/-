### 币种基本信息
1. 代码简称: ONT
2. 英文名: Ontology
3. 中文名: 本体网络
4. 市值排名: 20
5. 白皮书: https://ontio.github.io/documentation/wp_download_zh.html
6. 总量信息: 10亿,不增发
7. 项目定位: 新一代共有基础链项目&分布式信任协作平台,是新一代分布式信任链网

### 官方资料
1. 官网: https://ont.io/
2. 官方区块链浏览器: https://explorer.ont.io/
3. 官方github地址: https://github.com/ontio/ontology
4. 官方技术交流群: 暂无

### 技术架构
1. 区块链最新高度: 4221241
2. 出块速度: 待查
3. 区块链容量: 未知
4. 组织模型: 账户模型
5. 共识算法: VBFT,是结合PoS、VRF和BFT的全新共识算法
6. Token支持: 支持
7. 节点: 当前47个共识节点,组成共识网络(节点分为记账节点和同步节点,记账节点按照共识算法参与网络共识，产生区块。同步节点只同步记账节点生成的区块)
8. SDK: go/java/python/php等均支持

### API接口
1. 已提供RestfuL,RPC,Websocket
2. API地址: https://dev-docs.ont.io/#/docs-cn/ontology-cli/04-interface-specification
3. API是否支持RawData: 支持

#### 其他信息
1. ONT 的（小数点后）精度是 0，因此如果输入浮点数，那么小数部分将会被丢弃。
2. ONG 的（小数点后）精度是 9，因此超出小数点后 9 位的小数部分将会被丢弃。
3. RPC 接口监听在 20336 端口

### 数据结构和数据解析
交易接口参考: https://dev-docs.ont.io/#/docs-cn/ontology-cli/21-show-tx
交易id: `8a3643c447c3280dd8ea609739c8e8d89c3aaf50bd4089518dae773a992621cb`
原始数据:
```
00d11916f245f401000000000000204e0000000000005bcc5ebaac3a49c71ff15845da1ec5d6c9cca2117100c66b141ffb723601fe7bf5e78b9ec6f6c79d69e317b9c76a7cc814129c4988808ce38dc505a414e48e5083a82bf7346a7cc8526a7cc86c51c1087472616e736665721400000000000000000000000000000000000000010068164f6e746f6c6f67792e4e61746976652e496e766f6b6500024241010e453859680785febc4c4714a3177000060228fa3c70e6677f467edc3608f769db5721a5739b0b0bfa8ba57ef6aef2f80d2378e6650fe442b22722cfd0f324a1232103139a0670c02c5afda42861370e21f29f68a7bee11e7acd80cf1ab87b3efa26aeac42410126f7544c08804a50bd976b8863d51cab06ec5c49711c4a514dd943dfdd51585ce7dd8c39b8021b3f36a109419a7a0eac977b88ba093b95b91b12b19e84527ff9232103232493bdd2cc6b9f19fd2c202c2ad75af1f66f3016abb47702f90a779d16e5c9ac
```
JSON数据:
```
{
    "desc": "SUCCESS",
    "error": 0,
    "id": 1,
    "jsonrpc": "2.0",
    "result": {
        "Version": 0,
        "Nonce": 1173493273,
        "GasPrice": 500,
        "GasLimit": 20000,
        "Payer": "AQ9FxqKbXnZTqf22zy2NFcXhi13fipg48S",
        "TxType": 209,
        "Payload": {
            "Code": "00c66b141ffb723601fe7bf5e78b9ec6f6c79d69e317b9c76a7cc814129c4988808ce38dc505a414e48e5083a82bf7346a7cc8526a7cc86c51c1087472616e736665721400000000000000000000000000000000000000010068164f6e746f6c6f67792e4e61746976652e496e766f6b65"
        },
        "Attributes": [],
        "Sigs": [
            {
                "PubKeys": [
                    "03139a0670c02c5afda42861370e21f29f68a7bee11e7acd80cf1ab87b3efa26ae"
                ],
                "M": 1,
                "SigData": [
                    "010e453859680785febc4c4714a3177000060228fa3c70e6677f467edc3608f769db5721a5739b0b0bfa8ba57ef6aef2f80d2378e6650fe442b22722cfd0f324a1"
                ]
            },
            {
                "PubKeys": [
                    "03232493bdd2cc6b9f19fd2c202c2ad75af1f66f3016abb47702f90a779d16e5c9"
                ],
                "M": 1,
                "SigData": [
                    "0126f7544c08804a50bd976b8863d51cab06ec5c49711c4a514dd943dfdd51585ce7dd8c39b8021b3f36a109419a7a0eac977b88ba093b95b91b12b19e84527ff9"
                ]
            }
        ],
        "Hash": "8a3643c447c3280dd8ea609739c8e8d89c3aaf50bd4089518dae773a992621cb",
        "Height": 165453
    }
}
```
手动解析:
```
00  // version
d1  // type
1916f245  // nonce
f401000000000000  // gasprice
204e000000000000  // gaslimit
5bcc5ebaac3a49c71ff15845da1ec5d6c9cca21171  // payer
// payload code
00c66b141ffb723601fe7bf5e78b9ec6f6c79d69e317b9c76a7cc814129c4988808ce38dc505a414e48e5083a82bf7346a7cc8526a7cc86c51c1087472616e736665721400000000000000000000000000000000000000010068164f6e746f6c6f67792e4e61746976652e496e766f6b6500024241010e453859680785febc4c4714a3177000060228fa3c70e6677f467edc3608f769db5721a5739b0b0bfa8ba57ef6aef2f80d2378e6650fe442b22722cfd0f324a1232103139a0670c02c5afda42861370e21f29f68a7bee11e7acd80cf1ab87b3efa26aeac42410126f7544c08804a50bd976b8863d51cab06ec5c49711c4a514dd943dfdd51585ce7dd8c39b8021b3f36a109419a7a0eac977b88ba093b95b91b12b19e84527ff9232103232493bdd2cc6b9f19fd2c202c2ad75af1f66f3016abb47702f90a779d16e5c9ac

解析payload code

00c66b  // Nvm操作码, 参数序列化开始的标志
14  // 参数length
1ffb723601fe7bf5e78b9ec6f6c79d69e317b9c7
6a7cc8  // Nvm操作码, 第一个参数序列化完成的标志
14  // 参数length
129c4988808ce38dc505a414e48e5083a82bf734
6a7cc8  // Nvm操作码, 第二个参数序列化完成的标志
52  // 转账数量
6a7cc8  // Nvm操作码, 第三个参数序列化完成的标志
6c51c1  // Nvm操作码, 参数序列化完成的标志
08  // 方法名长度
7472616e73666572  // 方法名 transfer
14  // 合约地址长度
0000000000000000000000000000000000000001   // 合约地址：ONG
00  // version
68  // Nvm操作码
16  // 原生合约调用名长度
4f6e746f6c6f67792e4e61746976652e496e766f6b65  // 原生合约调用 "Ontology.Native.Invoke"
00  // version
02  // 签名个数
42  // total-length
41 // length
010e453859680785febc4c4714a3177000060228fa3c70e6677f467edc3608f769db5721a5739b0b0bfa8ba57ef6aef2f80d2378e6650fe442b22722cfd0f324a1  // signature
23
21
03139a0670c02c5afda42861370e21f29f68a7bee11e7acd80cf1ab87b3efa26ae  // pubkey
ac

42  // total-length
41  // length
0126f7544c08804a50bd976b8863d51cab06ec5c49711c4a514dd943dfdd51585ce7dd8c39b8021b3f36a109419a7a0eac977b88ba093b95b91b12b19e84527ff9  // signature
23
21
03232493bdd2cc6b9f19fd2c202c2ad75af1f66f3016abb47702f90a779d16e5c9  // pubkey
ac
```