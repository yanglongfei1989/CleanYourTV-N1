# N1 Remote 集成说明

## Provider 接口约定

Authority：

```text
com.gathin.n1remote.status
```

URI：

```text
content://com.gathin.n1remote.status/status
```

字段：

- `ip`
- `port`
- `pin`
- `serviceOnline`
- `url`

桌面仅在首页可见时查询。状态卡不可获得焦点，不参与方向键导航。

## 启动布局

N1 的应用扫描可能在首次窗口焦点之后才完成。因此桌面会：

1. 在多个启动检查点重新校正 Dock 内边距。
2. 等待第一个子视图真正创建。
3. 清除空 RecyclerView 的临时焦点。
4. 聚焦第一张 Dock 卡片，成功后才清除冷启动标记。
5. Dock 布局稳定后重新贴合共享高亮框。

## 应用横幅

`app_banners` 将包名映射到桌面内置 Drawable：

```xml
<item>com.gathin.n1remote=banner_n1remote</item>
<item>com.github.avbox.osc=banner_avbox</item>
<item>com.android.tv.settings=banner_settings</item>
```

只要应用包名不变，更新或重装后横幅仍能保持。

