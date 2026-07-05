# Time Recorder XP

一个手机优先的 Windows XP 像素复古风时间记录网页。首页只显示三项统计和三个入口：记录今天、月历统计、设置。项目图标使用“自定义字符 + 自定义颜色”，不需要上传图片。

## 文件

- `index.html`：直接上传到 GitHub Pages 的主页面。
- `supabase_setup.sql`：Supabase 建表、索引、RLS policy 初始化脚本。

## 本地预览

直接双击打开 `index.html`，如果没有填写 Supabase URL 和 anon key，会进入本地预览模式。这个模式下数据只存在当前浏览器的 localStorage 中，用来测试页面和交互。

## 连接 Supabase

打开 `index.html`，找到下面两行：

```js
const SUPABASE_URL = "https://YOUR_PROJECT_ID.supabase.co";
const SUPABASE_ANON_KEY = "YOUR_SUPABASE_ANON_KEY";
```

替换成 Supabase Project Settings -> API 里的 Project URL 和 anon public key。

然后在 Supabase Dashboard -> SQL Editor 中运行 `supabase_setup.sql`。

## GitHub Pages

把 `index.html` 放到仓库根目录，进入仓库 Settings -> Pages，Source 选择 Deploy from a branch，Branch 选择 `main` 和 `/root`，保存后等待部署完成。

## Auth 提示

这个版本使用 Supabase Auth 的邮箱 + 密码登录。第一次使用时可以在网页里点“注册”。如果 Supabase 开启了邮箱确认，需要先去邮箱确认；如果只是个人自用并希望简单测试，可以在 Supabase Auth 设置里临时关闭邮箱确认。

## 数据说明

`time_projects` 存项目名、图标字符、颜色、排序和是否归档。

`time_entries` 存某一天某个项目选择了哪些小时，`hours` 是 0 到 23 的整数数组。例如 `[9, 10, 11]` 表示 09:00 到 12:00。
