# 芙SPA · 主理人邀约问卷（GitHub Pages + FormSubmit）

静态问卷页，提交后 **每份答卷发一封邮件** 到你配置的邮箱。

## 部署前必改（2 处）

打开 `index.html` 确认邮箱与 `_next` 地址（已配置为当前仓库）：

1. **收件邮箱**（约第 168 行）

   ```html
   action="https://formsubmit.co/你的邮箱@example.com"
   ```

2. **提交成功跳转地址**（`_next`，约第 175 行）

   改成你的 GitHub Pages 完整地址，例如：

   ```html
   value="https://rachel-zhang-dev.github.io/fuspa-curator-campaign/thank-you.html"
   ```

   仓库名若不是 `fuspa-curator-campaign`，请同步修改。

## 推到 GitHub

```bash
cd campaign-curator
git init
git add index.html thank-you.html README.md
git commit -m "Add curator campaign questionnaire"
```

仓库：https://github.com/rachel-zhang-dev/fuspa-curator-campaign

```bash
git remote add origin git@github.com:rachel-zhang-dev/fuspa-curator-campaign.git
git branch -M main
git push -u origin main
```

若仓库已存在，把 `origin` 换成你的地址即可。

## 开启 GitHub Pages

1. 仓库 → **Settings** → **Pages**
2. **Source**：Deploy from a branch
3. **Branch**：`main` / **Folder**：`/ (root)`
4. 保存后等 1～3 分钟，访问：

   `https://rachel-zhang-dev.github.io/fuspa-curator-campaign/`

## 激活 FormSubmit（首次必做）

1. 改好 `index.html` 里的邮箱并部署 Pages
2. 用浏览器 **自己提交一次** 测试问卷
3. 去邮箱查 **FormSubmit 发来的确认邮件**，点链接激活
4. 之后他人提交才会稳定发到你的邮箱

邮件主题一般为：`【芙SPA】主理人邀约问卷`，正文为表格字段。

## 对外二维码

用任意「链接生成二维码」工具，填入 Pages 首页地址即可，例如：

`https://rachel-zhang-dev.github.io/fuspa-curator-campaign/`

## 修改题目

直接编辑 `index.html` 里各 `fieldset`，`name` 即邮件里的字段名。改完 `git push` 即可，无需改 FormSubmit 配置。

## 注意

- 免费、无后台列表，答卷在 **邮箱** 里；量大时可转发或抄送到表格
- FormSubmit 为海外服务，国内偶发慢；提交后若长时间无反应，可重试或换网络
- 勿把含真实用户数据的导出文件 commit 到 GitHub
