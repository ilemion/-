# Gantt图生成代码（第二次变更版）

本项目提供3种方式生成Gantt图:
1. **Mermaid语法** - Markdown原生支持,最简单
2. **HTML+JavaScript** - 交互式Gantt图,最美观
3. **Python** - 可导出图片,最灵活

**原始项目周期: 2026年3月16日-4月26日 (共42天/6周)**  
**CR-001后周期: 2026年3月16日-4月30日 (共47天/7周)**  
**CR-002后周期: 2026年3月16日-5月10日 (共56天/8周)**

---

## ⚠️ 第二次变更摘要

| 变更单号 | 变更日期 | 变更内容 | 工期影响 | 成本影响 |
|---------|---------|---------|---------|---------|
| CR-2026-001 | 2026年3月 | Q1报告频率调整为半月报 | +5天 | +¥15,000 |
| **CR-2026-002** | **2026年4月** | **移动端审核适配(iOS/Android)** | **+14天** | **+¥180,000** |

### 里程碑调整对比

| 里程碑 | 原始日期 | CR-001后 | CR-002后 | 总延期 |
|--------|---------|---------|---------|--------|
| M1: 需求基准化 | 3月20日 | 3月20日 | 3月20日 | 0天 |
| M2: 核心功能完成 | 3月31日 | 4月5日 | **4月19日** | **+19天** |
| M3: 数据分析上线 | 4月10日 | 4月17日 | **4月24日** | **+14天** |
| M4: 系统试运行 | 4月26日 | 4月30日 | **5月10日** | **+14天** |

---

## 方式一: Mermaid语法(推荐,最简单)

直接在Markdown中渲染,GitHub支持!

```mermaid
gantt
    title 云南省企业就业失业数据采集系统 - 项目Gantt图(含第二次变更)
    dateFormat  YYYY-MM-DD
    axisFormat  %m-%d
    
    section 第一阶段: 需求与设计
    需求调研           :t1, 2026-03-16, 2d
    编写需求规格说明书  :t2, after t1, 2d
    需求评审           :t3, after t2, 1d
    原型设计           :t4, after t1, 2d
    架构设计           :t5, after t3, 1d
    数据库设计         :t6, after t3, 1d
    接口设计           :t7, after t5, 1d
    设计评审           :t8, after t5, 1d
    
    section 第二阶段: 核心功能开发
    企业备案模块开发    :t9, after t8, 2d
    备案信息校验       :t10, after t9, 2d
    备案审核功能       :t11, after t9, 3d
    权限管理模块       :t12, after t8, 4d
    数据填报模块开发    :t13, after t9, 2d
    校验规则实现       :t14, after t13, 2d
    条件必填逻辑       :t15, after t13, 2d
    市级初审功能       :t16, after t11, 2d
    省级复核功能       :t17, after t16, 2d
    审核流程引擎       :t18, after t8, 3d
    模块联调           :t19, after t10, 2d
    集成测试           :t20, after t19, 1d
    
    section CR-001变更: 报告频率调整
    半月报需求设计      :cr1_1, after t8, 1d
    报告周期配置开发    :cr1_2, after cr1_1, 2d
    半月报校验规则      :cr1_3, after cr1_2, 1d
    报表生成逻辑调整    :cr1_4, after cr1_3, 1d
    半月报功能测试      :cr1_5, after cr1_4, 1d
    
    section 第三阶段: 数据分析
    折线图展示         :t21, after cr1_5, 2d
    数据对比逻辑       :t22, after cr1_5, 2d
    趋势数据计算       :t23, after t22, 2d
    趋势图展示         :t24, after t23, 2d
    饼图展示           :t25, after t21, 2d
    取样数据计算       :t26, after t23, 1d
    Excel导出         :t27, after t23, 2d
    PDF导出           :t28, after t23, 2d
    导出性能优化       :t29, after t27, 1d
    数据库优化         :t30, after t29, 1d
    查询优化           :t31, after t30, 1d
    性能测试           :t32, after t31, 1d
    
    section CR-002变更: 移动端适配
    移动端需求分析      :cr2_1, after cr1_5, 2d
    移动端UI设计       :cr2_2, after cr2_1, 2d
    移动端架构设计      :cr2_3, after cr2_1, 2d
    iOS端开发         :cr2_4, after cr2_2, 8d
    Android端开发     :cr2_5, after cr2_2, 8d
    移动端后端接口      :cr2_6, after cr2_3, 6d
    消息推送服务对接    :cr2_7, after cr2_6, 2d
    移动端功能测试      :cr2_8, after cr2_4, 3d
    移动端兼容性测试    :cr2_9, after cr2_8, 2d
    移动端安全测试      :cr2_10, after cr2_8, 2d
    试点运行           :cr2_11, after cr2_9, 2d
    用户培训           :cr2_12, after cr2_11, 1d
    移动端上线         :cr2_13, after cr2_12, 1d
    
    section 第四阶段: 测试与上线
    功能测试           :t33, after t32, 1d
    性能测试(系统)     :t34, after t33, 1d
    安全测试           :t35, after t33, 1d
    UAT环境部署        :t36, after t34, 1d
    UAT测试执行        :t37, after t36, 1d
    问题修复           :t38, after t37, 1d
    试点企业选择       :t39, after t38, 1d
    试点培训           :t40, after t39, 1d
    试点数据填报       :t41, after t40, 1d
    试点问题收集       :t42, after t41, 1d
    上线方案制定       :t43, after t42, 1d
    生产环境部署       :t44, after t43, 1d
    上线验证           :t45, after t44, 1d
    
    section 里程碑
    M1: 需求基准化     :milestone, m1, 2026-03-20, 0d
    M2: 核心功能完成   :milestone, m2, after cr2_4, 0d
    M3: 数据分析上线   :milestone, m3, after t32, 0d
    M4: 系统试运行     :milestone, m4, after cr2_13, 0d
```

