Transaction的bitconin源代码
=
./src

源代码解读
=
1. https://blog.csdn.net/pure_lady/article/details/77771392
2. https://juejin.im/post/5ae0738bf265da0b851c88ff
3. https://zhuanlan.zhihu.com/p/27512347
4. https://zhuanlan.zhihu.com/p/35684664
   
脚本系统
=
1. https://zhuanlan.zhihu.com/p/33157713

bitCoin源码
=
- CTransaction(代表交易) 
    ```c++
    public：
    //代表收入,一个CTxIn的列表
    const std::vector<CTxIn> vin;
    //代表支出，一个CTxOut的列表
    const std::vector<CTxOut> vout;
    //比特币version（分叉有关）
    const int32_t nVersion;
    //约定时间（过期无效？）
    const uint32_t nLockTime;
    private:
    /** Memory only. */
    //以下两个，只存在于内存，用于隔离见证
    const uint256 hash;
    const uint256 m_witness_hash;
    ```
- CTxin
    ```c++
  class CTxIn{
    public:
        //指向上一个TxPoint节点，本TXin来源,即CTxOut
        COutPoint prevout;
        //代表一个script（区块链上面），用于解锁
        CScript scriptSig;
        //软分叉，v0.1没用
        unsigned int nSequence;
        //支持一个叫隔离见证的比特币应用，默认不使用
        CScriptWitness scriptWitness; //!< Only serialized through CTransaction
    };  
    ```
- CtxOut    duiying
    ```C++
    class CTxOut{
    public:
        //表示付多少钱
        int64 nValue;
        //script 加锁（表示付给谁，加锁）
        CScript scriptPubKey;
    };
    ```
- Edgence Tansaction    
  =
  ```python
    #对应std::vector<CTxIn> vin
    txins: Iterable[TxIn]
    #对应std::vector<CTxOut> vout
    txouts: Iterable[TxOut]
    #对应uint32_t nLockTime;
    locktime: int = None
    #暂无版本控制以及private中用于隔离验证代码
  ```  
- Edgence TxIn
  =
  ```python
    #对应COutPoint prevout
    to_spend: Union[OutPoint, None]
    #对应Scrpt，但是区别比较大
    unlock_sig: bytes
    unlock_pk: bytes
    # 对应unsigned int nSequence;
    sequence: int
  ```
- Edgence TxOut
  =
  ```python
    #对应int64 nValue;
    value: int
    #对应CScript scriptPubKey，与比特币有区别
    to_address: str
  ```
- 综上
  =
  1. Edgence 字段与比特币高度一致,但Edgence不支持隔离见证（比特币中多个隔离见证的字段均未添加）
  2. 在transaction类中，无版本控制字段
  3. 比特币中指向付款节点的指针COutPoint prevout在我们系统中为 to_spend: Union[OutPoint, None]，可能是系统实现的关系？
  4. Txin与TxOut中，比特币由一个script类提供脚本验证支持，我们目前使用的。。。字符串？


