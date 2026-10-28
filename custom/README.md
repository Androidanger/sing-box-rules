# 自定义规则说明

这个目录用来给你自己的规则集增加额外域名，**不会被上游覆盖**。

## 如何给 geosite-gfw 增加域名

1. 编辑文件：`custom/geosite/gfw.txt`
2. 每行写一个域名（支持注释）
3. 保存后 push 到 main 分支，或者手动触发 Actions
4. 等待 Actions 跑完后，`rule-set-geosite` 分支里的 `geosite-gfw.srs` 就会包含你新增的域名

### 文件格式示例（gfw.txt）

```text
# 这是注释，会被忽略

# 普通域名（默认按 domain_suffix 处理，推荐）
example.com
another-site.org

# 精确匹配完整域名
full:www.exact-domain.com

# 关键词匹配
keyword:ads

# 正则匹配
regexp:^ads\..*
```

### 支持的前缀

| 写法 | 含义 | 对应规则类型 |
|------|------|--------------|
| `example.com` | 默认 | domain_suffix（会自动加前导 `.`） |
| `full:www.xxx.com` | 精确匹配 | domain |
| `keyword:xxx` | 关键词 | domain_keyword |
| `regexp:^xxx` | 正则 | domain_regex |

### 其他类别

你也可以创建其他文件，比如：
- `custom/geosite/cn.txt` → 会合并到 geosite-cn
- `custom/geosite/geolocation-!cn.txt` → 合并到 geosite-geolocation-!cn
- `custom/geosite/category-ads-all.txt` → 合并到对应类别

文件名去掉 `.txt` 就是对应的类别名。
