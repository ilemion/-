# Gantt图生成代码

本项目提供3种方式生成Gantt图:
1. **Mermaid语法** - Markdown原生支持,最简单
2. **HTML+JavaScript** - 交互式Gantt图,最美观
3. **Python** - 可导出图片,最灵活

**项目周期: 2026年3月16日-4月26日 (共42天/6周)**

---

## 方式一: Mermaid语法(推荐,最简单)

直接在Markdown中渲染,GitHub支持!

```mermaid
gantt
    title 云南省企业就业失业数据采集系统 - 项目Gantt图
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
    
    section 第三阶段: 数据分析
    折线图展示         :t21, after t20, 2d
    数据对比逻辑       :t22, after t20, 2d
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
    M1: 需求基准化     :milestone, m1, after t3, 0d
    M2: 核心功能完成   :milestone, m2, after t20, 0d
    M3: 数据分析上线   :milestone, m3, after t32, 0d
    M4: 系统试运行     :milestone, m4, after t45, 0d
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
    <title>云南省企业就业失业数据采集系统 - Gantt图</title>
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
            max-width: 1400px;
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
            min-width: 1200px;
        }
        .legend {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 20px;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 6px;
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
    </style>
</head>
<body>
    <div class="container">
        <h1>云南省企业就业失业数据采集系统</h1>
        <p class="subtitle">项目进度Gantt图 | 项目周期: 6周 | 2026年3月16日-4月26日</p>
        
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
        </div>

        <div class="stats">
            <div class="stat-card">
                <h3>总任务数</h3>
                <div class="value">45</div>
            </div>
            <div class="stat-card" style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);">
                <h3>里程碑</h3>
                <div class="value">4</div>
            </div>
            <div class="stat-card" style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);">
                <h3>项目周期</h3>
                <div class="value">6周</div>
            </div>
            <div class="stat-card" style="background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);">
                <h3>关键路径</h3>
                <div class="value">11任务</div>
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
            {
                id: 'm2',
                name: '◆ M2: 核心功能完成',
                start: '2026-03-31',
                end: '2026-03-31',
                progress: 0,
                dependencies: 't20',
                custom_class: 'bar-milestone'
            },

            // 第三阶段: 数据分析 (4月1-19日)
            {
                id: 't21',
                name: '折线图展示',
                start: '2026-04-01',
                end: '2026-04-02',
                progress: 0,
                dependencies: 't20',
                custom_class: 'bar-orange'
            },
            {
                id: 't22',
                name: '数据对比逻辑',
                start: '2026-04-01',
                end: '2026-04-02',
                progress: 0,
                dependencies: 't20',
                custom_class: 'bar-orange'
            },
            {
                id: 't23',
                name: '趋势数据计算',
                start: '2026-04-03',
                end: '2026-04-04',
                progress: 0,
                dependencies: 't22',
                custom_class: 'bar-orange'
            },
            {
                id: 't24',
                name: '趋势图展示',
                start: '2026-04-05',
                end: '2026-04-06',
                progress: 0,
                dependencies: 't23',
                custom_class: 'bar-orange'
            },
            {
                id: 't25',
                name: '饼图展示',
                start: '2026-04-03',
                end: '2026-04-04',
                progress: 0,
                dependencies: 't21',
                custom_class: 'bar-orange'
            },
            {
                id: 't26',
                name: '取样数据计算',
                start: '2026-04-05',
                end: '2026-04-05',
                progress: 0,
                dependencies: 't23',
                custom_class: 'bar-orange'
            },
            {
                id: 't27',
                name: 'Excel导出',
                start: '2026-04-05',
                end: '2026-04-06',
                progress: 0,
                dependencies: 't23',
                custom_class: 'bar-orange'
            },
            {
                id: 't28',
                name: 'PDF导出',
                start: '2026-04-05',
                end: '2026-04-06',
                progress: 0,
                dependencies: 't23',
                custom_class: 'bar-orange'
            },
            {
                id: 't29',
                name: '导出性能优化',
                start: '2026-04-07',
                end: '2026-04-07',
                progress: 0,
                dependencies: 't27',
                custom_class: 'bar-orange'
            },
            {
                id: 't30',
                name: '数据库优化',
                start: '2026-04-08',
                end: '2026-04-08',
                progress: 0,
                dependencies: 't29',
                custom_class: 'bar-orange'
            },
            {
                id: 't31',
                name: '查询优化',
                start: '2026-04-09',
                end: '2026-04-09',
                progress: 0,
                dependencies: 't30',
                custom_class: 'bar-orange'
            },
            {
                id: 't32',
                name: '性能测试',
                start: '2026-04-10',
                end: '2026-04-10',
                progress: 0,
                dependencies: 't31',
                custom_class: 'bar-orange'
            },
            {
                id: 'm3',
                name: '◆ M3: 数据分析上线',
                start: '2026-04-10',
                end: '2026-04-10',
                progress: 0,
                dependencies: 't32',
                custom_class: 'bar-milestone'
            },

            // 第四阶段: 测试与上线 (4月13-26日)
            {
                id: 't33',
                name: '功能测试',
                start: '2026-04-13',
                end: '2026-04-13',
                progress: 0,
                dependencies: 't32',
                custom_class: 'bar-purple'
            },
            {
                id: 't34',
                name: '性能测试(系统)',
                start: '2026-04-14',
                end: '2026-04-14',
                progress: 0,
                dependencies: 't33',
                custom_class: 'bar-purple'
            },
            {
                id: 't35',
                name: '安全测试',
                start: '2026-04-14',
                end: '2026-04-14',
                progress: 0,
                dependencies: 't33',
                custom_class: 'bar-purple'
            },
            {
                id: 't36',
                name: 'UAT环境部署',
                start: '2026-04-15',
                end: '2026-04-15',
                progress: 0,
                dependencies: 't34',
                custom_class: 'bar-purple'
            },
            {
                id: 't37',
                name: 'UAT测试执行',
                start: '2026-04-16',
                end: '2026-04-16',
                progress: 0,
                dependencies: 't36',
                custom_class: 'bar-purple'
            },
            {
                id: 't38',
                name: '问题修复',
                start: '2026-04-17',
                end: '2026-04-17',
                progress: 0,
                dependencies: 't37',
                custom_class: 'bar-purple'
            },
            {
                id: 't39',
                name: '试点企业选择',
                start: '2026-04-20',
                end: '2026-04-20',
                progress: 0,
                dependencies: 't38',
                custom_class: 'bar-purple'
            },
            {
                id: 't40',
                name: '试点培训',
                start: '2026-04-21',
                end: '2026-04-21',
                progress: 0,
                dependencies: 't39',
                custom_class: 'bar-purple'
            },
            {
                id: 't41',
                name: '试点数据填报',
                start: '2026-04-22',
                end: '2026-04-22',
                progress: 0,
                dependencies: 't40',
                custom_class: 'bar-purple'
            },
            {
                id: 't42',
                name: '试点问题收集',
                start: '2026-04-23',
                end: '2026-04-23',
                progress: 0,
                dependencies: 't41',
                custom_class: 'bar-purple'
            },
            {
                id: 't43',
                name: '上线方案制定',
                start: '2026-04-24',
                end: '2026-04-24',
                progress: 0,
                dependencies: 't42',
                custom_class: 'bar-purple'
            },
            {
                id: 't44',
                name: '生产环境部署',
                start: '2026-04-25',
                end: '2026-04-25',
                progress: 0,
                dependencies: 't43',
                custom_class: 'bar-purple'
            },
            {
                id: 't45',
                name: '上线验证',
                start: '2026-04-26',
                end: '2026-04-26',
                progress: 0,
                dependencies: 't44',
                custom_class: 'bar-purple'
            },
            {
                id: 'm4',
                name: '◆ M4: 系统试运行',
                start: '2026-04-26',
                end: '2026-04-26',
                progress: 0,
                dependencies: 't45',
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

## 方式三: Python代码(可导出图片)

创建文件 `generate_gantt.py`:

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
云南省企业就业失业数据采集系统 - Gantt图生成器
依赖: pip install matplotlib pandas
"""

import matplotlib.pyplot as plt
import matplotlib.dates as mdates
from datetime import datetime, timedelta
import pandas as pd

# 设置中文字体
plt.rcParams['font.sans-serif'] = ['Arial Unicode MS', 'SimHei', 'STHeiti']
plt.rcParams['axes.unicode_minus'] = False

# 任务数据
tasks = [
    # 第一阶段: 需求与设计
    {'name': '需求调研', 'start': '2026-03-16', 'end': '2026-03-17', 'phase': '需求与设计'},
    {'name': '编写需求规格说明书', 'start': '2026-03-18', 'end': '2026-03-19', 'phase': '需求与设计'},
    {'name': '需求评审', 'start': '2026-03-20', 'end': '2026-03-20', 'phase': '需求与设计'},
    {'name': '原型设计', 'start': '2026-03-18', 'end': '2026-03-19', 'phase': '需求与设计'},
    {'name': '架构设计', 'start': '2026-03-21', 'end': '2026-03-21', 'phase': '需求与设计'},
    {'name': '数据库设计', 'start': '2026-03-21', 'end': '2026-03-21', 'phase': '需求与设计'},
    {'name': '接口设计', 'start': '2026-03-22', 'end': '2026-03-22', 'phase': '需求与设计'},
    {'name': '设计评审', 'start': '2026-03-22', 'end': '2026-03-22', 'phase': '需求与设计'},
    
    # 第二阶段: 核心功能开发
    {'name': '企业备案模块开发', 'start': '2026-03-23', 'end': '2026-03-24', 'phase': '核心功能开发'},
    {'name': '备案信息校验', 'start': '2026-03-25', 'end': '2026-03-26', 'phase': '核心功能开发'},
    {'name': '备案审核功能', 'start': '2026-03-25', 'end': '2026-03-27', 'phase': '核心功能开发'},
    {'name': '权限管理模块', 'start': '2026-03-23', 'end': '2026-03-26', 'phase': '核心功能开发'},
    {'name': '数据填报模块开发', 'start': '2026-03-25', 'end': '2026-03-26', 'phase': '核心功能开发'},
    {'name': '校验规则实现', 'start': '2026-03-27', 'end': '2026-03-28', 'phase': '核心功能开发'},
    {'name': '条件必填逻辑', 'start': '2026-03-27', 'end': '2026-03-28', 'phase': '核心功能开发'},
    {'name': '市级初审功能', 'start': '2026-03-30', 'end': '2026-03-31', 'phase': '核心功能开发'},
    {'name': '省级复核功能', 'start': '2026-04-01', 'end': '2026-04-02', 'phase': '核心功能开发'},
    {'name': '审核流程引擎', 'start': '2026-03-23', 'end': '2026-03-25', 'phase': '核心功能开发'},
    {'name': '模块联调', 'start': '2026-03-29', 'end': '2026-03-30', 'phase': '核心功能开发'},
    {'name': '集成测试', 'start': '2026-03-31', 'end': '2026-03-31', 'phase': '核心功能开发'},
    
    # 第三阶段: 数据分析
    {'name': '折线图展示', 'start': '2026-04-01', 'end': '2026-04-02', 'phase': '数据分析'},
    {'name': '数据对比逻辑', 'start': '2026-04-01', 'end': '2026-04-02', 'phase': '数据分析'},
    {'name': '趋势数据计算', 'start': '2026-04-03', 'end': '2026-04-04', 'phase': '数据分析'},
    {'name': '趋势图展示', 'start': '2026-04-05', 'end': '2026-04-06', 'phase': '数据分析'},
    {'name': '饼图展示', 'start': '2026-04-03', 'end': '2026-04-04', 'phase': '数据分析'},
    {'name': '取样数据计算', 'start': '2026-04-05', 'end': '2026-04-05', 'phase': '数据分析'},
    {'name': 'Excel导出', 'start': '2026-04-05', 'end': '2026-04-06', 'phase': '数据分析'},
    {'name': 'PDF导出', 'start': '2026-04-05', 'end': '2026-04-06', 'phase': '数据分析'},
    {'name': '导出性能优化', 'start': '2026-04-07', 'end': '2026-04-07', 'phase': '数据分析'},
    {'name': '数据库优化', 'start': '2026-04-08', 'end': '2026-04-08', 'phase': '数据分析'},
    {'name': '查询优化', 'start': '2026-04-09', 'end': '2026-04-09', 'phase': '数据分析'},
    {'name': '性能测试', 'start': '2026-04-10', 'end': '2026-04-10', 'phase': '数据分析'},
    
    # 第四阶段: 测试与上线
    {'name': '功能测试', 'start': '2026-04-13', 'end': '2026-04-13', 'phase': '测试与上线'},
    {'name': '性能测试(系统)', 'start': '2026-04-14', 'end': '2026-04-14', 'phase': '测试与上线'},
    {'name': '安全测试', 'start': '2026-04-14', 'end': '2026-04-14', 'phase': '测试与上线'},
    {'name': 'UAT环境部署', 'start': '2026-04-15', 'end': '2026-04-15', 'phase': '测试与上线'},
    {'name': 'UAT测试执行', 'start': '2026-04-16', 'end': '2026-04-16', 'phase': '测试与上线'},
    {'name': '问题修复', 'start': '2026-04-17', 'end': '2026-04-17', 'phase': '测试与上线'},
    {'name': '试点企业选择', 'start': '2026-04-20', 'end': '2026-04-20', 'phase': '测试与上线'},
    {'name': '试点培训', 'start': '2026-04-21', 'end': '2026-04-21', 'phase': '测试与上线'},
    {'name': '试点数据填报', 'start': '2026-04-22', 'end': '2026-04-22', 'phase': '测试与上线'},
    {'name': '试点问题收集', 'start': '2026-04-23', 'end': '2026-04-23', 'phase': '测试与上线'},
    {'name': '上线方案制定', 'start': '2026-04-24', 'end': '2026-04-24', 'phase': '测试与上线'},
    {'name': '生产环境部署', 'start': '2026-04-25', 'end': '2026-04-25', 'phase': '测试与上线'},
    {'name': '上线验证', 'start': '2026-04-26', 'end': '2026-04-26', 'phase': '测试与上线'},
]

# 里程碑
milestones = [
    {'name': 'M1: 需求基准化', 'date': '2026-03-20'},
    {'name': 'M2: 核心功能完成', 'date': '2026-03-31'},
    {'name': 'M3: 数据分析上线', 'date': '2026-04-10'},
    {'name': 'M4: 系统试运行', 'date': '2026-04-26'},
]

# 颜色映射
phase_colors = {
    '需求与设计': '#3498db',
    '核心功能开发': '#2ecc71',
    '数据分析': '#e67e22',
    '测试与上线': '#9b59b6'
}

def create_gantt():
    """创建Gantt图"""
    fig, ax = plt.subplots(figsize=(20, 14))
    
    # 处理任务数据
    y_pos = len(tasks) - 1
    
    for task in reversed(tasks):
        start = datetime.strptime(task['start'], '%Y-%m-%d')
        end = datetime.strptime(task['end'], '%Y-%m-%d')
        duration = (end - start).days + 1
        
        color = phase_colors.get(task['phase'], '#95a5a6')
        
        # 绘制条形图
        ax.barh(y_pos, duration, left=start, height=0.6, 
                color=color, edgecolor='white', linewidth=1.5,
                label=task['phase'] if y_pos == len(tasks) - 1 else "")
        
        # 添加任务名称
        ax.text(start, y_pos, f" {task['name']}", 
                va='center', ha='left', fontsize=9, fontweight='bold')
        
        # 添加工期
        ax.text(end, y_pos, f" ({duration}天) ", 
                va='center', ha='right', fontsize=8, color='#666')
        
        y_pos -= 1
    
    # 添加里程碑
    for ms in milestones:
        date = datetime.strptime(ms['date'], '%Y-%m-%d')
        ax.axvline(x=date, color='red', linestyle='--', alpha=0.7, linewidth=2)
        ax.text(date, -1, f"◆ {ms['name']}", 
                rotation=90, va='bottom', ha='left', 
                fontsize=9, color='red', fontweight='bold')
    
    # 设置坐标轴
    ax.set_ylim(-2, len(tasks))
    ax.set_xlim(datetime(2026, 3, 15), datetime(2026, 4, 28))
    
    # 设置日期格式
    ax.xaxis.set_major_locator(mdates.WeekdayLocator(interval=1))
    ax.xaxis.set_major_formatter(mdates.DateFormatter('%m-%d'))
    
    # 添加网格
    ax.xaxis.grid(True, linestyle=':', alpha=0.5)
    ax.set_axisbelow(True)
    
    # 移除y轴
    ax.set_yticks([])
    
    # 标题和标签
    ax.set_title('云南省企业就业失业数据采集系统 - 项目Gantt图\n项目周期: 6周 (2026年3月16日-4月26日)', 
                 fontsize=16, fontweight='bold', pad=20)
    ax.set_xlabel('日期', fontsize=12)
    
    # 添加图例
    from matplotlib.patches import Patch
    legend_elements = [Patch(facecolor=color, edgecolor='white', label=phase) 
                      for phase, color in phase_colors.items()]
    ax.legend(handles=legend_elements, loc='upper right', fontsize=11, 
              framealpha=0.9, shadow=True)
    
    # 调整布局
    plt.tight_layout()
    
    # 保存图片
    plt.savefig('gantt-chart.png', dpi=300, bbox_inches='tight', 
                facecolor='white', edgecolor='none')
    print("✅ Gantt图已保存为 gantt-chart.png")
    
    # 显示图片
    plt.show()

if __name__ == '__main__':
    create_gantt()
```

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

