
# 当前TCPServer.py可以处理的请求
1. getTx可以使用TxStatusReq，目前这个api似乎不受支持了，不过哪按照代码指示，是根据transaction id获取transaction属性的函数
2. getTXPool暂无具体实现函数，目前似乎xmr也给这个api换名字了变成了get_txpool_backlog，这个api是获取当前tx的log
3. getBlock暂无具体实现函数，本项目中有一个TopBlockReq处理对最高点block的请求，但是不能根据hash值返回具体block
4. blockstats，实现一个getinfo_data的请求，暂无实现函数。<br/>getinfo_data是一个获取当前区块链状态的函数，如高度等信息.<br/>xmr初始项目api文档可以在[apiDoc](https://src.getmonero.org/resources/developer-guides/daemon-rpc.html#get_block)找到，目前发现blockstatus的返回异常复杂，我们可以根据具体使用到的内容进行支持,获取当前项目使用值需要阅读jinja模板。