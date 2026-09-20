# Talent Pool · LinkOS 人才库

多岗位招聘人才看板（GitHub Pages）。数据按岗位组织，顶部可在 **「全部岗位」总览** 与各岗位之间切换。

## 看板功能

- **岗位切换**：顶部岗位 Tab，全部岗位总览（跨岗位 KPI + 各岗位人才分布）↔ 单个岗位视图
- **概览 KPI**：在库候选人、平均适配分、高适配人数、在流程中、招聘岗位数
- **Pipeline 邀约看板**（岗位视图）：按初筛/二筛/邀约/面试/Offer/暂缓 等状态分组，点击状态筛选；总览页显示各岗位人数分布、点击可跳转
- **候选人卡片墙**：按适配分/面试顺序/年限排序，技能标签筛选，姓名/公司/技能搜索；总览页卡片带岗位徽标
- **候选人详情**：背景、技能亮点、风险短板、JD 六维雷达，一键经 CDN 秒开完整简历
- **多人六维对比**：同一岗位内勾选 2–4 人雷达叠加（六维口径按岗位定义，跨岗位不可对比）

## 数据与网页分离

- 唯一事实源：[`data/talent.json`](data/talent.json)，顶层结构：

```json
{
  "positions": [ { "key":"fde", "title":"...", "dimensions":[...], "statusFlow":[...] } ],
  "candidates": [ { "id":1, "positionKey":"fde", "name":"...", "scores":{...}, ... } ]
}
```

- `data/talent.js` 是同一份数据的 `window.TALENT` 包装，保证本地双击 `index.html`（file://）也能离线打开
- 候选人 `id` 全局唯一；每条候选人用 `positionKey` 归属岗位

## 新增岗位流程

1. 在 `data/talent.json` 的 `positions` 里加一个岗位对象（`key` / `title` / `location` / `salary` / `dimensions` 六维 / `statusFlow` 状态流）
2. 在 `candidates` 里加该岗位候选人，`positionKey` 填新岗位 key、`id` 接续全局唯一编号
3. 简历 PDF 放入 `resumes/<岗位key>/`（FDE 历史简历在 `resumes/` 根目录，已兼容）
4. 同步更新 `data/talent.js`（JSON 外包 `window.TALENT = ...;`）
5. commit & push，网页与岗位 Tab 自动更新，无需改代码

候选人记录字段：

```
id positionKey 姓名 年限 年限文本 原任方向 教育背景 技能亮点 适配分 风险短板
当前状态 建议面试顺序 备注 技能标签[] 六维评分{} 简历文件名
```

## 目录

```
TalentPool/
├─ index.html          # 多岗位门户（Pages 首页）
├─ data/
│  ├─ talent.json      # 唯一事实源
│  └─ talent.js        # 离线打开用包装
└─ resumes/            # 简历（新岗位放 <key>/ 子目录）
```

## 简历访问

简历通过 jsDelivr CDN 打开（国内快）：`https://cdn.jsdelivr.net/gh/gunani1/LinkOS-Hrbp@main/TalentPool/resumes/...`。
更新简历后若 CDN 有缓存，刷新对应文件的 CDN 缓存或变更文件名即可。

---
LinkOS Hrbp · Chenkeyao
