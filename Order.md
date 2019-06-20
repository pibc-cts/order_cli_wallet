# order_cli_wallet
orderofcli

第一条 ： 喂价命令：
publish_asset_feed init3 CNY {"settlement_price":{"base":{"amount":1100000,"asset_id":"1.3.1"},"quote":{"amount":10000000,"asset_id":"1.3.0"}},"core_exchange_rate":{"base":{"amount":1090000,"asset_id":"1.3.1"},"quote":{"amount":10000000,"asset_id":"1.3.0"}}} true

上面为重钱包喂价命令具体规格。   init3 为喂价账户   CNY 是要喂价的资产   base 是喂价目标资产  quote 为 系统币 （CTS）。
amount 为何会那么多0，请注意资产的小数位。 CNY 4小数位，  CTS 5小数位， 所以请删减掉 0 的位数。 再进行除法计算 CNY/CTS   110/100 最终   1.1 CNY/CTS
