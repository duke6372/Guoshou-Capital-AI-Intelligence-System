# API测试用例

## 测试概述

本文档定义系统API的测试用例，覆盖RESTful接口的正常场景、异常场景和安全测试。

---

## 工作台API

### API-WB-001: 获取KPI数据

**接口**: `GET /api/v1/workbench/kpi`

**请求参数**:
| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| date | string | 否 | 日期，格式YYYY-MM-DD |

**请求头**:
```
Authorization: Bearer {token}
Content-Type: application/json
```

**预期响应** (200):
```json
{
  "code": 200,
  "message": "success",
  "data": {
    "managedScale": 170000000000,
    "managedScaleUnit": "CNY",
    "occupancyRate": 0.924,
    "occupancyRateChange": -0.006,
    "noi": 284000000,
    "noiUnit": "CNY",
    "riskAlerts": {
      "total": 10,
      "red": 3,
      "yellow": 7
    },
    "lastUpdated": "2026-05-16T09:30:00Z"
  }
}
```

**错误响应**:
- 401: 未授权
- 403: 无权限访问该数据
- 500: 服务器错误

**优先级**: P0
**测试类型**: 接口测试

---

### API-WB-002: 获取趋势数据

**接口**: `GET /api/v1/workbench/trends`

**请求参数**:
| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| metric | string | 是 | 指标名：occupancy_rate/noi/rental_income |
| months | int | 否 | 月份数，默认12 |

