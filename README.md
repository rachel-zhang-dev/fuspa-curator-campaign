# 芙SPA · 长楹首店主理人体验计划（GitHub Pages + EmailJS）

静态问卷页，提交后通过 **EmailJS** 把答卷以邮件形式发到指定收件箱（默认 `122530385@qq.com`）。

- **页面 UI**：完全自定义（芙 SPA 暖色风），不依赖第三方表单平台样式
- **收数方式**：EmailJS 免费版 **每月 200 封** 邮件，足够单次邀约活动
- **国内可用**：EmailJS 走你自己授权的邮箱 SMTP，不会卡 Cloudflare 海外服务

---

## 一次性配置：EmailJS（约 10 分钟）

### 1. 注册账号

打开 https://www.emailjs.com → Sign Up（用 Gmail 一键登录最快）。

### 2. 添加 Email Service（推荐用 Gmail）

后台左侧 **Email Services → Add New Service**。

- 选 **Gmail**
- 点 **Connect Account** → 用 `ruiping.zhang.rachel@gmail.com` 授权（一键 OAuth）
- 保存后会得到一个 **Service ID**，例如 `service_abc1234`
- 复制下来备用

> 也可以用 QQ 邮箱（Other / SMTP），但需要在 QQ 邮箱后台开启 SMTP 并获取**授权码**，比 Gmail 多两步。推荐 Gmail 发送 → 收件人填 QQ 邮箱。

### 3. 创建 Email Template

左侧 **Email Templates → Create New Template**。

**Settings 标签：**

| 字段 | 填什么 |
|------|--------|
| Template Name | `fuspa-curator` |
| **To Email** | `122530385@qq.com` |
| From Name | `芙SPA 长楹店问卷` |
| Reply To | （留空或填回信邮箱） |
| Subject | `{{subject}}` |

**Content 标签**（直接粘贴下面这段）：

```
新的主理人问卷答卷

提交时间：{{submitted_at}}
姓名：{{respondent_name}}
手机：{{respondent_phone}}

----------------------------------------
{{content}}
----------------------------------------

来自：芙SPA 长楹首店主理人体验计划
```

保存后会得到一个 **Template ID**，例如 `template_xyz5678`，复制下来备用。

### 4. 获取 Public Key

左侧 **Account → General**，找到 **Public Key**，例如 `aBcDeFg123HiJkL`，复制下来。

### 5. 把 3 个 ID 填进代码

打开 `index.html`，找到这段（约第 510 行附近）：

```js
const EMAILJS_PUBLIC_KEY = 'YOUR_PUBLIC_KEY';
const EMAILJS_SERVICE_ID = 'YOUR_SERVICE_ID';
const EMAILJS_TEMPLATE_ID = 'YOUR_TEMPLATE_ID';
```

替换为你刚拿到的三个值，例如：

```js
const EMAILJS_PUBLIC_KEY = 'aBcDeFg123HiJkL';
const EMAILJS_SERVICE_ID = 'service_abc1234';
const EMAILJS_TEMPLATE_ID = 'template_xyz5678';
```

### 6. 推到 GitHub

```bash
cd campaign-curator
git add index.html
git commit -m "Configure EmailJS credentials"
git push origin main
```

等 1～2 分钟 Pages 重新部署。

### 7. 测试

1. 用浏览器打开问卷页填一份  
2. 提交后应跳到「感谢页」  
3. 去 `122530385@qq.com` 看邮件（可能要等几秒~1 分钟）  
4. **若 QQ 邮箱看不到 → 翻垃圾邮件 / 订阅邮件**

---

## 主要文件

| 文件 | 作用 |
|------|------|
| `index.html` | 问卷页（12 题 + 联系方式） |
| `thank-you.html` | 提交成功页 |
| `README.md` | 本文件 |

---

## 修改题目

直接编辑 `index.html` 里各 `fieldset`：

- `name` 即邮件正文里显示的字段名
- 多选用 `type="checkbox"` 同名重复
- 单选用 `type="radio"` 同名重复
- 文本用 `<textarea>` 或 `<input>`

改完 `git push` 即可，**无需重配 EmailJS**（模板只用到 `{{content}}` 这个汇总字段）。

---

## 注意

- EmailJS 的 Public Key、Service ID、Template ID 会出现在公开仓库的前端代码里 —— 这是设计上允许的（它们是「公开身份」，真正的鉴权在 EmailJS 后台限制 Domain / Rate Limit）
- 建议在 EmailJS 后台 **Account → Security** 开启 **Allowed Origins**，只允许 `https://rachel-zhang-dev.github.io` 访问，防止别人盗用配额
- 免费版 200 封/月，超出会暂停；对邀约制小范围活动一般够
- 不要把含真实用户数据的导出文件 commit 到 GitHub

---

## 链接

- 在线地址：https://rachel-zhang-dev.github.io/fuspa-curator-campaign/
- 仓库：https://github.com/rachel-zhang-dev/fuspa-curator-campaign
