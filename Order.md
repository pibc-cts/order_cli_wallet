# order_cli_wallet
orderofcli

第一条 ： 喂价命令：

publish_asset_feed init3 CNY {"settlement_price":{"base":{"amount":1100000,"asset_id":"1.3.1"},"quote":{"amount":10000000,"asset_id":"1.3.0"}},"core_exchange_rate":{"base":{"amount":1090000,"asset_id":"1.3.1"},"quote":{"amount":10000000,"asset_id":"1.3.0"}}} true

上面为重钱包喂价命令具体规格。   init3 为喂价账户   CNY 是要喂价的资产   base 是喂价目标资产  quote 为 喂价对的另一边衡量资产 当前是系统币 （CTS）。另外 asset_id 请使用对应的ID。
amount 为何会那么多0，请注意资产的小数位。 CNY 4小数位，  CTS 5小数位， 所以请删减掉 0 的位数。 再进行除法计算 CNY/CTS   110/100 最终   1.1 CNY/CTS

第二条：转账命令：

transfer2(string from, string to, string amount, string asset_symbol, string memo)
transfer2 init3 test01 20 CTS testtoxx
transfer2 init3 test01 20 CTS "testssadfas" true
上面两条在测试网都能过，但是为什么没有备注消息，我不懂。

第三条：买卖资产命令：

sell_asset(string seller_account, string amount_to_sell, string symbol_to_sell, string min_to_receive, string symbol_to_receive, uint32_t timeout_sec, bool fill_or_kill, bool broadcast)
sell_asset init3 100 CTS 200 CNY 60000000 false true
上述  卖100CTS  要求换200CNY  持续挂单时间60000000 市场上不够货则一直挂着 广播
sell_asset init3 100 CTS 200 CNY 60000000 true true
上述  卖100CTS  要求换200CNY  持续挂单时间60000000 只收市场上当前能满足的货，收完就收摊 广播 （测试网没有单子收，未实验确认成功）

第X条命令：查看可解冻资金：

 get_vesting_balances(string account_name)
 get_vesting_balances init3
 可以看到有两个资金账户可退款
 
第X条命令：取回可解冻资金 （）：

withdraw_vesting(string witness_name, string amount, string asset_symbol, bool broadcast)
withdraw_vesting init3 14 CTS true 
上面命令退14CTS 但是只是其中一个解冻账户的。 其他的账户看下面
withdraw_vesting 1.13.14 15 CTS true
上述命令退指定账户内的资金

 
 第X条命令：列出账户资产列表：
 
 list_account_balances init3
 
 导入私钥进钱包
 
 import_key "1.3.11" 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3 //这条为何要引号不清楚
 import_key init3 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3

通过brain_key注册账户

create_account_with_brain_key(string brain_key, string account_name, string registrar_account, string referrer_account, bool broadcast)
create_account_with_brain_key gg123123 test01 init3 init3 true

通过公钥注册账户

register_account(string name, public_key_type owner, public_key_type active, string registrar_account, string referrer_account, uint32_t referrer_percent, bool broadcast)
register_account "newaccount" "CORE6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV" "CORE6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV" "1.3.11" "1.3.11" 50 true


创建理事会成员

create_committee_member(string owner_account, string url, bool broadcast)
create_committee_member init3 "要显示的链接，没有也行，但是要留（""）" true

创建见证人
 create_witness(string owner_account, string url, bool broadcast)
  create_witness init3 "要显示的链接，没有也行，但是要留（""）" true
 
 获得指定账户信息
 
  get_account(string account_name_or_id)
  get_account init3
  
  查看当前注册账户总数
  
  get_account_count
 
 获得指定账户的历史信息 从最新的开始 总数几条
 
  get_account_history(string name, int limit)
  get_account_history init3 10
  
  获得指定账户的数字账号信息
  
  get_account_id(string account_name_or_id)
  get_account_id init3
  
  获得指定资产信息
  
  get_asset(string asset_name_or_id)
  get_asset CNY
  
  获得市场上的挂单 
  
  get_order_book(const string & base, const string & quote, unsigned limit)
  get_order_book CNY CTS 10
  10是查询有效条目数。
  
  获得指定见证人信息
  
get_witness(string owner_account)
get_witness init3

请求一组 密码 公钥 私钥

suggest_brain_key




  
