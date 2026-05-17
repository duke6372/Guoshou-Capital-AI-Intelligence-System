# 国寿资本AI智能体情报系统产品设计方案（要点卡）

## 这份材料在解决什么问题（目的）
- 给出产品概念设计（v1.0），定义愿景、目标用户、核心用例、六大模块（M1-M6）与技术架构/分期落地路线，为后续咨询建议书与实施推进提供“可落地的产品蓝图”。

## 覆盖的业务域/对象（范围）
- 业务域：投后经营分析、外部情报（竞品/政策/市场）、知识管理（合同/制度/案例）、风险预警、对话式决策支持。
- 对象：项目/基金/资产组合、经营指标（出租率/租金/NOI/IRR等）、竞品主体、合同与条款、风险事件与预警、报告模板。

## 关键结论/事实（可追溯）
- 产品愿景：面向中高管理层的一体化平台，覆盖数据整合、BI分析、知识管理、竞品情报与风险预警，提升经营分析效率与投资决策质量。[产品设计方案.pdf.md:L23-L26](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L23-L26)
- 核心用户画像与需求：高管层、投资总监、资产管理团队、风控合规团队、中层管理者等。[产品设计方案.pdf.md:L31-L39](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L31-L39)
- 核心用例：一页式经营仪表盘、尽调AI助手、竞品追踪、合同风险审查、退出策略推荐、政策解读。[产品设计方案.pdf.md:L42-L56](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L42-L56)
- 六大模块定义：M1数据中枢、M2情报引擎、M3知识库、M4经营仪表盘、M5风险卫士、M6 Copilot。[产品设计方案.pdf.md:L57-L75](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L57-L75)
- 分期路线：Phase 1 先做 M1+M4，Phase 2 做 M3+M5，Phase 3 做 M2+M6，Phase 4 持续迭代。[产品设计方案.pdf.md:L356-L362](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L356-L362)

## 明确的需求/能力点（用户故事/功能点）
- M1 DataHub：内部连接器（基金/财务/物业/合同/OA）、外部采集（代理行/企查查/政策/新闻）、统一字典与口径、质量评分、血缘追踪。[产品设计方案.pdf.md:L89-L106](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L89-L106)
- M2 IntelEngine：竞品采集与分类、置信度评估、政策解读与影响评估、对标分析、智能报告生成。[产品设计方案.pdf.md:L118-L144](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L118-L144)
- M3 KnowledgeBase：合同/制度/案例/行业知识结构；RAG应用（问答、尽调清单、条款比对、报告写作）。[产品设计方案.pdf.md:L157-L193](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L157-L193)
- M4 BIDashboard：高管驾驶舱（D1）、组合视图（D2）、单项目详情（D3）、市场分析（D4）、自定义分析/导出。[产品设计方案.pdf.md:L210-L239](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L210-L239)
- M5 RiskGuard：预警阈值定义（出租率/租户信用/租金逾期/政策合规/市场系统性风险）与分级推送。[产品设计方案.pdf.md:L255-L281](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L255-L281)
- M6 Copilot：四类Copilot能力、示例问句、多端部署（飞书/Web/App/邮件）。[产品设计方案.pdf.md:L292-L327](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L292-L327)

## 数据与系统边界（数据源、上下游、依赖）
- 数据资产分层：内部数据、外部数据、知识数据；交互层多端入口；基础设施强调私有化/国产化。[产品设计方案.pdf.md:L340-L355](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L340-L355)

## 约束与风险（合规、权限、口径、时效）
- 技术选型原则：数据安全优先、渐进式建设、集成优于自建。[产品设计方案.pdf.md:L351-L356](file:///Users/mic/Documents/trae_projects/Guoshou/docs/source/%E5%9B%BD%E5%AF%BF%E8%B5%84%E6%9C%ACAI%E6%99%BA%E8%83%BD%E4%BD%93%E6%83%85%E6%8A%A5%E7%B3%BB%E7%BB%9F%E4%BA%A7%E5%93%81%E8%AE%BE%E8%AE%A1%E6%96%B9%E6%A1%88.pdf.md#L351-L356)

## 未决问题（需要向业务/技术确认）
- M6多端入口的权限隔离、审计留痕与敏感数据脱敏规则（尤其是飞书机器人/邮件摘要场景）。
- M2“置信度评估/影响评估”的评价口径与人工复核流程（哪些情报必须人工确认后推送）。
