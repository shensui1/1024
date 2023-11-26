# 文档

### 概念


1、**公平分配**：是一种公平发射的铭文代币协议，每个人都可以公平参与。  
2、**余额记账**：通过余额记账的方式让转移更加灵活方便，节省gas。   
3、**公开透明**：在市场发布之后，我们会公开我们节点的同步方式，通过npm包的形式让大家可以监督记账的公平性。  
4、**节点共识**：在市场稳定之后，我们会采取共识节点的方式来验证所有节点的数据安全，以及数据准确性。 

### 约定
1、mint代币只能from=to  
2、不支持合约批量铸造  
3、将不再记录mint hash  
### 规范
1、**Deploy**：用于部署Inscription协议代币  
2、**Mint**：用于铸造Inscription协议代币  
3、**transfer**：用于转移Inscription协议代币  
4、**deposit**：用于Inscription质押触发的event  
4、**contractTransfer**：用于Inscription协议合约内部代币转出触发的event   
5、**proxyDeposit**：用于Inscription协议合约内部余额转质押触发的event    
### Deploy
```cpp
data:,{"a":"Inscription","p":"prc-20","op":"deploy","tick":"1024","max":"210000","lim":"100"}
```
| Key | Required? | Desc |
| :-----| :----  | ----: |
| a | yes | Inscription |
| p | yes | 代币协议          |
| op | yes | 操作类型deploy   |
| tick | yes | 代币名称       |
| max  | yes | 代币总量，必须是lim的倍数       |
| lim  | yes | mint代币数量限制       |

### Mint
```cpp
data:,{"a":"Inscription","p":"prc-20","op":"mint","tick":"1024","amt":"100"}
```
| Key | Required? | Desc |
| :-----| :----  | ----: |
| a | yes | Inscription |
| p | yes | 代币协议          |
| op | yes | 操作类型mint  |
| tick | yes | 代币名称      |
| amt  | yes | mint数量  |

### transfer
```cpp
data:,{"a":"NextInscription","p":"prc-20","op":"transfer","tick":"1024","amt":"100"}
```
| Key | Required? | Desc |
| :-----| :----  | ----: |
| a | yes | Inscription |
| p | yes | 代币协议          |
| op | yes | 操作类型transfer  |
| tick | yes | 代币名称      |
| amt  | yes | transfer数量  |
### deposit
```cpp
event deposit(
    bytes32 indexed collectionId,
    address indexed from,
    uint256 indexed amount 
);
//用于质押铭文代币给合约。
```
### contractTransfer
```cpp
event contractTransfer(
    bytes32 indexed collectionId,
    address indexed receive,
    uint256 indexed amount 
);
//合约内部代币转移，用于合约转账。
```
### proxyDeposit
```cpp
event contractTransfer(
    bytes32 indexed collectionId,
    address indexed from,
    address indexed to,
    uint256 amount 
);
//合约内部代币转质押。
```