### 方式三: Python(可定制)
```bash
# 1. 安装依赖
pip install matplotlib pandas

# 2. 运行脚本
python generate_gantt.py

# 3. 输出: gantt-chart.png (高清图片)
```

**特性:**
- ✅ 导出高清PNG图片
- ✅ 可自定义颜色、样式
- ✅ 支持PDF/SVG导出
- ✅ 可集成到报告中

---

## 项目时间线

| 阶段 | 时间范围 | 持续天数 | 主要任务 |
|------|----------|---------|---------|
| 第一阶段: 需求与设计 | 3月16日-22日 | 7天 | 需求调研、原型设计、架构设计 |
| 第二阶段: 核心功能开发 | 3月23日-4月5日 | 14天 | 企业备案、数据填报、审核流程 |
| 第三阶段: 数据分析 | 4月6日-19日 | 14天 | 图表展示、数据导出、性能优化 |
| 第四阶段: 测试与上线 | 4月20日-26日 | 7天 | 功能测试、UAT、试点推广、上线 |
| **总计** | **3月16日-4月26日** | **42天(6周)** | **45个任务+4个里程碑** |

## 里程碑

| 里程碑 | 日期 | 说明 |
|--------|------|------|
| M1: 需求基准化 | 3月20日 | 需求评审通过,需求基准确定 |
| M2: 核心功能完成 | 3月31日 | 所有核心功能开发完成,集成测试通过 |
| M3: 数据分析上线 | 4月10日 | 数据分析功能开发完成,性能测试通过 |
| M4: 系统试运行 | 4月26日 | 系统正式上线,开始试运行 |

---

## 项目文档总结

| 类别 | 文档数 | 主要文档 |
|------|--------|---------|
| 管理类 | 5份 | 进度计划、干系人管理、迭代计划、优化路线图 |
| 需求类 | 3份 | 需求规格说明书、数据校验规则、需求变更管理 |
| 设计类 | 8份 | 架构设计、权限管理、配置管理、国家系统对接 |
| 测试类 | 6份 | 风险管理、质量保证、UAT测试、性能测试 |
| 部署类 | 1份 | 系统部署与运维方案 |
| 文档管理 | 2份 | 文档管理规范、文档索引 |
| **总计** | **25份** | **覆盖45个管理特点** |

选择最适合你的方式生成Gantt图吧! 🎨
