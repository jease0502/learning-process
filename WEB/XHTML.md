---
tags: web
---
# XHTML
---
## 介紹

```htmlmixed=
<!DOCTYPE html>
<html xmlns="">
<!--xhtml 檔案根元素，其中xhtml屬性=聲明檔案空間-->
<meta charset="utf-8">
<head>
	<title></title>
</head>
<body>

</body>
</html>
```

## DTD
表示檔案類型定義，裡面包含了文檔的規則，網頁會根據DTD來解析網頁元素，要建立符合網頁標準的檔案，DOCTYPE是必備的，否則CSS將無法使用

## 規定

- 檔案開頭必須定義檔案類型
- 在根於訴必須命名空間，也就是設置XMLNS屬性
- 所有標籤都一定要閉合<><\>
- 所有元素與屬性都必須小寫
- 所有屬性都必須使用雙引號標記起來，例如```<table height="80"></table>```
- 所有屬性都必須被賦予值，沒有值的屬性就會直接用自身來賦予值，例如:
```錯誤寫法```
```htmlmixed=
<tp nowrap></tp>
```
```正確寫法```
```htmlmixed=
<tp nowrap='nowrap'></tp>
```
- 所有特殊符號都需要使用程式表示，例如小於```<```就必須使用```"&lt";```

---