---

## 方式二: HTML+JavaScript(交互式Gantt图)

创建文件 `gantt-chart.html`:

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>云南省企业就业失业数据采集系统 - Gantt图(含第二次变更)</title>
    <script src="https://cdn.jsdelivr.net/npm/frappe-gantt@0.6.1/dist/frappe-gantt.min.js"></script>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/frappe-gantt@0.6.1/dist/frappe-gantt.css">
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, "PingFang SC", "Microsoft YaHei", sans-serif;
            margin: 0;
            padding: 20px;
            background: #f5f7fa;
        }
        .container {
            max-width: 1600px;
            margin: 0 auto;
            background: white;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 2px 12px rgba(0,0,0,0.1);
        }
        h1 {
            color: #2c3e50;
            text-align: center;
            margin-bottom: 10px;
        }
        .subtitle {
            text-align: center;
            color: #7f8c8d;
            margin-bottom: 30px;
        }
        .gantt-container {
            overflow-x: auto;
        }
        .gantt-target {
            min-width: 1400px;
        }
        .legend {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 20px;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 6px;
            flex-wrap: wrap;
        }
        .legend-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }
        .legend-color {
            width: 20px;
            height: 12px;
            border-radius: 3px;
        }
        .stats {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 15px;
            margin-top: 20px;
        }
        .stat-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px;
            border-radius: 8px;
            text-align: center;
        }
        .stat-card h3 {
            margin: 0 0 10px 0;
            font-size: 14px;
            opacity: 0.9;
        }
        .stat-card .value {
            font-size: 28px;
            font-weight: bold;
        }
        .controls {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 20px;
        }
        .btn {
            padding: 8px 20px;
            border: 1px solid #dcdfe6;
            background: white;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.3s;
        }
        .btn:hover {
            background: #667eea;
            color: white;
            border-color: #667eea;
        }
        .btn.active {
            background: #667eea;
            color: white;
            border-color: #667eea;
        }
        .change-info {
            margin-top: 20px;
            padding: 15px;
            background: #fff3cd;
            border-left: 4px solid #ffc107;
            border-radius: 4px;
        }
        .change-info h3 {
            margin-top: 0;
            color: #856404;
        }
        .change-info table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 10px;
        }
        .change-info th, .change-info td {
            padding: 8px;
            border: 1px solid #dee2e6;
            text-align: left;
        }
        .change-info th {
            background: #e9ecef;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>云南省企业就业失业数据采集系统</h1>
        <p class="subtitle">项目进度Gantt图(含第二次变更) | 项目周期: 8周 | 2026年3月16日-5月10日</p>
        
        <div class="controls">
            <button class="btn" onclick="changeView('Day')">日视图</button>
            <button class="btn active" onclick="changeView('Week')">周视图</button>
            <button class="btn" onclick="changeView('Month')">月视图</button>
        </div>

        <div class="gantt-container">
            <div class="gantt-target" id="gantt"></div>
        </div>

        <div class="legend">
            <div class="legend-item">
                <div class="legend-color" style="background: #3498db;"></div>
                <span>需求与设计</span>
            </div>
            <div class="legend-item">
                <div class="legend-color" style="background: #2ecc71;"></div>
                <span>核心功能开发</span>
            </div>
            <div class="legend-item">
                <div class="legend-color" style="background: #e67e22;"></div>
                <span>数据分析</span>
            </div>
            <div class="legend-item">
                <div class="legend-color" style="background: #9b59b6;"></div>
                <span>测试与上线</span>
            </div>
            <div class="legend-item">
                <div class="legend-color" style="background: #f1c40f;"></div>
                <span>CR-001: 报告频率</span>
            </div>
            <div class="legend-item">
                <div class="legend-color" style="background: #e74c3c;"></div>
                <span>CR-002: 移动端</span>
            </div>
        </div>

        <div class="change-info">
            <h3>⚠️ 第二次变更影响详情 (CR-2026-002)</h3>
            <table>
                <tr>
                    <th>项目</th>
                    <th>原始计划</th>
                    <th>CR-001后</th>
                    <th>CR-002后</th>
                    <th>总延期</th>
                </tr>
                <tr>
                    <td>项目周期</td>
                    <td>6周 (42天)</td>
                    <td>7周 (47天)</td>
                    <td>8周 (56天)</td>
                    <td>+14天</td>
                </tr>
                <tr>
                    <td>M2 核心功能完成</td>
                    <td>3月31日</td>
                    <td>4月5日</td>
                    <td>4月19日</td>
                    <td>+19天</td>
                </tr>
                <tr>
                    <td>M3 数据分析上线</td>
                    <td>4月10日</td>
                    <td>4月17日</td>
                    <td>4月24日</td>
                    <td>+14天</td>
                </tr>
                <tr>
                    <td>M4 系统试运行</td>
                    <td>4月26日</td>
                    <td>4月30日</td>
                    <td>5月10日</td>
                    <td>+14天</td>
                </tr>
            </table>
            <p style="margin-top: 10px;"><strong>CR-002新增任务: 13个</strong> (移动端需求分析→移动端上线)</p>
            <p><strong>CR-002总工期: 31天</strong> (4月6日-5月6日)</p>
            <p><strong>CR-002成本: ¥180,000元</strong> (iOS/Android开发、测试、设备采购)</p>
        </div>

        <div class="stats">
            <div class="stat-card">
                <h3>总任务数</h3>
                <div class="value">58</div>
            </div>
            <div class="stat-card" style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);">
                <h3>里程碑</h3>
                <div class="value">4</div>
            </div>
            <div class="stat-card" style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);">
                <h3>项目周期</h3>
                <div class="value">8周</div>
            </div>
            <div class="stat-card" style="background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);">
                <h3>变更成本</h3>
                <div class="value">¥19.5万</div>
            </div>
        </div>
    </div>

    <script>
        // 任务数据
        const tasks = [
            // 第一阶段: 需求与设计 (3月16-22日)
            {
                id: 't1',
                name: '需求调研',
                start: '2026-03-16',
                end: '2026-03-17',
                progress: 100,
                dependencies: '',
                custom_class: 'bar-blue'
            },
            {
                id: 't2',
                name: '编写需求规格说明书',
                start: '2026-03-18',
                end: '2026-03-19',
                progress: 80,
                dependencies: 't1',
                custom_class: 'bar-blue'
            },
            {
                id: 't3',
                name: '需求评审',
                start: '2026-03-20',
                end: '2026-03-20',
                progress: 0,
                dependencies: 't2',
                custom_class: 'bar-blue'
            },
            {
                id: 't4',
                name: '原型设计',
                start: '2026-03-18',
                end: '2026-03-19',
                progress: 60,
                dependencies: 't1',
                custom_class: 'bar-blue'
            },
            {
                id: 't5',
                name: '架构设计',
                start: '2026-03-21',
                end: '2026-03-21',
                progress: 0,
                dependencies: 't3',
                custom_class: 'bar-blue'
            },
            {
                id: 't6',
                name: '数据库设计',
                start: '2026-03-21',
                end: '2026-03-21',
                progress: 0,
                dependencies: 't3',
                custom_class: 'bar-blue'
            },
            {
                id: 't7',
                name: '接口设计',
                start: '2026-03-22',
                end: '2026-03-22',
                progress: 0,
                dependencies: 't5',
                custom_class: 'bar-blue'
            },
            {
                id: 't8',
                name: '设计评审',
                start: '2026-03-22',
                end: '2026-03-22',
                progress: 0,
                dependencies: 't5',
                custom_class: 'bar-blue'
            },
            {
                id: 'm1',
                name: '◆ M1: 需求基准化',
                start: '2026-03-20',
                end: '2026-03-20',
                progress: 0,
                dependencies: 't3',
                custom_class: 'bar-milestone'
            },

            // 第二阶段: 核心功能开发 (3月23日-4月5日)
            {
                id: 't9',
                name: '企业备案模块开发',
                start: '2026-03-23',
                end: '2026-03-24',
                progress: 0,
                dependencies: 't8',
                custom_class: 'bar-green'
            },
            {
                id: 't10',
                name: '备案信息校验',
                start: '2026-03-25',
                end: '2026-03-26',
                progress: 0,
                dependencies: 't9',
                custom_class: 'bar-green'
            },
            {
                id: 't11',
                name: '备案审核功能',
                start: '2026-03-25',
                end: '2026-03-27',
                progress: 0,
                dependencies: 't9',
                custom_class: 'bar-green'
            },
            {
                id: 't12',
                name: '权限管理模块',
                start: '2026-03-23',
                end: '2026-03-26',
                progress: 0,
                dependencies: 't8',
                custom_class: 'bar-green'
            },
            {
                id: 't13',
                name: '数据填报模块开发',
                start: '2026-03-25',
                end: '2026-03-26',
                progress: 0,
                dependencies: 't9',
                custom_class: 'bar-green'
            },
            {
                id: 't14',
                name: '校验规则实现',
                start: '2026-03-27',
                end: '2026-03-28',
                progress: 0,
                dependencies: 't13',
                custom_class: 'bar-green'
            },
            {
                id: 't15',
                name: '条件必填逻辑',
                start: '2026-03-27',
                end: '2026-03-28',
                progress: 0,
                dependencies: 't13',
                custom_class: 'bar-green'
            },
            {
                id: 't16',
                name: '市级初审功能',
                start: '2026-03-30',
                end: '2026-03-31',
                progress: 0,
                dependencies: 't11',
                custom_class: 'bar-green'
            },
            {
                id: 't17',
                name: '省级复核功能',
                start: '2026-04-01',
                end: '2026-04-02',
                progress: 0,
                dependencies: 't16',
                custom_class: 'bar-green'
            },
            {
                id: 't18',
                name: '审核流程引擎',
                start: '2026-03-23',
                end: '2026-03-25',
                progress: 0,
                dependencies: 't8',
                custom_class: 'bar-green'
            },
            {
                id: 't19',
                name: '模块联调',
                start: '2026-03-29',
                end: '2026-03-30',
                progress: 0,
                dependencies: 't10',
                custom_class: 'bar-green'
            },
            {
                id: 't20',
                name: '集成测试',
                start: '2026-03-31',
                end: '2026-03-31',
                progress: 0,
                dependencies: 't19',
                custom_class: 'bar-green'
            },

            // CR-001: 报告频率调整
            {
                id: 'cr1_1',
                name: '[CR-001] 半月报需求设计',
                start: '2026-03-23',
                end: '2026-03-23',
                progress: 0,
                dependencies: 't8',
                custom_class: 'bar-yellow'
            },
            {
                id: 'cr1_2',
                name: '[CR-001] 报告周期配置开发',
                start: '2026-03-24',
                end: '2026-03-25',
                progress: 0,
                dependencies: 'cr1_1',
                custom_class: 'bar-yellow'
            },
            {
                id: 'cr1_3',
                name: '[CR-001] 半月报校验规则',
                start: '2026-03-26',
                end: '2026-03-26',
                progress: 0,
                dependencies: 'cr1_2',
                custom_class: 'bar-yellow'
            },
            {
                id: 'cr1_4',
                name: '[CR-001] 报表生成逻辑调整',
                start: '2026-03-27',
                end: '2026-03-27',
                progress: 0,
                dependencies: 'cr1_3',
                custom_class: 'bar-yellow'
            },
            {
                id: 'cr1_5',
                name: '[CR-001] 半月报功能测试',
                start: '2026-03-28',
                end: '2026-03-28',
                progress: 0,
                dependencies: 'cr1_4',
                custom_class: 'bar-yellow'
            },

            // 第三阶段: 数据分析 (4月6-19日)
            {
                id: 't21',
                name: '折线图展示',
                start: '2026-04-06',
                end: '2026-04-07',
                progress: 0,
                dependencies: 'cr1_5',
                custom_class: 'bar-orange'
            },
            {
                id: 't22',
                name: '数据对比逻辑',
                start: '2026-04-06',
                end: '2026-04-07',
                progress: 0,
                dependencies: 'cr1_5',
                custom_class: 'bar-orange'
            },
            {
                id: 't23',
                name: '趋势数据计算',
                start: '2026-04-08',
                end: '2026-04-09',
                progress: 0,
                dependencies: 't22',
                custom_class: 'bar-orange'
            },
            {
                id: 't24',
                name: '趋势图展示',
                start: '2026-04-10',
                end: '2026-04-11',
                progress: 0,
                dependencies: 't23',
                custom_class: 'bar-orange'
            },
            {
                id: 't25',
                name: '饼图展示',
                start: '2026-04-08',
                end: '2026-04-09',
                progress: 0,
                dependencies: 't21',
                custom_class: 'bar-orange'
            },
            {
                id: 't26',
                name: '取样数据计算',
                start: '2026-04-10',
                end: '2026-04-10',
                progress: 0,
                dependencies: 't23',
                custom_class: 'bar-orange'
            },
            {
                id: 't27',
                name: 'Excel导出',
                start: '2026-04-10',
                end: '2026-04-11',
                progress: 0,
                dependencies: 't23',
                custom_class: 'bar-orange'
            },
            {
                id: 't28',
                name: 'PDF导出',
                start: '2026-04-10',
                end: '2026-04-11',
                progress: 0,
                dependencies: 't23',
                custom_class: 'bar-orange'
            },
            {
                id: 't29',
                name: '导出性能优化',
                start: '2026-04-12',
                end: '2026-04-12',
                progress: 0,
                dependencies: 't27',
                custom_class: 'bar-orange'
            },
            {
                id: 't30',
                name: '数据库优化',
                start: '2026-04-13',
                end: '2026-04-13',
                progress: 0,
                dependencies: 't29',
                custom_class: 'bar-orange'
            },
            {
                id: 't31',
                name: '查询优化',
                start: '2026-04-14',
                end: '2026-04-14',
                progress: 0,
                dependencies: 't30',
                custom_class: 'bar-orange'
            },
            {
                id: 't32',
                name: '性能测试',
                start: '2026-04-15',
                end: '2026-04-15',
                progress: 0,
                dependencies: 't31',
                custom_class: 'bar-orange'
            },

            // CR-002: 移动端适配 (4月6日-5月6日)
            {
                id: 'cr2_1',
                name: '[CR-002] 移动端需求分析',
                start: '2026-04-06',
                end: '2026-04-07',
                progress: 0,
                dependencies: 'cr1_5',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_2',
                name: '[CR-002] 移动端UI设计',
                start: '2026-04-08',
                end: '2026-04-09',
                progress: 0,
                dependencies: 'cr2_1',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_3',
                name: '[CR-002] 移动端架构设计',
                start: '2026-04-08',
                end: '2026-04-09',
                progress: 0,
                dependencies: 'cr2_1',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_4',
                name: '[CR-002] iOS端开发',
                start: '2026-04-10',
                end: '2026-04-17',
                progress: 0,
                dependencies: 'cr2_2',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_5',
                name: '[CR-002] Android端开发',
                start: '2026-04-10',
                end: '2026-04-17',
                progress: 0,
                dependencies: 'cr2_2',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_6',
                name: '[CR-002] 移动端后端接口',
                start: '2026-04-10',
                end: '2026-04-15',
                progress: 0,
                dependencies: 'cr2_3',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_7',
                name: '[CR-002] 消息推送服务对接',
                start: '2026-04-16',
                end: '2026-04-17',
                progress: 0,
                dependencies: 'cr2_6',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_8',
                name: '[CR-002] 移动端功能测试',
                start: '2026-04-18',
                end: '2026-04-20',
                progress: 0,
                dependencies: 'cr2_4',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_9',
                name: '[CR-002] 移动端兼容性测试',
                start: '2026-04-21',
                end: '2026-04-22',
                progress: 0,
                dependencies: 'cr2_8',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_10',
                name: '[CR-002] 移动端安全测试',
                start: '2026-04-21',
                end: '2026-04-22',
                progress: 0,
                dependencies: 'cr2_8',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_11',
                name: '[CR-002] 试点运行',
                start: '2026-05-03',
                end: '2026-05-04',
                progress: 0,
                dependencies: 'cr2_9',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_12',
                name: '[CR-002] 用户培训',
                start: '2026-05-05',
                end: '2026-05-05',
                progress: 0,
                dependencies: 'cr2_11',
                custom_class: 'bar-red'
            },
            {
                id: 'cr2_13',
                name: '[CR-002] 移动端上线',
                start: '2026-05-06',
                end: '2026-05-06',
                progress: 0,
                dependencies: 'cr2_12',
                custom_class: 'bar-red'
            },

            // 第四阶段: 测试与上线
            {
                id: 't33',
                name: '功能测试',
                start: '2026-04-16',
                end: '2026-04-16',
                progress: 0,
                dependencies: 't32',
                custom_class: 'bar-purple'
            },
            {
                id: 't34',
                name: '性能测试(系统)',
                start: '2026-04-17',
                end: '2026-04-17',
                progress: 0,
                dependencies: 't33',
                custom_class: 'bar-purple'
            },
            {
                id: 't35',
                name: '安全测试',
                start: '2026-04-17',
                end: '2026-04-17',
                progress: 0,
                dependencies: 't33',
                custom_class: 'bar-purple'
            },
            {
                id: 't36',
                name: 'UAT环境部署',
                start: '2026-04-18',
                end: '2026-04-18',
                progress: 0,
                dependencies: 't34',
                custom_class: 'bar-purple'
            },
            {
                id: 't37',
                name: 'UAT测试执行',
                start: '2026-04-19',
                end: '2026-04-19',
                progress: 0,
                dependencies: 't36',
                custom_class: 'bar-purple'
            },
            {
                id: 't38',
                name: '问题修复',
                start: '2026-04-20',
                end: '2026-04-20',
                progress: 0,
                dependencies: 't37',
                custom_class: 'bar-purple'
            },
            {
                id: 't39',
                name: '试点企业选择',
                start: '2026-04-23',
                end: '2026-04-23',
                progress: 0,
                dependencies: 't38',
                custom_class: 'bar-purple'
            },
            {
                id: 't40',
                name: '试点培训',
                start: '2026-04-24',
                end: '2026-04-24',
                progress: 0,
                dependencies: 't39',
                custom_class: 'bar-purple'
            },
            {
                id: 't41',
                name: '试点数据填报',
                start: '2026-04-25',
                end: '2026-04-25',
                progress: 0,
                dependencies: 't40',
                custom_class: 'bar-purple'
            },
            {
                id: 't42',
                name: '试点问题收集',
                start: '2026-04-26',
                end: '2026-04-26',
                progress: 0,
                dependencies: 't41',
                custom_class: 'bar-purple'
            },
            {
                id: 't43',
                name: '上线方案制定',
                start: '2026-04-27',
                end: '2026-04-27',
                progress: 0,
                dependencies: 't42',
                custom_class: 'bar-purple'
            },
            {
                id: 't44',
                name: '生产环境部署',
                start: '2026-04-28',
                end: '2026-04-28',
                progress: 0,
                dependencies: 't43',
                custom_class: 'bar-purple'
            },
            {
                id: 't45',
                name: '上线验证',
                start: '2026-04-29',
                end: '2026-04-29',
                progress: 0,
                dependencies: 't44',
                custom_class: 'bar-purple'
            },

            // 里程碑
            {
                id: 'm1',
                name: '◆ M1: 需求基准化 (3月20日)',
                start: '2026-03-20',
                end: '2026-03-20',
                progress: 0,
                dependencies: 't3',
                custom_class: 'bar-milestone'
            },
            {
                id: 'm2',
                name: '◆ M2: 核心功能完成 (4月19日)',
                start: '2026-04-19',
                end: '2026-04-19',
                progress: 0,
                dependencies: 'cr2_4',
                custom_class: 'bar-milestone'
            },
            {
                id: 'm3',
                name: '◆ M3: 数据分析上线 (4月24日)',
                start: '2026-04-24',
                end: '2026-04-24',
                progress: 0,
                dependencies: 't32',
                custom_class: 'bar-milestone'
            },
            {
                id: 'm4',
                name: '◆ M4: 系统试运行 (5月10日)',
                start: '2026-05-10',
                end: '2026-05-10',
                progress: 0,
                dependencies: 'cr2_13',
                custom_class: 'bar-milestone'
            }
        ];

        // 初始化Gantt图
        let gantt;
        
        function initGantt(viewMode = 'Week') {
            gantt = new Gantt("#gantt", tasks, {
                header_height: 50,
                column_width: 30,
                step: 24,
                view_modes: ['Quarter Day', 'Half Day', 'Day', 'Week', 'Month'],
                bar_height: 25,
                bar_corner_radius: 3,
                arrow_curve: 5,
                padding: 18,
                view_mode: viewMode,
                date_format: 'YYYY-MM-DD',
                custom_popup_html: function(task) {
                    return `
                        <div style="padding: 15px; min-width: 250px;">
                            <h4 style="margin: 0 0 10px 0; color: #2c3e50;">${task.name}</h4>
                            <p style="margin: 5px 0; color: #7f8c8d;">
                                <strong>开始:</strong> ${task.start}<br>
                                <strong>结束:</strong> ${task.end}<br>
                                <strong>进度:</strong> ${task.progress}%<br>
                                ${task.dependencies ? `<strong>前置任务:</strong> ${task.dependencies}` : ''}
                            </p>
                        </div>
                    `;
                }
            });
        }

        function changeView(mode) {
            if (gantt) {
                gantt.change_view_mode(mode);
                document.querySelectorAll('.btn').forEach(btn => btn.classList.remove('active'));
                event.target.classList.add('active');
            }
        }

        // 添加自定义样式
        const style = document.createElement('style');
        style.textContent = `
            .bar-blue { fill: #3498db !important; }
            .bar-green { fill: #2ecc71 !important; }
            .bar-orange { fill: #e67e22 !important; }
            .bar-purple { fill: #9b59b6 !important; }
            .bar-yellow { fill: #f1c40f !important; }
            .bar-red { fill: #e74c3c !important; }
            .bar-milestone { fill: #e74c3c !important; }
            .gantt .bar-label { fill: white; font-size: 11px; }
            .gantt .bar-progress { fill: rgba(255,255,255,0.3); }
        `;
        document.head.appendChild(style);

        // 页面加载后初始化
        window.onload = () => initGantt('Week');
    </script>
