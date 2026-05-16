import csv
from collections import defaultdict

# 读取CSV文件
with open(r'h:\视频内容\uap-release001.csv', 'r', encoding='utf-8') as f:
    reader = csv.DictReader(f)
    rows = list(reader)

# 按部门分组
dept_war = []
fbi = []
nasa = []
dept_state = []

for row in rows:
    agency = row.get('Agency', '').strip()
    if agency == 'Department of War':
        dept_war.append(row)
    elif agency == 'FBI':
        fbi.append(row)
    elif agency == 'NASA':
        nasa.append(row)
    elif agency == 'Department of State':
        dept_state.append(row)

# 生成Markdown
md = f"""# 🛸 UAP官方解密档案库 - Release 001

> **发布日期**: 2026年5月8日  
> **总档案数**: {len(rows)}份  
> **数据来源**: 美国政府官方解密文件

---

## 📊 档案统计总览

| 统计项 | 数量 |
|--------|------|
| **总档案数** | {len(rows)} |
| **PDF文档** | 116 |
| **视频档案(VID)** | 28 |
| **图像档案(IMG)** | 14 |

### 按部门统计

| 部门 | 档案数量 |
|------|---------|
| Department of War (战争部) | {len(dept_war)} |
| FBI (联邦调查局) | {len(fbi)} |
| NASA (国家航空航天局) | {len(nasa)} |
| Department of State (国务院) | {len(dept_state)} |

---

## 🏛️ 按部门分类档案

---

"""

# Department of War
md += f"""### 1️⃣ Department of War (战争部) - {len(dept_war)}份档案

"""

for i, row in enumerate(dept_war, 1):
    title = row.get('Title', '').strip()
    file_type = row.get('Type', '').strip()
    incident_date = row.get('Incident Date', '').strip()
    location = row.get('Incident Location', '').strip()
    description = row.get('Description Blurb', '').strip()
    if len(description) > 300:
        description = description[:300] + '...'
    pdf_link = row.get('PDF | Image Link', '').strip()
    video_id = row.get('DVIDS Video ID', '').strip()
    
    md += f"""#### {i}. {title}

| 属性 | 内容 |
|------|------|
| **类型** | {file_type} |
| **事件日期** | {incident_date if incident_date else 'N/A'} |
| **事件地点** | {location if location else 'N/A'} |
| **视频ID** | {video_id if video_id else 'N/A'} |

**描述**: {description}

"""
    if pdf_link:
        md += f"📥 **下载链接**: [点击下载]({pdf_link})\n\n"
    md += "---\n\n"

# FBI
md += f"""### 2️⃣ FBI (联邦调查局) - {len(fbi)}份档案

"""

for i, row in enumerate(fbi, 1):
    title = row.get('Title', '').strip()
    file_type = row.get('Type', '').strip()
    incident_date = row.get('Incident Date', '').strip()
    location = row.get('Incident Location', '').strip()
    description = row.get('Description Blurb', '').strip()
    if len(description) > 300:
        description = description[:300] + '...'
    pdf_link = row.get('PDF | Image Link', '').strip()
    
    md += f"""#### {i}. {title}

| 属性 | 内容 |
|------|------|
| **类型** | {file_type} |
| **事件日期** | {incident_date if incident_date else 'N/A'} |
| **事件地点** | {location if location else 'N/A'} |

**描述**: {description}

"""
    if pdf_link:
        md += f"📥 **下载链接**: [点击下载]({pdf_link})\n\n"
    md += "---\n\n"

# NASA
md += f"""### 3️⃣ NASA (国家航空航天局) - {len(nasa)}份档案

"""

for i, row in enumerate(nasa, 1):
    title = row.get('Title', '').strip()
    file_type = row.get('Type', '').strip()
    incident_date = row.get('Incident Date', '').strip()
    location = row.get('Incident Location', '').strip()
    description = row.get('Description Blurb', '').strip()
    if len(description) > 300:
        description = description[:300] + '...'
    pdf_link = row.get('PDF | Image Link', '').strip()
    
    md += f"""#### {i}. {title}

| 属性 | 内容 |
|------|------|
| **类型** | {file_type} |
| **事件日期** | {incident_date if incident_date else 'N/A'} |
| **事件地点** | {location if location else 'N/A'} |

**描述**: {description}

"""
    if pdf_link:
        md += f"📥 **下载链接**: [点击下载]({pdf_link})\n\n"
    md += "---\n\n"

# Department of State
md += f"""### 4️⃣ Department of State (国务院) - {len(dept_state)}份档案

"""

for i, row in enumerate(dept_state, 1):
    title = row.get('Title', '').strip()
    file_type = row.get('Type', '').strip()
    incident_date = row.get('Incident Date', '').strip()
    location = row.get('Incident Location', '').strip()
    description = row.get('Description Blurb', '').strip()
    if len(description) > 300:
        description = description[:300] + '...'
    pdf_link = row.get('PDF | Image Link', '').strip()
    
    md += f"""#### {i}. {title}

| 属性 | 内容 |
|------|------|
| **类型** | {file_type} |
| **事件日期** | {incident_date if incident_date else 'N/A'} |
| **事件地点** | {location if location else 'N/A'} |

**描述**: {description}

"""
    if pdf_link:
        md += f"📥 **下载链接**: [点击下载]({pdf_link})\n\n"
    md += "---\n\n"

md += """---

## ⚠️ 重要说明

> **免责声明**: 本档案库中所有描述性和估计性语言均反映报告者在事件发生时的主观解释。此类描述不应被解释为对所描述事件的有效性、性质或重要性的分析判断、调查结论或事实确定的结论性指示。

---

<div align="center">

**最后更新**: 2026年5月8日  
**数据来源**: 美国政府官方解密档案  
**档案总数**: 158份

</div>
"""

# 写入文件
with open(r'h:\视频内容\uap-release001.md', 'w', encoding='utf-8') as f:
    f.write(md)

print("Markdown文档生成成功！")
print(f"总档案数: {len(rows)}")
print(f"Department of War: {len(dept_war)}份")
print(f"FBI: {len(fbi)}份")
print(f"NASA: {len(nasa)}份")
print(f"Department of State: {len(dept_state)}份")
