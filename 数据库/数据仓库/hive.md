## 函数

```sql
regexp_extract(decode(unbase64(split(b64content, '\\|')[1]),'utf8'), '&a=(.*?)&', 1)
```