**预期响应** (200):
```json
{
  "code": 200,
  "data": {
    "metric": "occupancy_rate",
    "dataPoints": [
      {"date": "2025-06", "value": 0.918},
      {"date": "2025-07", "value": 0.920},
      {"date": "2025-08", "value": 0.922}
    ],
    "summary": {
      "avg": 0.921,
      "max": 0.924,
      "min": 0.918
    }
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

### API-WB-003: 获取Top异常项目

**接口**: `GET /api/v1/workbench/top-alerts`

**请求参数**:
| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| limit | int | 否 | 返回数量，默认10 |

**预期响应** (200):
```json
{
  "code": 200,
  "data": {
    "items": [
      {
        "projectId": "proj_001",
        "projectName": "上海·项目A",
        "metric": "occupancy_rate",
        "currentValue": 0.886,
        "threshold": 0.90,
        "level": "red",
        "duration": 14,
        "lastUpdated": "2026-05-16"
      }
    ],
    "total": 4
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

## 经营分析API

### API-BI-001: 获取指标拆解

**接口**: `GET /api/v1/bi/metrics/{metric}/breakdown`

**请求参数**:
| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| dimension | string | 是 | 维度：city/business_type/project |
| date | string | 是 | 日期 |

**预期响应** (200):
```json
{
  "code": 200,
  "data": {
    "dimension": "city",
    "items": [
      {
        "name": "上海",
        "contribution": -0.004,
        "description": "受项目A空置影响"
      }
    ]
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

### API-BI-002: 获取指标口径

**接口**: `GET /api/v1/bi/metrics/{metric}/definition`

**预期响应** (200):
```json
{
  "code": 200,
  "data": {
    "metricId": "occupancy_rate",
    "name": "出租率（组合）",
    "version": "v1.0",
    "formula": "(已出租面积 / 总可出租面积) * 100%",
    "filters": ["排除装修期", "排除培育期"],
    "refreshFrequency": "日",
    "owner": "数据治理组"
  }
}
```

**优先级**: P1
**测试类型**: 接口测试

---

## 项目组合API

### API-PF-001: 获取项目列表

**接口**: `GET /api/v1/portfolio/projects`

**请求参数**:
| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| city | string | 否 | 城市筛选 |
| businessType | string | 否 | 业态筛选 |
| riskLevel | string | 否 | 风险等级 |
| page | int | 否 | 页码，默认1 |
| pageSize | int | 否 | 每页数量，默认20 |

**预期响应** (200):
```json
{
  "code": 200,
  "data": {
    "items": [
      {
        "projectId": "proj_001",
        "name": "上海·项目A",
        "city": "上海",
        "businessType": "商业",
        "occupancyRate": 0.886,
        "riskLevel": "red",
        "noi": 50000000
      }
    ],
    "pagination": {
      "page": 1,
      "pageSize": 20,
      "total": 45,
      "totalPages": 3
    }
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

### API-PF-002: 获取项目详情

**接口**: `GET /api/v1/portfolio/projects/{projectId}`

**预期响应** (200):
```json
{
  "code": 200,
  "data": {
    "projectId": "proj_001",
    "name": "上海·项目A",
    "city": "上海",
    "businessType": "商业",
    "totalArea": 50000,
    "rentableArea": 45000,
    "occupancyRate": 0.886,
    "metrics": {
      "noi": 50000000,
      "rentalIncome": 80000000
    }
  }
}
```

**错误响应**:
- 403: 无权限访问该项目
- 404: 项目不存在

**优先级**: P0
**测试类型**: 接口测试

---

## 情报中心API

### API-INT-001: 获取情报列表

**接口**: `GET /api/v1/intelligence/items`

**请求参数**:
| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| type | string | 否 | 情报类型 |
| level | string | 否 | L级别 |
| confidence | string | 否 | 置信度 |
| page | int | 否 | 页码 |
| pageSize | int | 否 | 每页数量 |

**预期响应** (200):
```json
{
  "code": 200,
  "data": {
    "items": [
      {
        "id": "intel_001",
        "type": "competition",
        "level": "L3",
        "title": "竞品新增项目获取动向",
        "summary": "一线核心商办...",
        "source": "公开新闻",
        "confidence": "high",
        "publishedAt": "2026-05-16T10:00:00Z"
      }
    ],
    "total": 156
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

### API-INT-002: 创建订阅

**接口**: `POST /api/v1/intelligence/subscriptions`

**请求体**:
```json
{
  "type": "competition",
  "keywords": ["平安不动产", "竞品"],
  "frequency": "weekly",
  "channel": "in_app"
}
```

**预期响应** (201):
```json
{
  "code": 201,
  "message": "subscription created",
  "data": {
    "subscriptionId": "sub_001"
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

## 知识库API

### API-KB-001: 搜索知识

**接口**: `POST /api/v1/knowledge/search`

**请求体**:
```json
{
  "query": "租赁合同风险点",
  "category": "contract",
  "limit": 10
}
```

**预期响应** (200):
```json
{
  "code": 200,
  "data": {
    "items": [
      {
        "id": "kb_001",
        "title": "租赁合同关键条款",
        "category": "合同知识",
        "relevance": 0.95,
        "snippet": "租赁合同中需要关注...",
        "references": ["clause_12", "clause_15"]
      }
    ]
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

### API-KB-002: 创建知识

**接口**: `POST /api/v1/knowledge/items`

**请求体**:
```json
{
  "title": "新知识条目",
  "category": "制度/SOP",
  "content": "正文内容...",
  "tags": ["标签1", "标签2"]
}
```

**预期响应** (201):
```json
{
  "code": 201,
  "data": {
    "id": "kb_new_001",
    "version": "v1.0",
    "status": "pending_review"
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

## 风险预警API

### API-RG-001: 获取预警列表

**接口**: `GET /api/v1/risk/alerts`

**请求参数**:
| 参数 | 类型 | 必填 | 说明 |
|------|------|------|------|
| level | string | 否 | red/yellow/info |
| status | string | 否 | pending/confirmed/resolved |

**预期响应** (200):
```json
{
  "code": 200,
  "data": {
    "items": [
      {
        "alertId": "alert_001",
        "level": "red",
        "type": "occupancy_rate",
        "projectId": "proj_001",
        "currentValue": 0.886,
        "threshold": 0.90,
        "status": "pending",
        "createdAt": "2026-05-01T00:00:00Z"
      }
    ],
    "stats": {
      "red": 3,
      "yellow": 7,
      "total": 10
    }
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

### API-RG-002: 更新预警状态

**接口**: `PATCH /api/v1/risk/alerts/{alertId}/status`

**请求体**:
```json
{
  "status": "confirmed",
  "comment": "确认原因：正常波动"
}
```

**预期响应** (200):
```json
{
  "code": 200,
  "message": "status updated",
  "data": {
    "alertId": "alert_001",
    "status": "confirmed",
    "updatedAt": "2026-05-16T11:00:00Z"
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

## Copilot API

### API-CP-001: 发送对话

**接口**: `POST /api/v1/copilot/chat`

**请求体**:
```json
{
  "message": "解释本月NOI变化原因",
  "context": {
    "date": "2026-05"
  }
}
```

**预期响应** (200):
```json
{
  "code": 200,
  "data": {
    "conversationId": "conv_001",
    "messageId": "msg_001",
    "response": "本月NOI为2.84亿，主要原因是...",
    "citations": [
      {
        "sourceType": "data",
        "sourceId": "noi_monthly",
        "snippet": "NOI=收入-运营成本",
        "relevance": 0.95
      }
    ],
    "suggestions": [
      "查看北京项目贡献度",
      "查看能耗异常"
    ]
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

### API-CP-002: 生成报告

**接口**: `POST /api/v1/copilot/reports`

**请求体**:
```json
{
  "type": "executive_daily",
  "date": "2026-05-16",
  "includeSections": ["summary", "metrics", "alerts"]
}
```

**预期响应** (202):
```json
{
  "code": 202,
  "message": "report generation started",
  "data": {
    "reportId": "report_001",
    "status": "processing"
  }
}
```

**轮询状态**: `GET /api/v1/copilot/reports/{reportId}`

**优先级**: P0
**测试类型**: 接口测试

---

## 管理API

### API-ADM-001: 获取用户列表

**接口**: `GET /api/v1/admin/users`

**预期响应** (200):
```json
{
  "code": 200,
  "data": {
    "items": [
      {
        "userId": "user_001",
        "name": "张三",
        "email": "zhangsan@company.com",
        "roles": ["analyst"],
        "status": "active"
      }
    ]
  }
}
```

**优先级**: P0
**测试类型**: 接口测试

---

### API-ADM-002: 更新用户权限

**接口**: `PUT /api/v1/admin/users/{userId}/permissions`

**请求体**:
```json
{
  "projectPermissions": ["proj_001", "proj_002"],
  "dataDomainPermissions": ["sales_data"]
}
```

**预期响应** (200):
```json
{
  "code": 200,
  "message": "permissions updated"
}
```

**优先级**: P0
**测试类型**: 安全测试

---

## 安全测试用例

### API-SEC-001: 未授权访问

**测试步骤**:
1. 不带token访问各API
2. 带过期token访问

**预期结果**:
- 返回401 Unauthorized
- 无数据泄露

**优先级**: P0
**测试类型**: 安全测试

---

### API-SEC-002: 越权访问

**前置条件**:
- 用户A仅能访问部分项目

**测试步骤**:
1. 用用户A的token访问用户B的项目数据

**预期结果**:
- 返回403 Forbidden
- 无数据泄露

**优先级**: P0
**测试类型**: 安全测试

---

### API-SEC-003: SQL注入测试

**测试步骤**:
1. 在API参数中注入SQL
```
?projectId=proj_001'; DROP TABLE users;--
```

**预期结果**:
- 参数被正确转义
- 不执行注入SQL
- 返回正常或空结果

**优先级**: P0
**测试类型**: 安全测试

---

### API-SEC-004: 参数校验

**测试步骤**:
1. 传入非法参数类型
2. 传入超长字符串
3. 传入特殊字符

**预期结果**:
- 返回400 Bad Request
- 错误信息清晰
- 不暴露内部信息

**优先级**: P1
**测试类型**: 安全测试

---

## 性能测试用例

### API-PERF-001: 响应时间基准

**测试步骤**:
1. 对每个API执行100次请求
2. 记录响应时间分布

**性能指标**:
| API | P50 | P95 | P99 |
|-----|-----|-----|-----|
| GET /kpi | <100ms | <500ms | <1s |
| GET /trends | <200ms | <1s | <2s |
| POST /chat | <1s | <3s | <5s |

**优先级**: P0
**测试类型**: 性能测试

---

### API-PERF-002: 并发测试

**测试步骤**:
1. 模拟50并发用户
2. 持续压测5分钟

**预期结果**:
- 成功率 ≥ 99%
- 无内存泄漏
- 服务稳定

**优先级**: P0
**测试类型**: 性能测试

---
*版本: v0.1*