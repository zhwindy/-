#### 币种基本信息
1. 代码简称: NAS
2. 英文名: Nebulas
3. 中文名: 星云链
4. 市值排名: 93
5. 技术白皮书: https://nebulas.io/docs/NebulasTechnicalWhitepaperZh.pdf
6. 非技术白皮书: https://nebulas.io/docs/NebulasWhitepaperZh.pdf
6. 总量信息: 1亿,不增发
7. 项目定位: 协作的自治元网络

#### 官方资料
1. 官网: https://nebulas.io/cn/index.html
2. 官方区块链浏览器: https://explorer.nebulas.io/#/
3. 官方github地址: https://github.com/nebulasio/go-nebulas
4. 官方技术交流群: 微信

#### 技术架构
1. 区块链最新高度: 2431447
2. 出块速度: 15s
3. 区块链容量: 未知
4. 组织模型: 账户模型
5. 共识算法: DPOS, 总共有21个矿工，每个矿工会轮流每15s出一个新区块
6. Token支持: 支持,NRC20,NRC721
7. 节点: 按朝代更替,每个朝代21个节点轮流出块(目前只有1个朝代)
8. SDK: go/java/python/php等均支持

#### API接口
1. 提供: RPC和HTTP接口
2. API服务器地址: 52.76.103.107, 52.56.55.238, 34.198.52.191
3. API列表: https://github.com/nebulasio/wiki/blob/master/rpc.md#getaccountstate
4. API是否支持RawData: 不支持

#### 其他信息
1. 每个区块和交易只会属于一条唯一的链，保证安全性.对于主网，chain_id=1；对于测试网，chain_id=1001
2. RPC接口默认端口: 8684
3. HTTP接口默认端口: 8685

### 数据结构和数据解析
1. 交易结构定义
```
message Data {
    string payload_type = 1;
    bytes payload = 2;
}

message Transaction {
    bytes hash  = 1;
    bytes from = 2;
    bytes to = 3;
    bytes value = 4;
    uint64 nonce = 5;
    int64 timestamp = 6;
    Data data = 7;
    uint32 chain_id = 8;
    bytes gas_price = 9;
    bytes gas_limit = 10;

    uint32 alg = 11;
    bytes sign = 12;
}
```
2. Transaction交易数据
* 构建数据
```
chain_id: 1001
from: n1H2Yb5Q6ZfKvs61htVSV4b1U2gr2GA9vo6
to: n1JmhE82GNjdZPNZr6dgUuSfzy2WRwmD9zy
gasPrice: 1000000
gasLimit: 20000
value: 0
nonce: 159
timestamp: 1559027767821
hash: eda5f5bb94ae082a43144c321c9b658602ff2189267bea38508a79126644aa93
data: {payload_type: "binary", payload: "test"}
alg: 1
sign: b37f9592036431eb14cd46adce104cb20de0954cf2257547b1b392c54a80fc841d8c7988e8450646fbc86e67441f8e542ff37c31aaccd599977e2e65cfa8014d01
```
* rawData
```
0a20eda5f5bb94ae082a43144c321c9b658602ff2189267bea38508a79126644aa93121a19571b8df1d7065d1f9c36a9dec6d736d252c065b13e39b163d51a1a19572eaf2b0607105087808278ca2f90ea6df9d9a8eab02c3a22221000000000000000000000000000000000289f01308db4afeaaf2d3a0e0a0662696e61727912047465737440e9074a10000000000000000000000000000f4240521000000000000000000000000000004e2058016241b37f9592036431eb14cd46adce104cb20de0954cf2257547b1b392c54a80fc841d8c7988e8450646fbc86e67441f8e542ff37c31aaccd599977e2e65cfa8014d01
```
* 手动解析
```
0a  // hash-tag
20  // hash-length
eda5f5bb94ae082a43144c321c9b658602ff2189267bea38508a79126644aa93  // hash

12  // from-tag
1a // from-length
19571b8df1d7065d1f9c36a9dec6d736d252c065b13e39b163d5  // from

1a  // to-tag
1a  // to-length
19572eaf2b0607105087808278ca2f90ea6df9d9a8eab02c3a22  // to

22  // value-tag
10  // value-length
00000000000000000000000000000000  // value

28  // nonce-tag
9f01  // nonce --> 000000010011111 --> 159

30 // timestamp-tag
8db4afeaaf2d  // timestamp --> 100011011011010010101111111010101010111100101101 -->  0010110101011111101010010111101101000001101 --> 1559027767821

3a  // data-tag
0e  // data-length
0a0662696e617279120474657374  // data

40  // chain_id-tag
e907  // chain_id --> 1110100100000111 --> 000001111101001  --> 1001

4a  // gasprice-tag
10  // gasprice-length
000000000000000000000000000f4240  // gasprice

52  // gaslimit-tag
10  // gaslimit-length
00000000000000000000000000004e20  // gaslimit

58  // alg-tag
01  // alg

62  //  sign-tag
41  // sign-length
b37f9592036431eb14cd46adce104cb20de0954cf2257547b1b392c54a80fc841d8c7988e8450646fbc86e67441f8e542ff37c31aaccd599977e2e65cfa8014d01  // sign
```