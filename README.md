# china_area_mysql
## 中国5级行政区域mysql库

  爬取国家统计局官网的行政区域数据,包括省市县镇村5个层级;
  
  港澳地区的数据只有3级;台湾地区4级;
  
  包含大陆地区的邮政编码和经纬度信息.
  
---------------------------------------
#####  cnarea20171031.7z是爬取2017年的数据,截止2017年10月31日.

  全部共 **778937** 条  
  - 大陆数据共**720988** 条,其中
     - 省/直辖市 `31`
     - 市/州 `343`
     - 县/区 `3364`
     - 乡/镇 `44666`
     - 村/社区 `672584`
     
  - 港澳台数据共**57949** 条,其中
     - 省/特区 `3`
     - 港澳辖区 `33`
     - 台湾市/县 `23`
     - 台湾区/镇 `370`
     - 台湾街道/村 `57522`  
  
  - 改动:  
    - 2017比2016的数据多了26703条记录
    - 修正了大陆地区乡村级经纬度的准确度 [#21](https://github.com/kakuilan/china_area_mysql/issues/21)
    - 修正了台湾地区部分记录的经纬度 [#27](https://github.com/kakuilan/china_area_mysql/issues/27)
### 表结构

```mysql

CREATE TABLE `cnarea_2017` (
  `id` mediumint(7) unsigned NOT NULL AUTO_INCREMENT,
  `parent_id` mediumint(7) unsigned NOT NULL DEFAULT '0' COMMENT '父级ID',
  `level` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '层级',
  `area_code` bigint(12) unsigned NOT NULL DEFAULT '0' COMMENT '行政代码',
  `zip_code` mediumint(6) unsigned zerofill NOT NULL DEFAULT '000000' COMMENT '邮政编码',
  `city_code` char(6) NOT NULL DEFAULT '' COMMENT '区号',
  `name` varchar(50) NOT NULL DEFAULT '' COMMENT '名称',
  `short_name` varchar(50) NOT NULL DEFAULT '' COMMENT '简称',
  `merger_name` varchar(50) NOT NULL DEFAULT '' COMMENT '组合名',
  `pinyin` varchar(30) NOT NULL DEFAULT '' COMMENT '拼音',
  `lng` decimal(10,6) NOT NULL DEFAULT '0.000000' COMMENT '经度',
  `lat` decimal(10,6) NOT NULL DEFAULT '0.000000' COMMENT '纬度',
  PRIMARY KEY (`id`),
  KEY `idx_lev` (`level`,`parent_id`) USING BTREE
) ENGINE=MyISAM DEFAULT CHARSET=utf8 COMMENT='中国行政地区表';

```
