# 动态累加SQL

---

## 获取金额多条数据累加值不超过输入值
```
SELECT 
  t.* 
FROM
  (SELECT 
    user_recharge_address.*,
    (@sum := @sum + `balance`) AS cumulative_balance 
  FROM
    `user_recharge_address`,
    (SELECT @sum := 0) params 
  WHERE coin_code = 'BTC' ORDER BY `balance` DESC, `ID`) t 
WHERE cumulative_balance <= 10 OR (cumulative_balance > 10 AND cumulative_balance - balance < 10)
```

## 例子
### 创建表
```
CREATE TABLE `user_recharge_address` (
  `ID` INT(11) NOT NULL AUTO_INCREMENT COMMENT '记录id，自增长',
  `user_id` INT(11) NOT NULL COMMENT '用户ID',
  `coin_code` VARCHAR(6) NOT NULL COMMENT '币种，RMB-人民币  BTC-比特币 ETH-以太币',
  `url` VARCHAR(42) NOT NULL COMMENT '充值地址',
  `balance` DECIMAL(20,8) DEFAULT '0.00000000' COMMENT '余额',
  `blocked` DECIMAL(20,8) DEFAULT '0.00000000' COMMENT '冻结额',
  `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  PRIMARY KEY (`ID`)
) ENGINE=INNODB DEFAULT CHARSET=utf8 COMMENT='用户充币地址表';
```

### 添加测试数据
```
INSERT INTO `user_recharge_address` (`ID`, `user_id`, `coin_code`, `url`, `balance`, `blocked`, `create_time`) VALUES('1','6','BTC','123456_test','3.00000000','0.00000000','2017-09-15 10:35:44');
INSERT INTO `user_recharge_address` (`ID`, `user_id`, `coin_code`, `url`, `balance`, `blocked`, `create_time`) VALUES('11','2','BTC','123456_test1','1.00000000','0.00000000','2017-09-15 10:35:44');
INSERT INTO `user_recharge_address` (`ID`, `user_id`, `coin_code`, `url`, `balance`, `blocked`, `create_time`) VALUES('12','3','BTC','123456_test12','3.00000000','0.00000000','2017-09-15 10:35:44');
INSERT INTO `user_recharge_address` (`ID`, `user_id`, `coin_code`, `url`, `balance`, `blocked`, `create_time`) VALUES('13','11','BTC','123456_test121','3.00000000','0.00000000','2017-09-15 10:35:44');
INSERT INTO `user_recharge_address` (`ID`, `user_id`, `coin_code`, `url`, `balance`, `blocked`, `create_time`) VALUES('14','12','BTC','123456_test1211','1.00000000','0.00000000','2017-09-15 10:35:44');
INSERT INTO `user_recharge_address` (`ID`, `user_id`, `coin_code`, `url`, `balance`, `blocked`, `create_time`) VALUES('4','1','BTC','XXXX','3.00000000','0.00000000','2017-09-15 11:01:54');

```




