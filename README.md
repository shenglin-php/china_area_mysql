# china_area_mysql
## 中国5级行政区域mysql库

  爬取国家统计局官网的行政区域数据,包括省市县镇村5个层级;
  
  港澳台地区的数据只有3级;
  
  包含大陆地区的邮政编码和经纬度信息.
  
---------------------------------------
####  cnarea20141031.7z是爬取2014年的数据,截止2014年10月31日.

  全部共714472条
  
  ·大陆数据共714048条,其中
  
  省/直辖市 31
  
  市/州 346
  
  县/区 3139
  
  乡/镇 40053
  
  村/社区 670479
  

### 表结构

```

CREATE TABLE `cnarea_2014` (
  `id` mediumint(7) unsigned NOT NULL AUTO_INCREMENT,
  `parent_id` mediumint(7) unsigned NOT NULL DEFAULT '0' COMMENT '父级ID',
  `level` tinyint(1) unsigned NOT NULL DEFAULT '0' COMMENT '层级',
  `zip_code` char(6) NOT NULL DEFAULT '' COMMENT '邮政编码',
  `city_code` char(4) NOT NULL DEFAULT '' COMMENT '区号',
  `area_code` varchar(20) NOT NULL DEFAULT '' COMMENT '行政代码',
  `name` varchar(50) NOT NULL DEFAULT '' COMMENT '名称',
  `short_name` varchar(50) NOT NULL DEFAULT '' COMMENT '简称',
  `merger_name` varchar(255) NOT NULL DEFAULT '' COMMENT '组合名',
  `pinyin` varchar(100) NOT NULL DEFAULT '' COMMENT '拼音',
  `lng` decimal(12,8) NOT NULL DEFAULT '0.00000000' COMMENT '经度',
  `lat` decimal(12,8) NOT NULL DEFAULT '0.00000000' COMMENT '维度',
  PRIMARY KEY (`id`),
  KEY `idx_lev` (`level`,`parent_id`) USING BTREE
) ENGINE=MyISAM AUTO_INCREMENT=714473 DEFAULT CHARSET=utf8 COMMENT='中国行政地区表';

```
