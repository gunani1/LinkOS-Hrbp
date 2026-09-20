# Talent Pool · 人才库

内部招聘人才看板（GitHub Pages）。当前收录 **前沿部署工程师 FDE** 岗位的 8 位候选人。

## 看板功能

- **概览 KPI**：人才库总数、平均适配分、高适配人数、活跃邀约数、暂停人数
- **pipeline 邀约看板**：按初筛 / 技术二筛 / 邀约 / 面试 / Offer / 暂缓 等状态分组，点击状态筛选
- **候选人卡片墙**：按适配分 / 年限 / 建议面试顺序排序，按年限、适配度、技能标签筛选，支持姓名搜索
- **候选人详情**：背景、技能亮点、风险短板、JD 六维雷达、面试结论，一键打开完整简历
- **多人六维对比**：勾选 2–3 位候选人，雷达叠加对比
- **人才结构图**：适配分分布

## 数据与网页分离

- 唯一事实源：[`data/talent.json`](data/talent.json)，网页读取后渲染
- [`data/talent.js`](data/talent.js) 是同一份数据的 `window.TALENT` 包装，保证本地双击 `index.html`（`file://`）也能离线打开
- **新增 / 更新候选人只需改 `data/talent.json`，网页自动更新，无需改代码**

候选人记录字段：

```
id 姓名 年限 年限文本 原任方向 教育背景 技能亮点 适配分 风险短板
当前状态 建议面试顺序 备注 技能标签[] 六维评分{} 简历文件名
```

六维评分口径（对标 JD，0–10）：AI 研发经验 / 全栈+Agent 技术深度 / 业务洞察 / 客户对接 / 原型验证落地 / 业务价值聚焦。

## 目录

```
talent-pool/
├─ index.html          # 看板（GitHub Pages 首页）
├─ data/
│  ├─ talent.json      # 唯一事实源
│  └─ talent.js        # 离线打开用包装
└─ resumes/            # 候选人简历 PDF
```

## 更新流程

1. 编辑 `data/talent.json`，同步更新 `data/talent.js`（在 JSON 外包一层 `window.TALENT = ...;`）
2. 简历 PDF 放入 `resumes/`，文件名与候选人记录的 `resume` 字段一致
3. commit & push，Pages 自动更新

---
LinkOS Hrbp · Chenkeyao
