# Noctalia Shell 拼音搜索补丁

为 Noctalia Shell (Quickshell 版) 启动器添加拼音全拼和首字母搜索支持。

## 功能

- `weixin` → 微信
- `wx` → 微信
- `zfb` → 支付宝
- 支持所有中文应用名

## 安装

```bash
sudo cp PinyinHelper.js /etc/xdg/quickshell/noctalia-shell/Helpers/
sudo cp qml/ApplicationsProvider.qml /etc/xdg/quickshell/noctalia-shell/Modules/Panels/Launcher/Providers/
```

重启 quickshell：

```bash
pkill -f "qs -c noctalia"
nohup qs -c noctalia-shell > /dev/null 2>&1 &
```

如果遇到 QML 缓存问题：

```bash
rm -rf ~/.cache/noctalia-qs/qmlcache
```

## 修改的文件

| 文件 | 改动 |
|------|------|
| `PinyinHelper.js` | **新增** — 20924 汉字拼音映射 + 转换函数 |
| `qml/ApplicationsProvider.qml` | 搜索拼音/首字母字段；FuzzySort 和 fallback 搜索均加入拼音匹配 |

## 技术说明

- `PinyinHelper.toPinyinCompact(text)` — 中文转拼音连写（微信 → weixin）
- `PinyinHelper.toPinyinInitials(text)` — 中文转首字母（微信 → wx）
- 映射数据源自 [dms-pinyin-search](https://github.com/SafetyFA/dms-pinyin-search)

搜索优先级：拼音全拼和首字母，与 FuzzySort 的 keys 中其他字段一同参与模糊匹配。
