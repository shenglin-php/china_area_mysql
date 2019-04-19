# china_area_mysql
## 中国5级行政区域mysql库

  爬取国家统计局官网的行政区域数据,包括省市县镇村5个层级;
  
  港澳地区的数据只有3级;台湾地区4级;
  
  包含大陆地区的邮政编码和经纬度信息.
  
---------------------------------------
#####  cnarea20181031.7z是爬取2018年的数据,截止2018年10月31日.

  全部共 **778092** 条  
  - 大陆数据共**713479** 条,其中
     - 省/直辖市 `31`
     - 市/州 `343`
     - 县/区 `3359`
     - 乡/镇 `44706`
     - 村/社区 `665040`
     
  - 港澳台数据共**64613** 条,其中
     - 省/特区 `3`
     - 港澳辖区 `33`
     - 台湾市/县 `23`
     - 台湾区/镇 `371`
     - 台湾街道/村 `64185`  
  
  - 改动:   
    - 调整了数据表结构,parent_id改为parent_code
    - 2018比2017的数据少了845条记录
    - 具体说明见 [#33](https://github.com/kakuilan/china_area_mysql/issues/33)

### 表结构

```mysql

CREATE TABLE `cnarea_2018` (
  `id` mediumint(7) unsigned NOT NULL AUTO_INCREMENT,
  `level` tinyint(1) unsigned NOT NULL COMMENT '层级',
  `parent_code` bigint(14) unsigned NOT NULL DEFAULT '0' COMMENT '父级行政代码',
  `area_code` bigint(14) unsigned NOT NULL DEFAULT '0' COMMENT '行政代码',
  `zip_code` mediumint(6) unsigned zerofill NOT NULL DEFAULT '000000' COMMENT '邮政编码',
  `city_code` char(6) NOT NULL DEFAULT '' COMMENT '区号',
  `name` varchar(50) NOT NULL DEFAULT '' COMMENT '名称',
  `short_name` varchar(50) NOT NULL DEFAULT '' COMMENT '简称',
  `merger_name` varchar(50) NOT NULL DEFAULT '' COMMENT '组合名',
  `pinyin` varchar(30) NOT NULL DEFAULT '' COMMENT '拼音',
  `lng` decimal(10,6) NOT NULL DEFAULT '0.000000' COMMENT '经度',
  `lat` decimal(10,6) NOT NULL DEFAULT '0.000000' COMMENT '纬度',
  PRIMARY KEY (`id`),
  UNIQUE KEY `idx` (`area_code`) USING BTREE
) ENGINE=MyISAM DEFAULT CHARSET=utf8 COMMENT='中国行政地区表';

```