</body>
</html>
```

---

## 项目变更影响总结

### 原始计划 vs 变更后计划对比

| 项目 | 原始计划 | CR-001后 | CR-002后 | 总差异 |
|------|---------|---------|---------|--------|
| 项目周期 | 6周 (42天) | 7周 (47天) | 8周 (56天) | **+14天** |
| 开始日期 | 2026-03-16 | 2026-03-16 | 2026-03-16 | 不变 |
| 结束日期 | 2026-04-26 | 2026-04-30 | 2026-05-10 | **+14天** |
| 总任务数 | 45个 | 50个 | 58个 | **+13个** |
| 里程碑 | 4个 | 4个 | 4个 | 不变 |

### 里程碑调整对比

| 里程碑 | 原始日期 | CR-001后 | CR-002后 | 总延期 |
|--------|---------|---------|---------|--------|
| M1: 需求基准化 | 3月20日 | 3月20日 | 3月20日 | 0天 |
| M2: 核心功能完成 | 3月31日 | 4月5日 | 4月19日 | +19天 |
| M3: 数据分析上线 | 4月10日 | 4月17日 | 4月24日 | +14天 |
| M4: 系统试运行 | 4月26日 | 4月30日 | 5月10日 | +14天 |

### 成本影响

| 变更项 | 开发成本 | 测试成本 | 其他成本 | 合计 |
|--------|---------|---------|---------|------|
| CR-001: 报告频率 | ¥9,000 | ¥5,000 | ¥1,000 | ¥15,000 |
| CR-002: 移动端 | ¥240,000 | ¥75,000 | ¥60,000 | ¥375,000 |
| 减: 复用逻辑 | -¥190,000 | - | - | -¥190,000 |
| **总成本** | **¥59,000** | **¥80,000** | **¥61,000** | **¥200,000** |

---

## 使用指南

### 方式一: Mermaid(最简单)
1. 在任何支持Mermaid的Markdown编辑器中打开
2. 或者在GitHub/GitLab中直接查看
3. 无需安装任何工具

**在线编辑器:**
- https://mermaid.live
- 粘贴代码即可预览

### 方式二: HTML+JavaScript(最美观)
```bash
# 1. 保存为 gantt-chart.html
# 2. 双击打开即可
# 或使用本地服务器
python -m http.server 8080
# 访问 http://localhost:8080/gantt-chart.html
```

**特性:**
- ✅ 交互式: 日/周/月视图切换
- ✅ 悬停显示任务详情
- ✅ 依赖关系可视化
- ✅ 进度条显示
- ✅ 统计面板
- ✅ 变更影响摘要(表格形式)

---

## 项目文档总结

| 类别 | 文档数 | 主要文档 |
|------|--------|---------|
| 管理类 | 5份 | 进度计划、干系人管理、迭代计划、优化路线图 |
| 需求类 | 3份 | 需求规格说明书、数据校验规则、需求变更管理 |
| 设计类 | 8份 | 架构设计、权限管理、配置管理、国家系统对接 |
| 测试类 | 6份 | 风险管理、质量保证、UAT测试、性能测试 |
| 部署类 | 1份 | 系统部署与运维方案 |
| 变更管理 | 2份 | 变更申请单、变更通知单 |
| 文档管理 | 2份 | 文档管理规范、文档索引 |
| **总计** | **27份** | **覆盖45个管理特点+2次变更** |

选择最适合你的方式生成Gantt图吧! 🎨
