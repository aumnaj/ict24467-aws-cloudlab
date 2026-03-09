# 📚 เฉลยแบบฝึกหัดและสรุปการเรียนรู้
# ICT24467 — AWS Cloud Workshop: Data Pipeline & Serverless Architecture

---

> **คณะเทคโนโลยีสารสนเทศ (School of Information Technology)**  
> มหาวิทยาลัยศรีปทุม · Sripatum University  
>
> | | |
> |---|---|
> | **รายวิชา** | ICT24467 — Cloud Computing Software Development and Data Security |
> | **ภาคการศึกษา** | 2 / 2568 |
> | **อาจารย์ผู้สอน** | อ.อำนาจ คงเจริญถิ่น |
> | **เอกสารนี้** | เฉลยแบบฝึกหัด + สรุปเนื้อหา + เทคนิคการนำไปใช้จริง |

---

## 📑 สารบัญ

| | หัวข้อ |
|---|---|
| | [วิธีใช้เอกสารนี้](#วิธีใช้เอกสารนี้) |
| **Week 1** | [สรุปเนื้อหา + เฉลย — Event-Driven with S3 + Lambda](#-week-1--event-driven-with-s3--lambda) |
| | [สรุปหัวข้อการเรียน Week 1](#-สรุปหัวข้อการเรียน-week-1) |
| | [เฉลยคำถามท้าย LAB Week 1](#-เฉลยคำถามท้าย-lab-week-1) |
| | [เฉลยแบบฝึกหัดเพิ่มเติม Week 1](#-เฉลยแบบฝึกหัดเพิ่มเติม-week-1) |
| | [เทคนิคและทริคสำหรับชีวิตจริง Week 1](#-เทคนิคและทริคสำหรับชีวิตจริง-week-1) |
| **Week 2** | [สรุปเนื้อหา + เฉลย — Message Queue with SQS](#-week-2--message-queue-with-sqs) |
| | [สรุปหัวข้อการเรียน Week 2](#-สรุปหัวข้อการเรียน-week-2) |
| | [เฉลยคำถามท้าย LAB Week 2](#-เฉลยคำถามท้าย-lab-week-2) |
| | [เฉลยแบบฝึกหัดเพิ่มเติม Week 2](#-เฉลยแบบฝึกหัดเพิ่มเติม-week-2) |
| | [เทคนิคและทริคสำหรับชีวิตจริง Week 2](#-เทคนิคและทริคสำหรับชีวิตจริง-week-2) |
| **Week 3** | [สรุปเนื้อหา + เฉลย — Orchestration with Step Functions](#-week-3--orchestration-with-step-functions) |
| | [สรุปหัวข้อการเรียน Week 3](#-สรุปหัวข้อการเรียน-week-3) |
| | [เฉลยคำถามท้าย LAB Week 3](#-เฉลยคำถามท้าย-lab-week-3) |
| | [เฉลยแบบฝึกหัดเพิ่มเติม Week 3](#-เฉลยแบบฝึกหัดเพิ่มเติม-week-3) |
| | [เทคนิคและทริคสำหรับชีวิตจริง Week 3](#-เทคนิคและทริคสำหรับชีวิตจริง-week-3) |
| **Week 4** | [สรุปเนื้อหา + เฉลย — Notification & Monitoring](#-week-4--notification--monitoring) |
| | [สรุปหัวข้อการเรียน Week 4](#-สรุปหัวข้อการเรียน-week-4) |
| | [เฉลยคำถามท้าย LAB Week 4](#-เฉลยคำถามท้าย-lab-week-4) |
| | [เฉลยแบบฝึกหัดเพิ่มเติม Week 4](#-เฉลยแบบฝึกหัดเพิ่มเติม-week-4) |
| | [เทคนิคและทริคสำหรับชีวิตจริง Week 4](#-เทคนิคและทริคสำหรับชีวิตจริง-week-4) |
| **สรุปรวม** | [Mindmap ความรู้ทั้ง 4 สัปดาห์](#-mindmap-ความรู้ทั้ง-4-สัปดาห์) |
| | [Design Patterns เปรียบเทียบ](#-design-patterns-เปรียบเทียบ) |
| | [Checklist ก่อนไป Production](#-production-readiness-checklist) |

---

## วิธีใช้เอกสารนี้

> 💡 **แนะนำให้ทำ Lab เองก่อนเสมอ** แล้วค่อยมาเทียบกับเฉลย การลองผิดลองถูกเองสร้างความเข้าใจที่ลึกกว่ามาก
>
> เอกสารนี้แบ่งออกเป็น 3 ส่วนสำหรับแต่ละ Week:
> 1. **สรุปเนื้อหา** — ทบทวน Concepts หลักที่เรียนมา
> 2. **เฉลยคำถาม** — อธิบายเหตุผลเชิงลึก ไม่ใช่แค่ตอบว่าถูกหรือผิด
> 3. **เทคนิคชีวิตจริง** — สิ่งที่ Engineer ใน Production ทำจริงๆ

---

---

# 📅 WEEK 1 — Event-Driven with S3 + Lambda

---

## 📖 สรุปหัวข้อการเรียน Week 1

### แนวคิดหลักที่ต้องจำ

**1. Event-Driven Architecture**

ระบบ Event-Driven ทำงานโดย "ตอบสนองต่อเหตุการณ์" แทนการ "ถามซ้ำๆ" (Polling) ประโยชน์หลักคือ:

| Polling | Event-Driven |
|---------|-------------|
| ใช้ Resource ตลอดเวลา | ใช้ Resource เฉพาะเมื่อมีงาน |
| Latency ขึ้นกับ Interval | Latency ต่ำ (ตอบสนองทันที) |
| จ่ายเงินแม้ไม่มีงาน | จ่ายเฉพาะเมื่อมี Event |
| Tight Coupling | Loose Coupling |

**2. S3 Events — ประเภทที่ควรรู้**

```
s3:ObjectCreated:Put        — อัปโหลดปกติ
s3:ObjectCreated:Post       — อัปโหลดผ่าน Form
s3:ObjectCreated:Copy       — Copy Object
s3:ObjectCreated:*          — รวมทุกแบบ (ใช้บ่อยที่สุด)
s3:ObjectRemoved:Delete     — ลบไฟล์
s3:ObjectRemoved:*          — รวมทุกแบบการลบ
```

**3. IAM Least Privilege — หลักการสำคัญ**

```
❌ ห้ามใช้: "Resource": "*"
✅ ถูกต้อง:  "Resource": "arn:aws:s3:::bucket-name/specific-prefix/*"

❌ ห้ามใช้: "Action": "s3:*"
✅ ถูกต้อง:  "Action": ["s3:GetObject", "s3:PutObject"]
```

**4. Structured Logging ทำไมถึงสำคัญ**

```python
# ❌ Log แบบธรรมดา — ค้นหายาก
print(f"Processing file: {filename}")

# ✅ Structured Log แบบ JSON — ค้นหาง่าย, Filter ได้, Alert ได้
logger.info(json.dumps({
    "event": "file_received",
    "file": filename,
    "size_bytes": size,
    "timestamp": datetime.now().isoformat()
}))
```

**5. Flow ที่สร้างใน Week 1**

```
[User Upload CSV] 
    → [S3: pipeline-raw/uploads/] 
    → S3 ObjectCreated Event 
    → [Lambda: csv-validator]
        → ตรวจสอบนามสกุล (.csv ?)
        → ตรวจสอบว่าไม่ว่างเปล่า
        → Log ผลลัพธ์ใน CloudWatch
```

---

## ❓ เฉลยคำถามท้าย LAB Week 1

---

### คำถามที่ 1
**"ทำไม S3 Event Trigger ถึงไม่รับประกันว่าจะ Trigger ครั้งเดียวเสมอ? แล้วจะออกแบบ Lambda ให้รองรับ Duplicate Events ได้ยังไง? (Idempotency)"**

**เฉลย:**

S3 Event Trigger ใช้ระบบ Distributed ที่ออกแบบมาเพื่อ **"At-Least-Once Delivery"** หมายความว่าระบบรับประกันว่า Event จะถูกส่งอย่างน้อย 1 ครั้ง แต่ไม่รับประกันว่าจะส่งแค่ครั้งเดียว ในกรณีที่มีปัญหาด้าน Network หรือ Retry อาจเกิด Duplicate ได้

**วิธีออกแบบ Idempotent Lambda:**

```python
import hashlib

def lambda_handler(event, context):
    for record in event['Records']:
        bucket = record['s3']['bucket']['name']
        key    = record['s3']['object']['key']
        
        # ✅ วิธีที่ 1: ใช้ S3 Key เป็น Idempotency Key
        # ถ้าประมวลผลแล้ว output_key จะมีอยู่แล้ว ก็ Skip
        output_key = f"processed/{key.replace('uploads/', '')}.json"
        
        try:
            s3.head_object(Bucket=DEST_BUCKET, Key=output_key)
            logger.info(f"Already processed: {key}, skipping.")
            continue  # ข้ามถ้าทำไปแล้ว
        except s3.exceptions.ClientError:
            pass  # ยังไม่มี → ประมวลผลต่อ
        
        # ✅ วิธีที่ 2: Hash เนื้อหาไฟล์
        # สร้าง Hash จากเนื้อหา → ถ้า Hash เดิมเคย Process แล้ว → Skip
        content = s3.get_object(Bucket=bucket, Key=key)['Body'].read()
        file_hash = hashlib.md5(content).hexdigest()
        
        # เก็บ Hash ที่เคยทำแล้วใน DynamoDB หรือ S3 metadata
        # ถ้าพบ Hash เดิม → Skip
```

> 💡 **กฎสำคัญ:** Lambda ที่รับ Event จาก S3, SQS, SNS ควรออกแบบให้เป็น **Idempotent** เสมอ คือ "รันกี่ครั้งก็ให้ผลลัพธ์เดิม" วิธีที่ง่ายที่สุดคือตรวจสอบว่า Output มีอยู่แล้วหรือยังก่อน Process

---

### คำถามที่ 2
**"Lambda มี Concurrency Limit เท่าไหร่ใน Default? ถ้า Upload ไฟล์พร้อมกัน 1,000 ไฟล์จะเกิดอะไรขึ้น?"**

**เฉลย:**

| ค่า | รายละเอียด |
|-----|-----------|
| **Default Concurrency** | 1,000 Concurrent Executions ต่อ Account ต่อ Region |
| **Reserved Concurrency** | สามารถ "จอง" จำนวนสำหรับ Function เฉพาะได้ |
| **Provisioned Concurrency** | Pre-warm ไว้เลย ไม่มี Cold Start (เสียเงินเพิ่ม) |

**ถ้า Upload 1,000 ไฟล์พร้อมกัน:**

```
ไฟล์ที่ 1–1,000   → Lambda เปิด 1,000 Instance พร้อมกัน (ถึง Limit)
ไฟล์ที่ 1,001+    → ได้รับ Throttling Error (429 Too Many Requests)
                   → S3 จะ Retry อัตโนมัติ แต่ถ้า Retry ก็ยัง Full อยู่
                   → Event อาจหาย! (S3 Retry ไม่เกิน 3 ครั้ง)
```

**วิธีแก้:**

```
วิธีที่ 1: ใช้ SQS เป็น Buffer (เรียนใน Week 2)
  → S3 → Lambda Validator → SQS Queue → Consumer Lambda
  → Queue จะเก็บ Message ไว้รอ ไม่มีการสูญหาย

วิธีที่ 2: ตั้ง Reserved Concurrency บน Lambda
  → จำกัด Concurrency = ควบคุม Rate ที่ประมวลผล
  → แต่ถ้าเกิน Limit จะ Throttle ไม่ใช่ Drop Event

วิธีที่ 3: เพิ่ม Concurrency Limit ของ Account
  → ติดต่อ AWS Support เพื่อขอเพิ่มจาก Default 1,000
```

> 💡 **สิ่งสำคัญ:** S3 Event ที่ถูก Throttle อาจไม่ถูก Retry ทุกครั้ง ดังนั้น **SQS เป็น Buffer ที่ดีที่สุด** สำหรับการรับ Event ปริมาณมาก เพราะ SQS เก็บ Message ได้นานหลายวันและ Retry อัตโนมัติ

---

### คำถามที่ 3
**"Prefix `uploads/` ใน S3 Trigger ป้องกัน Recursive Loop ได้จริงหรือเปล่า? มีกรณีที่ยังเกิด Loop ได้ไหม?"**

**เฉลย:**

Prefix ป้องกันได้ **เฉพาะในกรณีที่ Lambda เขียนไปยัง Folder อื่น** แต่ยังมีกรณีที่ Loop เกิดได้:

| กรณี | เกิด Loop หรือเปล่า |
|------|-------------------|
| Lambda อ่านจาก `uploads/` เขียนไปยัง Bucket อื่น | ❌ ไม่เกิด (ปลอดภัย) |
| Lambda อ่านจาก `uploads/` เขียนไปยัง `processed/` ใน Bucket เดิม + Trigger ตั้งเฉพาะ `uploads/` | ❌ ไม่เกิด (ปลอดภัย) |
| Lambda อ่านจาก `uploads/` แล้วเขียนกลับไปที่ `uploads/` ใน Bucket เดิม | ✅ **เกิด Loop ทันที!** |
| มี 2 Trigger ที่ `uploaded/` และ `processed/` และ Lambda A เขียนไป `processed/` แล้ว Lambda B เขียนกลับไป `uploaded/` | ✅ **เกิด Indirect Loop!** |

**Best Practice:**

```
✅ วิธีที่ปลอดภัยที่สุดคือใช้ 2 Bucket แยกกัน
   Input Bucket  → ห้าม Lambda ของเรา Write กลับเด็ดขาด
   Output Bucket → Lambda Write ได้ แต่ไม่มี Event Trigger

✅ ถ้าต้องใช้ Bucket เดียว ให้ใช้ Prefix ที่ต่างกันอย่างเคร่งครัด
   และตรวจสอบว่า Lambda ไม่มีทางเขียนกลับไปยัง Prefix ที่ Trigger อยู่เลย
```

> ⚠️ **Warning ใน AWS Console:** เมื่อตั้ง S3 Trigger AWS จะแสดง Recursive Warning เสมอ อ่านให้ดีและกด Acknowledge อย่างมีสติ

---

## 🔧 เฉลยแบบฝึกหัดเพิ่มเติม Week 1

---

### แบบฝึกหัดที่ 1
**"แก้ไข Lambda ให้ตรวจสอบว่าไฟล์มี Column `order_id` อยู่หรือเปล่า ถ้าไม่มีให้ Reject"**

**เฉลย — โค้ดที่ถูกต้อง:**

```python
import json, boto3, csv, io, logging
from datetime import datetime

logger = logging.getLogger()
logger.setLevel(logging.INFO)
s3 = boto3.client('s3')

# ✅ เทคนิค: กำหนด Required Columns เป็น Constant ข้างนอก Lambda Handler
# → ง่ายต่อการแก้ไขในอนาคต ไม่ต้องไปหาในโค้ด
REQUIRED_COLUMNS = {'order_id', 'customer_name', 'product', 'quantity', 'price', 'date'}

def lambda_handler(event, context):
    for record in event['Records']:
        bucket_name = record['s3']['bucket']['name']
        object_key  = record['s3']['object']['key']
        file_size   = record['s3']['object']['size']

        if not object_key.lower().endswith('.csv'):
            logger.warning(json.dumps({"event": "rejected", "file": object_key, "reason": "not_csv"}))
            continue

        try:
            response   = s3.get_object(Bucket=bucket_name, Key=object_key)
            content    = response['Body'].read().decode('utf-8')
            csv_reader = csv.DictReader(io.StringIO(content))
            rows       = list(csv_reader)
            headers    = set(csv_reader.fieldnames or [])

            if not rows:
                logger.warning(json.dumps({"event": "rejected", "file": object_key, "reason": "empty_file"}))
                continue

            # ✅ ตรวจสอบ Column ที่ขาด
            missing = REQUIRED_COLUMNS - headers
            if missing:
                logger.warning(json.dumps({
                    "event": "rejected",
                    "file": object_key,
                    "reason": "missing_required_columns",
                    "missing_columns": list(missing),  # แปลง set เป็น list เพื่อ JSON Serialize ได้
                    "found_columns": list(headers)
                }))
                continue  # หรือ copy ไป failed/ folder

            # ✅ ผ่านทุกการตรวจสอบ
            logger.info(json.dumps({
                "event": "file_validated",
                "file": object_key,
                "status": "valid",
                "total_rows": len(rows),
                "headers": list(headers),
                "file_size_bytes": file_size,
                "processed_at": datetime.utcnow().isoformat() + "Z"
            }))

        except Exception as e:
            logger.error(json.dumps({"event": "error", "file": object_key, "error": str(e)}))
            raise  # ✅ Re-raise เพื่อให้ Lambda Return Error → S3 Retry

    return {"statusCode": 200}
```

> 💡 **เทคนิค:** ใช้ `set` แทน `list` สำหรับการตรวจสอบ Column เพราะ `column in set` เร็วกว่า `column in list` มาก (O(1) vs O(n)) โดยเฉพาะเมื่อมี Column จำนวนมาก

---

### แบบฝึกหัดที่ 2
**"เพิ่ม Metric: ใช้ boto3 ส่ง Custom Metric ไป CloudWatch เพื่อนับจำนวนไฟล์ที่ Valid/Invalid ต่อวัน"**

**เฉลย:**

```python
import boto3

cloudwatch = boto3.client('cloudwatch', region_name='ap-southeast-1')

def send_metric(metric_name, value, unit='Count', dimensions=None):
    """
    ส่ง Custom Metric ไป CloudWatch
    ✅ เทคนิค: Wrap ใน Function แยก เพื่อใช้ซ้ำและ Test ง่าย
    """
    metric_data = {
        'MetricName': metric_name,
        'Value': value,
        'Unit': unit,
        'Dimensions': dimensions or [
            {'Name': 'Pipeline', 'Value': 'CSVProcessor'},
            {'Name': 'Environment', 'Value': 'production'}
        ]
    }
    
    try:
        cloudwatch.put_metric_data(
            Namespace='DataPipeline/FileProcessing',  # ✅ Namespace ควรสื่อความหมาย
            MetricData=[metric_data]
        )
    except Exception as e:
        # ✅ ไม่ Raise Error เพื่อไม่ให้ Metric Failure หยุด Main Flow
        logger.warning(f"Failed to send metric {metric_name}: {e}")

# ใช้งานใน Lambda Handler:
def lambda_handler(event, context):
    valid_count   = 0
    invalid_count = 0
    
    for record in event['Records']:
        # ... ประมวลผล ...
        if result == 'valid':
            valid_count += 1
        else:
            invalid_count += 1
    
    # ส่ง Metrics หลังประมวลผลทั้ง Batch เสร็จ
    # ✅ เทคนิค: ส่งเป็น Batch ดีกว่าส่งทีละ Record (ประหยัด API Call)
    send_metric('FilesValidated', valid_count)
    send_metric('FilesRejected', invalid_count)
    
    return {"statusCode": 200}
```

> 💡 **เทคนิค:** กำหนด `Namespace` ให้ชัดเจนและ Consistent เช่น `CompanyName/ServiceName/SubService` จะทำให้หา Metric ใน CloudWatch Dashboard ได้ง่าย ใน Production จริงๆ มักใช้ `Namespace` เดียวกันทั้ง Team

---

### แบบฝึกหัดที่ 3
**"ทดลอง Upload ไฟล์ CSV ขนาดใหญ่ (1,000 rows) แล้วดูว่า Duration เพิ่มขึ้นเท่าไหร่"**

**เฉลย — Script สร้างไฟล์ CSV ขนาด 1,000 rows:**

```python
# สร้างไฟล์นี้ในเครื่อง แล้วรัน: python generate_large_csv.py
import csv, random
from datetime import datetime, timedelta

def generate_large_csv(filename='large_sales.csv', rows=1000):
    products  = ['Widget A', 'Widget B', 'Widget C', 'Gadget X', 'Gadget Y']
    customers = ['สมชาย', 'สมหญิง', 'วิชัย', 'นิดา', 'ประสิทธิ์']
    
    with open(filename, 'w', newline='', encoding='utf-8') as f:
        writer = csv.writer(f)
        writer.writerow(['order_id', 'customer_name', 'product', 'quantity', 'price', 'date'])
        
        for i in range(1, rows + 1):
            date = datetime(2024, 1, 1) + timedelta(days=random.randint(0, 90))
            writer.writerow([
                f'ORD{i:05d}',
                random.choice(customers),
                random.choice(products),
                random.randint(1, 20),
                round(random.uniform(100, 2000), 2),
                date.strftime('%Y-%m-%d')
            ])
    
    print(f"Created {filename} with {rows} rows")

generate_large_csv()
```

**ผลลัพธ์ที่คาดว่าจะเห็นจาก CloudWatch Metrics:**

| ขนาดไฟล์ | Duration โดยประมาณ | Memory ใช้ |
|---------|------------------|-----------|
| 5 rows (312 bytes) | ~50–100ms | ~50 MB |
| 1,000 rows (~60 KB) | ~200–400ms | ~80 MB |
| 10,000 rows (~600 KB) | ~1,000–2,000ms | ~120 MB |

> 💡 **เทคนิค:** ถ้า Duration เพิ่มแบบ Linear ตามจำนวน Row แสดงว่าโค้ดทำงาน O(n) ซึ่งปกติ แต่ถ้า Duration เพิ่มแบบ Quadratic (n²) แสดงว่ามี Nested Loop ที่ไม่จำเป็น ควรแก้ไข

---

## 🚀 เทคนิคและทริคสำหรับชีวิตจริง Week 1

### 🎯 Tip 1: เสมอทดสอบ Lambda โดยตรงก่อน Trigger จาก S3

ในชีวิตจริง Engineer จะทดสอบ Lambda ด้วย Mock Event ก่อนเสมอ เพราะ Debug ง่ายกว่าต้องอัปโหลดไฟล์ทุกครั้ง:

```bash
# ✅ สร้าง Mock Event จาก S3 Event ที่ถูกจริง
# เข้า S3 → เลือก Object → กด "Copy S3 URI" แล้วนำมาสร้าง Test Event
{
  "Records": [{
    "s3": {
      "bucket": {"name": "YOUR-BUCKET"},
      "object": {"key": "uploads/test.csv", "size": 1024}
    }
  }]
}
```

### 🎯 Tip 2: ใช้ Environment Variables แทน Hard-code

```python
# ❌ อย่าทำแบบนี้
BUCKET_NAME = "pipeline-processed-john-1234"

# ✅ ทำแบบนี้
import os
BUCKET_NAME = os.environ.get('PROCESSED_BUCKET_NAME')
# ตั้งใน Lambda → Configuration → Environment variables
```

**ทำไมถึงสำคัญ:** ถ้า Bucket ชื่อเปลี่ยน ต้องแก้โค้ดและ Deploy ใหม่ แต่ถ้าใช้ Environment Variable แก้แค่ Config เดียว ไม่ต้อง Deploy ใหม่เลย

### 🎯 Tip 3: Log ทุก Exception พร้อม Stack Trace

```python
import traceback

try:
    # โค้ดที่อาจ Error
    process_file(bucket, key)
except Exception as e:
    logger.error(json.dumps({
        "event": "unhandled_error",
        "error": str(e),
        "error_type": type(e).__name__,
        "traceback": traceback.format_exc(),  # ✅ Full Stack Trace
        "file": key
    }))
    raise  # ✅ Re-raise เสมอ เพื่อให้ Lambda Report Error ถูกต้อง
```

### 🎯 Tip 4: Cold Start ทำให้ช้า — วางโค้ด Init นอก Handler

```python
# ✅ วางตรงนี้ — รันครั้งเดียวตอน Cold Start
import boto3
s3  = boto3.client('s3')        # Connection Pool
sqs = boto3.client('sqs')       # Reused ทุก Warm Invocation

# ❌ ห้ามวางตรงนี้ (ใน Handler) — สร้างใหม่ทุก Invocation
def lambda_handler(event, context):
    s3  = boto3.client('s3')   # ช้า และสิ้นเปลือง
    sqs = boto3.client('sqs')  # ช้า และสิ้นเปลือง
```

---

---

# 📅 WEEK 2 — Message Queue with SQS

---

## 📖 สรุปหัวข้อการเรียน Week 2

### แนวคิดหลักที่ต้องจำ

**1. ทำไมต้องมี Queue — ปัญหาที่แก้ได้**

| ปัญหา | ไม่มี Queue | มี SQS Queue |
|-------|------------|-------------|
| Upload 500 ไฟล์พร้อมกัน | Lambda 500 ตัว Throttle | Queue รับทั้งหมด Consumer ค่อยๆ อ่าน |
| Consumer Service Down | Message หาย | Message รออยู่ใน Queue นาน 4 วัน |
| ประมวลผลล้มเหลว | ข้อมูลหาย | Retry อัตโนมัติ → DLQ |
| Rate Limit ของ Service ถัดไป | Overflow | Queue เป็น Buffer ควบคุม Rate |

**2. SQS Standard vs FIFO**

```
Standard Queue:
  ✅ Throughput ไม่จำกัด
  ✅ ราคาถูกกว่า
  ⚠️  At-Least-Once Delivery (อาจ Duplicate)
  ⚠️  Best-Effort Ordering (ลำดับไม่รับประกัน)
  → ใช้เมื่อ: ลำดับไม่สำคัญ และออกแบบ Idempotent ได้

FIFO Queue:
  ✅ Exactly-Once Delivery (ไม่ Duplicate)
  ✅ First-In-First-Out (ลำดับรับประกัน)
  ⚠️  Throughput จำกัด 300–3,000 msg/sec
  ⚠️  ราคาแพงกว่าเล็กน้อย
  → ใช้เมื่อ: ลำดับสำคัญ เช่น Financial Transactions
```

**3. Dead Letter Queue (DLQ) — Safety Net**

```
Message → Main Queue → Consumer Lambda
                              ↓ (ล้มเหลว)
                         Retry 1 ครั้ง (หลัง Visibility Timeout)
                              ↓ (ล้มเหลว)
                         Retry 2 ครั้ง
                              ↓ (ล้มเหลว)
                         Retry 3 ครั้ง (maxReceiveCount = 3)
                              ↓ (ยังล้มเหลว)
                        → DLQ (เก็บไว้ 14 วัน สำหรับ Debug)
                        → CloudWatch Alarm แจ้งเตือน
```

**4. Visibility Timeout — กฎสำคัญ**

```
Visibility Timeout ของ Queue > Lambda Timeout เสมอ

ตัวอย่าง:
  Lambda Timeout = 60 seconds
  Visibility Timeout = 90 seconds  ✅ (มีเวลาเผื่อ)

ถ้าตั้งผิด:
  Lambda Timeout = 60 seconds
  Visibility Timeout = 30 seconds  ❌
  → Lambda ยังประมวลผลไม่เสร็จ แต่ Message กลับมา Visible แล้ว
  → Consumer อื่นหรือ Lambda ตัวเดิมรับ Message ซ้ำ!
```

**5. Batch Item Failures — Pattern ที่ดีที่สุด**

```python
# ✅ Return เฉพาะ Message ที่ล้มเหลว
return {
    "batchItemFailures": [
        {"itemIdentifier": "message-id-456"}  # ล้มเหลวแค่ตัวนี้
    ]
}
# ผลลัพธ์: SQS Retry เฉพาะ message-id-456 ไม่ต้อง Retry ทั้ง Batch
```

---

## ❓ เฉลยคำถามท้าย LAB Week 2

---

### คำถามที่ 1
**"ถ้าตั้ง Visibility Timeout สั้นกว่า Lambda Timeout จะเกิดอะไรขึ้น?"**

**เฉลย:**

เกิด **Double Processing** หรือที่เรียกว่า "Phantom Retry":

```
Timeline:
T=0s   : Lambda A รับ Message (Visibility Timeout = 30s เริ่มนับ)
T=0s   : Lambda A เริ่มประมวลผล (Timeout = 60s)
T=30s  : Visibility Timeout หมด → Message กลับมา Visible ใน Queue
T=30s  : Lambda B รับ Message เดิม! (Double Processing เริ่มต้น)
T=60s  : Lambda A ประมวลผลเสร็จ เขียนผลลัพธ์ลง S3
T=90s  : Lambda B ประมวลผลเสร็จ เขียนผลลัพธ์ลง S3 (เขียนทับ!)
```

**ผลกระทบ:**
- **ข้อมูลถูกเขียนทับ** โดย Lambda ที่รันช้ากว่า
- **ค่าใช้จ่ายเพิ่มขึ้น** เพราะประมวลผลไฟล์เดิมสองครั้ง
- **DLQ อาจผิดปกติ** เพราะ maxReceiveCount นับ Receive ซ้ำด้วย

**กฎ:**
```
Visibility Timeout = Lambda Timeout × 6
(AWS แนะนำให้มีเผื่อ buffer 6x เพื่อรองรับกรณี Lambda Retry)
```

---

### คำถามที่ 2
**"SQS Standard Queue อาจ Deliver Message มากกว่า 1 ครั้ง — เราออกแบบ `csv-processor` ให้รองรับกรณีนี้ได้ยังไง?"**

**เฉลย:**

ใน Lab โค้ดออกแบบ Idempotent ผ่าน `output_key`:

```python
# ✅ ใน transform-data Lambda:
output_key = f"processed/{datetime.now().strftime('%Y/%m/%d')}/{filename}_result.json"
# output_key เดิม → s3.put_object จะเขียนทับ → ผลลัพธ์เหมือนเดิม ✅
```

**แต่มีปัญหาคือ:** ถ้า Message เดิมถูก Deliver สองครั้งในวันต่างกัน `output_key` จะต่างกัน!

**วิธีที่ดีกว่า — ใช้ Job ID เป็น Key:**

```python
# ✅ วิธีที่ดีกว่า: ใช้ job_id ที่คงที่
filename  = source_key.split('/')[-1].replace('.csv', '')
output_key = f"processed/{filename}-{job_id}_result.json"
# job_id เดิม → output_key เดิม → เขียนทับผลลัพธ์เดิม → Idempotent ✅

# หรือตรวจสอบก่อน Process:
try:
    s3.head_object(Bucket=dest_bucket, Key=output_key)
    logger.info(f"Already processed job {job_id}, skipping.")
    return  # Skip โดยไม่ Error
except s3.exceptions.ClientError:
    pass  # ยังไม่มี → Process ต่อ
```

---

### คำถามที่ 3
**"Long Polling กับ Short Polling ต่างกันยังไงในแง่ Cost และ Latency?"**

**เฉลย:**

| | Short Polling | Long Polling |
|--|--------------|-------------|
| **ทำงานยังไง** | ถาม SQS ทันที → ตอบกลับทันที (อาจว่างเปล่า) | ถาม SQS → รอนานสูงสุด 20 วินาทีถ้าไม่มี Message |
| **Cost** | สูงกว่า — ทุก API Call คิดเงิน แม้ได้ Response ว่างเปล่า | ต่ำกว่า — API Call น้อยกว่าเพราะรอ Message แบบ Batch |
| **Latency** | ต่ำมาก (ตอบทันที) | อาจมี Delay สูงสุด 20 วินาที แต่ส่วนใหญ่น้อยกว่า |
| **ตั้งค่า** | `ReceiveMessageWaitTimeSeconds = 0` | `ReceiveMessageWaitTimeSeconds = 1–20` |

**ตัวอย่างการประหยัด Cost:**

```
สมมติ Consumer Poll ทุก 1 วินาที:

Short Polling:
  1 วัน = 86,400 API Calls
  1 เดือน = 2,592,000 Calls
  (เกิน Free Tier 1M → เสียเงิน)

Long Polling (wait 20s):
  1 วัน = 4,320 API Calls
  1 เดือน = 129,600 Calls
  (อยู่ใน Free Tier ✅ ประหยัดได้ ~95%)
```

> 💡 **คำแนะนำ:** ตั้ง Long Polling ไว้เสมอ (`WaitTimeSeconds=20`) ยกเว้นกรณีที่ต้องการ Latency ต่ำมากๆ เช่น Real-time System ที่ทุก millisecond สำคัญ

---

## 🔧 เฉลยแบบฝึกหัดเพิ่มเติม Week 2

---

### แบบฝึกหัดที่ 1
**"เพิ่ม CloudWatch Alarm แจ้งเตือนเมื่อ `pipeline-dlq` มี Message มากกว่า 0"**

**เฉลย — ขั้นตอนใน AWS Console:**

1. เข้า **CloudWatch** → **Alarms** → **Create alarm**
2. **Select metric** → **SQS** → **Queue Metrics** → ค้นหา `pipeline-dlq`
3. เลือก `ApproximateNumberOfMessagesVisible`
4. กำหนดค่า:

```
Statistic:         Maximum
Period:            1 minute
Threshold type:    Static
Condition:         Greater than
Threshold value:   0     ← แจ้งทันทีที่มี Message แม้แค่ตัวเดียว

Treat missing data as: Good (not breaching)
```

5. Notification: เลือก SNS Topic (สร้างใน Week 4 หรือสร้างใหม่ชั่วคราว)
6. Alarm name: `pipeline-dlq-messages-alarm`

**เฉลย — ผ่าน AWS CLI (สำหรับทดลอง):**

```bash
aws cloudwatch put-metric-alarm \
  --alarm-name "pipeline-dlq-messages-alarm" \
  --alarm-description "Alert when DLQ has messages" \
  --metric-name "ApproximateNumberOfMessagesVisible" \
  --namespace "AWS/SQS" \
  --dimensions Name=QueueName,Value=pipeline-dlq \
  --statistic Maximum \
  --period 60 \
  --threshold 0 \
  --comparison-operator GreaterThanThreshold \
  --evaluation-periods 1 \
  --treat-missing-data notBreaching
```

> 💡 **เทคนิค:** ตั้ง DLQ Alarm ให้ Trigger ที่ `> 0` เสมอ (ไม่ใช่ `> 5` หรือ `> 10`) เพราะทุก Message ใน DLQ คือ "งานที่ยังไม่เสร็จ" ที่ต้องรีบแก้ไข ใน Production จริง DLQ ควรว่างเปล่าเสมอ

---

### แบบฝึกหัดที่ 2
**"ทดสอบ High Volume: เขียน Script อัปโหลด CSV 20 ไฟล์พร้อมกัน"**

**เฉลย:**

```python
# upload_bulk.py — รันในเครื่อง
import boto3, csv, io, threading, time, random, string
from datetime import datetime, timedelta

s3          = boto3.client('s3', region_name='ap-southeast-1')
BUCKET_NAME = 'pipeline-raw-[ชื่อคุณ]-[random]'
NUM_FILES   = 20

def generate_csv_content(rows=10):
    """สร้างเนื้อหา CSV แบบสุ่ม"""
    output   = io.StringIO()
    writer   = csv.writer(output)
    products = ['Widget A', 'Widget B', 'Widget C']
    writer.writerow(['order_id', 'customer_name', 'product', 'quantity', 'price', 'date'])
    for i in range(rows):
        date = datetime(2024, 1, 1) + timedelta(days=random.randint(0, 90))
        writer.writerow([f'ORD{i:04d}', f'Customer{i}', random.choice(products),
                         random.randint(1, 10), round(random.uniform(100, 1000), 2),
                         date.strftime('%Y-%m-%d')])
    return output.getvalue()

def upload_file(file_index):
    """Upload ไฟล์เดียว — ใช้ใน Thread"""
    rand_suffix = ''.join(random.choices(string.ascii_lowercase, k=4))
    filename    = f"test_batch_{file_index:03d}_{rand_suffix}.csv"
    key         = f"uploads/{filename}"
    content     = generate_csv_content(random.randint(5, 50))
    
    s3.put_object(Bucket=BUCKET_NAME, Key=key,
                  Body=content.encode('utf-8'), ContentType='text/csv')
    print(f"[{datetime.now().strftime('%H:%M:%S')}] Uploaded: {filename}")

# ✅ ใช้ Threading เพื่ออัปโหลดพร้อมกัน
print(f"Uploading {NUM_FILES} files simultaneously...")
start     = time.time()
threads   = [threading.Thread(target=upload_file, args=(i,)) for i in range(NUM_FILES)]
[t.start() for t in threads]
[t.join()  for t in threads]  # รอทุก Thread เสร็จ

print(f"Done! Uploaded {NUM_FILES} files in {time.time()-start:.2f}s")
print("Now check SQS Console → pipeline-main-queue for messages...")
```

---

### แบบฝึกหัดที่ 3
**"เพิ่ม Message Deduplication ID: แก้โค้ดให้ไม่ประมวลผลไฟล์เดิมซ้ำ"**

**เฉลย:**

```python
import hashlib

def lambda_handler(event, context):  # ใน csv-validator
    for record in event['Records']:
        object_key = record['s3']['object']['key']
        file_size  = record['s3']['object']['size']
        
        # ✅ สร้าง Deduplication ID จาก Key + Size + ETag (ถ้ามี)
        # ETag = MD5 Hash ของไฟล์ (AWS คำนวณให้)
        etag = record['s3']['object'].get('eTag', '')
        dedup_id = hashlib.md5(f"{object_key}:{file_size}:{etag}".encode()).hexdigest()
        
        message = {
            "job_id": f"job-{dedup_id[:12]}",  # ✅ ใช้ Hash ส่วนหนึ่งเป็น Job ID
            "source_bucket": bucket_name,
            "source_key": object_key,
            "deduplication_id": dedup_id,       # ✅ เก็บไว้สำหรับ Debug
            # ...
        }
        
        # ✅ สำหรับ FIFO Queue ใช้ MessageDeduplicationId โดยตรง
        # สำหรับ Standard Queue ต้องตรวจสอบใน Consumer เอง
        sqs.send_message(
            QueueUrl=QUEUE_URL,
            MessageBody=json.dumps(message),
            # MessageDeduplicationId=dedup_id,  # ใช้กับ FIFO Queue เท่านั้น
        )
```

---

## 🚀 เทคนิคและทริคสำหรับชีวิตจริง Week 2

### 🎯 Tip 1: ตั้งค่า Queue ให้ถูกต้องตั้งแต่แรก

```
Rule ของ Visibility Timeout:
  Queue Visibility Timeout ≥ Lambda Timeout × 6
  ถ้า Lambda Timeout = 60s → Queue Visibility = 360s ขึ้นไป

Rule ของ Message Retention:
  DLQ Retention = 14 วัน (max) — เผื่อเวลา Debug เยอะๆ
  Main Queue Retention = 4–7 วัน ก็พอ

Rule ของ Batch Size:
  เริ่มจาก Batch Size = 1 ก่อนเสมอ แล้วค่อยเพิ่ม
  ดู Duration ของ Lambda ถ้ายังไม่ถึง Timeout → เพิ่ม Batch Size ได้
```

### 🎯 Tip 2: Monitor DLQ เป็นสัญญาณสุขภาพของระบบ

ใน Production จริงๆ DLQ คือ "ตัวบ่งชี้ระบบ" ที่สำคัญที่สุด:

```
DLQ ว่างเปล่า = ระบบทำงานปกติ ✅
DLQ มี Message = มีบางอย่างผิดพลาด ต้องตรวจสอบทันที ⚠️

ใน Production:
  1. ตั้ง Alarm ที่ DLQ > 0 → แจ้ง Engineer On-Call
  2. มี Runbook (คู่มือ) สำหรับจัดการ DLQ Message แต่ละประเภท
  3. ทุกสัปดาห์ Review DLQ Message เพื่อหา Pattern ของ Error
```

### 🎯 Tip 3: ใช้ Message Attributes สำหรับ Routing

```python
# ✅ ส่ง Metadata พร้อม Message โดยไม่ต้อง Parse Body
sqs.send_message(
    QueueUrl=QUEUE_URL,
    MessageBody=json.dumps(message),
    MessageAttributes={
        'file_type':   {'DataType': 'String', 'StringValue': 'csv'},
        'priority':    {'DataType': 'String', 'StringValue': 'high'},
        'source_team': {'DataType': 'String', 'StringValue': 'finance'},
        'row_count':   {'DataType': 'Number', 'StringValue': str(len(rows))}
    }
)

# Consumer สามารถ Filter หรือ Route ตาม Attribute ได้
# โดยไม่ต้อง Deserialize Body ก่อน
```

---

---

# 📅 WEEK 3 — Orchestration with Step Functions

---

## 📖 สรุปหัวข้อการเรียน Week 3

### แนวคิดหลักที่ต้องจำ

**1. Choreography vs Orchestration**

```
Choreography (Week 1-2):
  Lambda A ──Event──> Lambda B ──Event──> Lambda C
  
  ข้อดี: Loose Coupling สุดๆ
  ข้อเสีย: ไม่มีที่เดียวที่เห็น Flow ทั้งหมด, Debug ยาก

Orchestration (Step Functions):
  State Machine ──เรียก──> Lambda A
                ──เรียก──> Lambda B (ถ้า A สำเร็จ)
                ──เรียก──> Lambda C (ถ้า B สำเร็จ)
  
  ข้อดี: เห็น Flow ทั้งหมด, Debug ง่าย, Error Handling รวมศูนย์
  ข้อเสีย: State Machine เป็น Single Point of Control (แต่ AWS จัดการ HA ให้)
```

**2. State Types ที่ใช้ใน Lab**

| State | ใช้ทำอะไร | ตัวอย่างใน Lab |
|-------|-----------|--------------|
| `Task` | เรียก Lambda / AWS Service | ParseCSV, ValidateSchema, TransformData |
| `Choice` | แยกเส้นทางตามเงื่อนไข | ถ้า schema_valid = true → TransformData |
| `Succeed` | จบ Execution สำเร็จ | ProcessingComplete |
| `Fail` | จบ Execution แบบ Error | ValidationFailed, HandleError |
| `Parallel` | รันหลาย Branch พร้อมกัน | (แบบฝึกหัด) |
| `Wait` | รอเวลา | (แบบฝึกหัด) |
| `Map` | Iterate ข้อมูล | (แบบฝึกหัด) |

**3. Retry กับ Catch — ความแตกต่าง**

```json
{
  "Retry": [
    {
      "ErrorEquals": ["Lambda.ServiceException"],
      "IntervalSeconds": 2,
      "MaxAttempts": 3,
      "BackoffRate": 2
      // ลองใหม่อัตโนมัติก่อน
    }
  ],
  "Catch": [
    {
      "ErrorEquals": ["States.ALL"],
      "Next": "HandleError"
      // ถ้า Retry ครบแล้วยังล้มเหลว → ไปที่นี่
    }
  ]
}
```

**4. Flow ที่สร้างใน Week 3**

```
[SQS] → [csv-processor] → start_execution() → [Step Functions]
                                                    │
                                              [ParseCSV]
                                                    │
                                           [ValidateSchema]
                                                    │
                                            [CheckValidation]
                                           /                \
                                    schema_valid=true    schema_valid=false
                                           │                     │
                                    [TransformData]       [MoveToFailed]
                                           │                     │
                                   [ProcessingComplete]  [ValidationFailed]
```

---

## ❓ เฉลยคำถามท้าย LAB Week 3

---

### คำถามที่ 1
**"Standard Workflow กับ Express Workflow ใน Step Functions ต่างกันยังไง? เลือกใช้อะไรเมื่อไหร่?"**

**เฉลย:**

| | Standard Workflow | Express Workflow |
|--|------------------|-----------------|
| **Duration สูงสุด** | 1 ปี | 5 นาที |
| **Execution History** | เก็บนาน 90 วัน | เก็บสั้น (ต้องใช้ CloudWatch) |
| **Delivery** | Exactly-once | At-least-once |
| **ราคา** | $0.025 ต่อ 1,000 State Transitions | $1 ต่อ 1M Executions + Duration |
| **Free Tier** | 4,000 transitions/เดือน | ไม่มี Free Tier |
| **Suitable for** | Long-running Workflows, ต้องการ History | High-volume, Short-duration (<5 min) |

**เมื่อไหร่ใช้อะไร:**

```
Standard Workflow → ใช้เมื่อ:
  ✅ Pipeline ที่ต้องการ Audit Trail (บันทึกทุก Step)
  ✅ Human Approval Workflow (รออนุมัติ หลายชั่วโมง/วัน)
  ✅ Order Processing ที่ต้องการ Exactly-once
  ✅ ใน Lab นี้ ✅

Express Workflow → ใช้เมื่อ:
  ✅ Real-time Streaming Processing (Kinesis → Lambda)
  ✅ IoT Data Processing (ข้อมูลเข้าหลายพัน/วินาที)
  ✅ High-volume API Processing ที่แต่ละ Execution สั้น
  ✅ ราคาถูกกว่าสำหรับปริมาณมาก
```

---

### คำถามที่ 2
**"Retry ใน ASL ทำงานยังไง? `BackoffRate: 2` หมายความว่าอะไร?"**

**เฉลย:**

`BackoffRate` คือตัวคูณของ Interval ระหว่าง Retry แต่ละครั้ง (Exponential Backoff):

```
ตัวอย่าง: IntervalSeconds=2, MaxAttempts=3, BackoffRate=2

Attempt 1: ล้มเหลว → รอ 2 seconds → ลองใหม่
Attempt 2: ล้มเหลว → รอ 2×2 = 4 seconds → ลองใหม่  
Attempt 3: ล้มเหลว → รอ 4×2 = 8 seconds → ลองใหม่
หลัง Attempt 3: ยังล้มเหลว → ไปที่ Catch
```

**ทำไม Exponential Backoff ถึงสำคัญ:**

```
ปัญหา: ถ้า Service ถัดไปมีปัญหา (Overload, Down ชั่วคราว)
         และเรา Retry ทันทีซ้ำๆ → ทำให้ Service นั้น Overload หนักขึ้น

Exponential Backoff:
  รอนานขึ้นเรื่อยๆ → ให้ Service มีเวลา Recover
  → ระบบ Stabilize เองได้โดยไม่ต้อง Manual Intervention
```

**Jitter — เทคนิคขั้นสูง:**

```python
# ✅ ใน Production จริงๆ เพิ่ม Random Jitter
# ป้องกัน "Thundering Herd" (ทุก Lambda Retry พร้อมกัน)
import random, time

def retry_with_jitter(func, max_attempts=3, base_delay=2, backoff=2):
    for attempt in range(max_attempts):
        try:
            return func()
        except Exception as e:
            if attempt == max_attempts - 1:
                raise
            # Exponential Backoff + Random Jitter (0–1 วินาที)
            delay = base_delay * (backoff ** attempt) + random.uniform(0, 1)
            time.sleep(delay)
```

---

### คำถามที่ 3
**"ถ้า Execution หนึ่งใช้เวลานานมาก จะ Cancel ได้ยังไง? มี Side Effects อะไรบ้าง?"**

**เฉลย:**

**วิธี Cancel Execution:**

```python
# ผ่าน AWS Console:
# Step Functions → Executions → เลือก Execution → Stop execution → กำหนด Error + Cause

# ผ่าน boto3:
import boto3
sfn = boto3.client('stepfunctions')

sfn.stop_execution(
    executionArn='arn:aws:states:ap-southeast-1:...:execution:...',
    error='ManualCancellation',
    cause='Cancelled by operator due to extended runtime'
)
```

**Side Effects ที่ต้องระวัง:**

```
1. Lambda ที่กำลังรันอยู่ยังทำงานต่อไปจนเสร็จ
   → Step Functions หยุด แต่ Lambda ไม่หยุดตาม
   → อาจมีข้อมูลเขียนลง S3 หรือ DynamoDB หลังจาก Cancel แล้ว

2. ข้อมูลอาจค้างกลางคัน (Partial State)
   → ถ้า TransformData กำลังเขียน S3 อยู่ ไฟล์อาจ Incomplete

3. ต้องทำ Cleanup ด้วยตัวเอง
   → ลบไฟล์ Partial ที่เขียนไม่เสร็จ
   → ส่ง Notification ว่า Job ถูก Cancel

4. SQS Message ที่ Start Execution ไปแล้ว จะไม่ถูก Retry อัตโนมัติ
   → ต้อง Re-queue ด้วยตัวเอง
```

> 💡 **Best Practice:** ออกแบบให้ State Machine มี `Catch` → `NotifyFailure` เสมอ และใน NotifyFailure Lambda ให้ทำ Cleanup งานที่ค้างอยู่ด้วย

---

## 🔧 เฉลยแบบฝึกหัดเพิ่มเติม Week 3

---

### แบบฝึกหัดที่ 1
**"เพิ่ม Parallel State: รัน validate-schema และตรวจสอบ File Size พร้อมกัน"**

**เฉลย — Lambda check-file-size:**

```python
def lambda_handler(event, context):
    """ตรวจสอบขนาดไฟล์ — รันพร้อมกับ validate-schema"""
    source_bucket = event['source_bucket']
    source_key    = event['source_key']
    job_id        = event['job_id']
    
    response     = s3.head_object(Bucket=source_bucket, Key=source_key)
    file_size_mb = response['ContentLength'] / (1024 * 1024)
    
    MAX_SIZE_MB = 10  # กำหนด Limit ที่ยอมรับได้
    
    return {
        **event,
        "file_size_mb":  round(file_size_mb, 2),
        "size_valid":    file_size_mb <= MAX_SIZE_MB,
        "size_check_msg": f"OK ({file_size_mb:.2f} MB)" if file_size_mb <= MAX_SIZE_MB 
                          else f"Too large ({file_size_mb:.2f} MB > {MAX_SIZE_MB} MB)"
    }
```

**เฉลย — ASL สำหรับ Parallel State:**

```json
"ValidateInParallel": {
  "Type": "Parallel",
  "Branches": [
    {
      "StartAt": "ValidateSchema",
      "States": {
        "ValidateSchema": {
          "Type": "Task",
          "Resource": "arn:aws:lambda:...:function:validate-schema",
          "End": true
        }
      }
    },
    {
      "StartAt": "CheckFileSize",
      "States": {
        "CheckFileSize": {
          "Type": "Task",
          "Resource": "arn:aws:lambda:...:function:check-file-size",
          "End": true
        }
      }
    }
  ],
  "ResultSelector": {
    "schema_result.$": "$[0]",
    "size_result.$":   "$[1]"
  },
  "ResultPath": "$.parallel_results",
  "Next": "CheckBothResults"
}
```

> 💡 **หมายเหตุ:** Parallel State จะรอให้ทุก Branch เสร็จก่อน แล้วรวม Output เป็น Array ดังนั้น `$[0]` = ผล Branch แรก และ `$[1]` = ผล Branch สอง

---

### แบบฝึกหัดที่ 2
**"เพิ่ม Wait State: ถ้า File Size > 1 MB ให้รอ 30 วินาที"**

**เฉลย — ASL:**

```json
"CheckIfLargeFile": {
  "Type": "Choice",
  "Choices": [
    {
      "Variable": "$.file_size_mb",
      "NumericGreaterThan": 1.0,
      "Next": "WaitForRateLimit"
    }
  ],
  "Default": "TransformData"
},

"WaitForRateLimit": {
  "Type": "Wait",
  "Seconds": 30,
  "Comment": "Rate limiting: wait before processing large files",
  "Next": "TransformData"
}
```

**ทางเลือกขั้นสูง — Wait จนถึงเวลาที่กำหนด:**

```json
"WaitUntilOffPeak": {
  "Type": "Wait",
  "TimestampPath": "$.process_after_time",
  "Comment": "Process during off-peak hours (from event input)",
  "Next": "TransformData"
}
```

---

## 🚀 เทคนิคและทริคสำหรับชีวิตจริง Week 3

### 🎯 Tip 1: ใช้ ResultPath เพื่อรักษาข้อมูล Input

```json
// ❌ ไม่ระบุ ResultPath → Lambda Output ทับ Input ทั้งหมด
"ParseCSV": {
  "Type": "Task",
  "Resource": "...",
  "Next": "ValidateSchema"
}

// ✅ ระบุ ResultPath → เพิ่ม Output เข้า Input โดยไม่ทับ
"ParseCSV": {
  "Type": "Task", 
  "Resource": "...",
  "ResultPath": "$.parse_result",   // เพิ่ม parse_result เข้าไปใน Event
  "Next": "ValidateSchema"
}
// Event ถัดไปจะมีทั้งข้อมูลเดิมและ parse_result
```

### 🎯 Tip 2: ใช้ Pass State สำหรับ Debugging

```json
// ✅ Pass State ส่งข้อมูลต่อโดยไม่ทำอะไร — ดีสำหรับ Test Flow
"MockTransform": {
  "Type": "Pass",
  "Result": {
    "transform_status": "success",
    "output_key": "test/mock_result.json"
  },
  "ResultPath": "$.transform_output",
  "Next": "ProcessingComplete"
}
// ใช้แทน Lambda จริงขณะยังพัฒนา Lambda ไม่เสร็จ
```

### 🎯 Tip 3: ตั้งชื่อ Execution ให้มีความหมาย

```python
# ❌ ชื่อ Execution แบบไม่มีความหมาย
sfn.start_execution(
    stateMachineArn=STATE_MACHINE_ARN,
    name=f"execution-{uuid.uuid4()}"  # ค้นหาไม่ได้
)

# ✅ ชื่อที่ Search ได้
timestamp = datetime.utcnow().strftime('%Y%m%dT%H%M%S')
sfn.start_execution(
    stateMachineArn=STATE_MACHINE_ARN,
    name=f"csv-{job_id[:8]}-{timestamp}"
    # ค้นหาใน Console ด้วย job_id ได้ทันที
)
```

---

---

# 📅 WEEK 4 — Notification & Monitoring

---

## 📖 สรุปหัวข้อการเรียน Week 4

### แนวคิดหลักที่ต้องจำ

**1. SNS Pub/Sub Pattern**

```
Publisher (Lambda) → SNS Topic → Subscribers
                                   ├── Email
                                   ├── SMS  
                                   ├── Lambda (Trigger อื่นๆ)
                                   ├── SQS Queue (Buffer)
                                   └── HTTP/HTTPS Endpoint
```

**2. SNS vs SQS เลือกอย่างไร**

| ต้องการ | ใช้ |
|---------|-----|
| แจ้งเตือนหลาย Channel พร้อมกัน | **SNS** (Fan-out) |
| เก็บงานรอ Consumer ค่อยๆ ประมวลผล | **SQS** (Queue) |
| แจ้งเตือนหลาย Channel + เก็บ Buffer | **SNS → SQS** (Fan-out + Queue) |
| Exactly-once Processing | **SQS FIFO** |

**3. CloudWatch Alarm States**

```
OK       → Metric อยู่ใน Range ปกติ
ALARM    → Metric เกิน Threshold → Action (ส่ง SNS)
INSUFFICIENT_DATA → ยังไม่มีข้อมูลพอที่จะตัดสิน (ช่วงแรกหลัง Create)
```

**4. CloudWatch Dashboard — Metrics สำคัญของ Pipeline**

| Service | Metric ที่ควรดู | เหตุผล |
|---------|---------------|--------|
| Lambda | Invocations, Errors, Duration | รู้ว่า Function ถูกเรียกบ่อยแค่ไหน และ Error เท่าไหร่ |
| SQS | ApproximateNumberOfMessagesVisible | รู้ว่า Queue คั่งค้างหรือเปล่า |
| SQS (DLQ) | ApproximateNumberOfMessagesVisible | มี Failed Message หรือเปล่า |
| Step Functions | ExecutionsFailed, ExecutionsSucceeded | Pipeline ทำงานปกติหรือเปล่า |

**5. Pipeline สมบูรณ์ที่สร้างตลอด 4 สัปดาห์**

```
[User Upload CSV]
       │
[S3: raw/uploads/]
       │ S3 ObjectCreated Event
       ▼
[Lambda: csv-validator]
  • ตรวจ .csv
  • ตรวจ headers
  • ส่ง Message → SQS
       │
[SQS: pipeline-main-queue]
  (DLQ: pipeline-dlq → DLQ Alarm → Email Alert)
       │ SQS Trigger
       ▼
[Lambda: csv-processor]
  • รับ Message จาก SQS
  • start_execution() → Step Functions
       │
[Step Functions: ProcessCSVWorkflow]
  ParseCSV → ValidateSchema → CheckValidation
                           /                \
                    Valid                 Invalid
                      │                      │
              [TransformData]       [MoveToFailed → S3 failed/]
                      │
              [send-notification]
                      │
              [SNS: pipeline-notifications]
              /             \
          [Email]           [SQS สำหรับ Integration อื่น]

[CloudWatch Dashboard + 3 Alarms]
```

---

## ❓ เฉลยคำถามท้าย LAB Week 4

---

### คำถามที่ 1
**"SNS Subscription แบบ Email กับแบบ SQS ต่างกันยังไงในแง่ Reliability? อะไรเกิดขึ้นถ้า Email Server Down?"**

**เฉลย:**

| | Email Subscription | SQS Subscription |
|--|------------------|-----------------|
| **Delivery Guarantee** | Best-effort — SNS พยายาม Deliver แต่ไม่รับประกัน | At-least-once — SQS เก็บ Message ไว้จนกว่าจะ Deliver |
| **ถ้า Receiver Down** | Message อาจหาย (SNS Retry บ้าง แต่จำกัด) | Message อยู่ใน SQS Queue นาน 4 วัน รอให้ Consumer กลับมา |
| **Retry** | SNS มี Retry Policy แต่จำกัด | SQS Retry ได้ตาม maxReceiveCount |
| **Ordering** | ไม่รับประกัน | Standard: ไม่รับประกัน / FIFO: รับประกัน |
| **ใช้เมื่อ** | Human Notification (ยอมหายได้บ้าง) | System Integration ที่ต้องการความน่าเชื่อถือ |

**ถ้า Email Server Down:**
- SNS ส่ง Email ล้มเหลว → Retry ตาม Retry Policy (สูงสุด ~23 ชั่วโมง)
- ถ้า Retry หมดแล้วยังล้มเหลว → Email หาย ไม่มี Dead Letter สำหรับ Email Sub
- ดังนั้น **ถ้า Notification สำคัญมาก ควรใช้ SNS → SQS → Lambda** แทน Email โดยตรง

**Pattern ที่ดีกว่าสำหรับ Critical Notification:**

```
SNS Topic
  ├── Email Subscription (Human notification — best effort OK)
  └── SQS Subscription → Lambda → เก็บใน DynamoDB/Database
                                 → ถ้ายังไม่ Acknowledge ใน 15 นาที → Alert ซ้ำ
```

---

### คำถามที่ 2
**"CloudWatch Alarm มีกี่ State? แต่ละ State หมายความว่าอะไร?"**

**เฉลย:**

CloudWatch Alarm มี **3 States:**

| State | ความหมาย | Action ที่ Trigger |
|-------|---------|-----------------|
| **OK** | Metric อยู่ใน Range ที่ยอมรับได้ | ✅ ปกติ (อาจส่ง OK Notification ถ้าตั้งไว้) |
| **ALARM** | Metric เกิน Threshold ที่กำหนด | ⚠️ ส่ง SNS Notification, Auto Scale, อื่นๆ |
| **INSUFFICIENT_DATA** | ไม่มีข้อมูลเพียงพอสำหรับประเมิน | 🔵 ช่วงเริ่มต้น หรือไม่มี Metric ใหม่เข้ามา |

**State Transition:**
```
(สร้าง Alarm ใหม่) → INSUFFICIENT_DATA
                          ↓ (ได้รับ Metric)
                    ┌─────┴─────┐
                    ↓           ↓
                   OK         ALARM
                    ↕           ↕ (Threshold เปลี่ยน)
                    └─────┬─────┘
                          ↓ (ไม่มี Metric นาน)
                    INSUFFICIENT_DATA
```

**เทคนิค — ตั้ง Action สำหรับทุก State Transition:**
```
OK Action:      ส่ง "ระบบกลับมาปกติแล้ว" แจ้ง Engineer ว่าหยุด Monitor ได้
ALARM Action:   ส่ง Alert ให้ On-Call Engineer ทันที
INSUFFICIENT_DATA Action: อาจส่ง Warning ว่า "ไม่ได้รับ Metric — ระบบอาจมีปัญหา"
```

---

### คำถามที่ 3
**"ถ้าต้องการ Monitor Latency ของ Pipeline ทั้งหมด (ตั้งแต่ Upload จนถึง Email ส่ง) จะวัดได้ยังไง?"**

**เฉลย:**

วิธีที่ดีที่สุดคือ **Timestamp ที่แต่ละ Step** และคำนวณ End-to-End Duration:

```python
# ✅ วิธีที่ 1: เก็บ Timestamp ในแต่ละ Lambda แล้วรวมใน send-notification
# ใน csv-validator:
message = {
    "job_id": job_id,
    "upload_detected_at": event_time,   # S3 Event Timestamp
    "validator_queued_at": datetime.utcnow().isoformat() + "Z",
    # ...
}

# ใน send-notification Lambda:
def lambda_handler(event, context):
    now          = datetime.utcnow()
    uploaded_at  = datetime.fromisoformat(event['upload_detected_at'].rstrip('Z'))
    total_sec    = (now - uploaded_at).total_seconds()
    
    logger.info(json.dumps({
        "event":           "pipeline_complete",
        "job_id":          event['job_id'],
        "total_latency_s": total_sec,
        "breakdown": {
            "upload_to_queue_s":    ...,
            "queue_to_sfn_s":       ...,
            "sfn_execution_s":      event.get('sfn_duration'),
        }
    }))
    
    # ✅ ส่ง Custom Metric ไป CloudWatch
    cloudwatch.put_metric_data(
        Namespace='DataPipeline/Latency',
        MetricData=[{
            'MetricName': 'EndToEndLatency',
            'Value':      total_sec,
            'Unit':       'Seconds'
        }]
    )
```

**วิธีที่ขั้นสูงกว่า — AWS X-Ray:**

```python
# ✅ เปิด X-Ray Tracing ใน Lambda
# Lambda → Configuration → Monitoring and operations tools → Active tracing: ON

from aws_xray_sdk.core import xray_recorder, patch_all
patch_all()  # Auto-instrument boto3 calls

# X-Ray จะ Track ทุก AWS SDK Call อัตโนมัติ
# และแสดง Timeline ของทุก Step ใน X-Ray Console
```

---

## 🔧 เฉลยแบบฝึกหัดเพิ่มเติม Week 4

---

### แบบฝึกหัดที่ 1
**"เพิ่ม SMS Notification: สร้าง SNS Subscription แบบ SMS"**

**เฉลย — ขั้นตอน:**

1. **SNS Console** → `pipeline-notifications` → **Create subscription**
2. Protocol: **SMS**
3. Endpoint: `+6681XXXXXXX` (ใส่เบอร์มือถือจริงพร้อม Country Code)
4. กด **Create subscription** (ไม่ต้อง Confirm ต่างจาก Email)

**ข้อควรระวัง:**

```
Free Tier ของ SNS SMS: 100 SMS ฟรี/เดือน สำหรับ US เท่านั้น
สำหรับ Thailand (+66): คิดเงินทุก SMS (~$0.04–0.08/SMS)

✅ ใช้ทดสอบได้ แต่ใน Production ระวัง Cost
✅ ตั้ง Budget Alert ก่อนเปิดใช้ SMS

ทางเลือกประหยัดกว่า:
  LINE Notify / Telegram Bot / Slack → ใช้ Lambda Subscribe กับ SNS
  แล้วส่งต่อไป Messaging Platform → ฟรีทั้งหมด
```

---

### แบบฝึกหัดที่ 2
**"สร้าง CloudWatch Metric Filter: ดึง Custom Metric จาก Log เช่น นับ `event: file_validated` ต่อชั่วโมง"**

**เฉลย:**

1. **CloudWatch** → **Log groups** → `/aws/lambda/csv-validator`
2. กด **Metric filters** → **Create metric filter**
3. กรอก Filter pattern:

```
{ $.event = "file_validated" }
```

4. กด **Test pattern** → ใส่ Log ตัวอย่าง → ตรวจสอบว่า Match

5. กำหนด Metric:
```
Filter name: FilesValidatedFilter
Metric namespace: DataPipeline/FileProcessing
Metric name: FilesValidated
Metric value: 1
Default value: 0
Unit: Count
```

6. กด **Create metric filter**

**ใช้งาน Metric นี้:**

```python
# ดู Metric ใน CloudWatch → Metrics → DataPipeline/FileProcessing → FilesValidated
# สร้าง Graph: Sum per 1 hour → เห็น Peak Hours ของการ Upload ไฟล์

# สร้าง Alarm บน Metric นี้:
# ถ้า FilesValidated = 0 นานกว่า 4 ชั่วโมง → อาจมีปัญหาที่ต้นทาง
```

---

### แบบฝึกหัดที่ 3
**"เพิ่ม S3 Lifecycle Policy: ตั้งให้ไฟล์ใน `failed/` ถูกลบอัตโนมัติหลัง 30 วัน"**

**เฉลย:**

1. เข้า **S3** → `pipeline-raw-[ชื่อคุณ]`
2. กด **Management** tab → **Lifecycle rules** → **Create lifecycle rule**
3. กรอกข้อมูล:

```
Rule name:    delete-failed-files
Rule scope:   Limit the scope using filters
Prefix:       failed/                   ← เฉพาะ folder นี้เท่านั้น

Lifecycle rule actions:
  ✅ Expire current versions of objects

Expire current versions:
  Days after object creation: 30
```

4. กด **Create rule**

**เพิ่มเติม — Transition ก่อน Delete (ประหยัด Cost):**

```
วันที่ 0:   ไฟล์ Upload มา (S3 Standard: $0.023/GB/เดือน)
วันที่ 7:   Transition → S3 Infrequent Access ($0.0125/GB/เดือน) ประหยัด 45%
วันที่ 30:  Delete อัตโนมัติ
```

---

## 🚀 เทคนิคและทริคสำหรับชีวิตจริง Week 4

### 🎯 Tip 1: สร้าง Runbook สำหรับแต่ละ Alarm

ใน Production จริงๆ ทุก Alarm ควรมี Runbook ควบคู่กัน:

```markdown
# Runbook: pipeline-dlq-messages-alarm

## Symptom
CloudWatch Alarm "pipeline-dlq-messages-alarm" Triggered

## Immediate Actions (5 นาทีแรก)
1. เปิด SQS Console → pipeline-dlq → ดูจำนวน Messages
2. กด "Send and receive messages" → Poll → อ่าน Message Body
3. ดู Error Type จาก Message Body

## Diagnosis
- KeyError ใน Message Body → CSV format เปลี่ยน → แจ้ง Data Team
- S3 Access Denied → IAM Policy หมดอายุหรือถูกแก้ไข → ตรวจ IAM
- Lambda Timeout → ไฟล์ใหญ่เกินไป → เพิ่ม Timeout หรือ Memory

## Recovery
1. แก้ไข Root Cause
2. Redrive DLQ Messages: SQS → DLQ → Start DLQ redrive
3. Monitor ว่า Messages ถูก Process สำเร็จ
4. Update Runbook ด้วย Lesson Learned
```

### 🎯 Tip 2: ใช้ SNS → Lambda แทน Email สำหรับ Smart Notification

```python
# Lambda ที่ Subscribe กับ SNS → ส่งต่อไป Slack
import json, urllib.request

SLACK_WEBHOOK = "https://hooks.slack.com/services/YOUR/WEBHOOK/URL"

def lambda_handler(event, context):
    sns_msg = json.loads(event['Records'][0]['Sns']['Message'])
    
    # Format Slack Message ให้สวยงาม
    job_id   = sns_msg.get('job_id', 'unknown')
    status   = sns_msg.get('status', 'unknown')
    emoji    = "✅" if status == "success" else "❌"
    
    slack_payload = {
        "text": f"{emoji} *Pipeline {status.upper()}*",
        "attachments": [{
            "color":  "good" if status == "success" else "danger",
            "fields": [
                {"title": "Job ID",  "value": job_id,                        "short": True},
                {"title": "Status",  "value": status,                        "short": True},
                {"title": "Revenue", "value": f"฿{sns_msg.get('total_revenue', 0):,.2f}", "short": True},
            ]
        }]
    }
    
    req = urllib.request.Request(SLACK_WEBHOOK, 
                                  data=json.dumps(slack_payload).encode(),
                                  method='POST')
    urllib.request.urlopen(req)
```

---

---

# 🗺️ Mindmap ความรู้ทั้ง 4 สัปดาห์

```
AWS Serverless Data Pipeline
│
├── Week 1: Event-Driven
│   ├── S3 Events (ObjectCreated, ObjectRemoved)
│   ├── Lambda Handler (event, context)
│   ├── IAM Least Privilege
│   ├── Structured Logging (JSON)
│   └── Idempotency Pattern
│
├── Week 2: Message Queue
│   ├── SQS Standard vs FIFO
│   ├── Visibility Timeout Rule
│   ├── Dead Letter Queue (DLQ)
│   ├── Long Polling vs Short Polling
│   └── Batch Item Failures
│
├── Week 3: Orchestration
│   ├── Choreography vs Orchestration
│   ├── Amazon States Language (ASL)
│   ├── State Types: Task, Choice, Parallel, Wait, Map
│   ├── Retry + Exponential Backoff
│   └── ResultPath / InputPath / OutputPath
│
└── Week 4: Notification & Observability
    ├── SNS Pub/Sub (Fan-out)
    ├── CloudWatch Metrics + Alarms
    ├── CloudWatch Logs + Metric Filters
    ├── Alarm States (OK / ALARM / INSUFFICIENT_DATA)
    └── S3 Lifecycle Policy
```

---

# ⚖️ Design Patterns เปรียบเทียบ

| Pattern | ใช้ใน Lab | เมื่อไหร่ใช้ในชีวิตจริง | ข้อระวัง |
|---------|---------|----------------------|---------|
| **Event-Driven** (S3 → Lambda) | Week 1 | ตอบสนองต่อ File Upload, User Action | ออกแบบ Idempotent เสมอ |
| **Message Queue** (SQS) | Week 2 | Load Leveling, Decouple Services | Visibility Timeout > Lambda Timeout |
| **Orchestration** (Step Functions) | Week 3 | Multi-step Workflow, Long-running Process | ใช้ Standard สำหรับ Audit Trail |
| **Fan-out** (SNS) | Week 4 | แจ้งเตือนหลาย Channel, Integration | Email ไม่ Reliable ใช้ SQS สำรอง |
| **Dead Letter Queue** | Week 2, 4 | Safety Net สำหรับ Failed Message | Monitor DLQ เสมอ ตั้ง Alarm |
| **Exponential Backoff** | Week 3 | Retry กับ Downstream Service | เพิ่ม Jitter ป้องกัน Thundering Herd |

---

# ✅ Production Readiness Checklist

ก่อน Deploy Pipeline ไป Production จริงๆ ตรวจสอบรายการนี้:

### Security
- [ ] IAM Roles ใช้ Least Privilege — ระบุ Resource ARN เจาะจง ไม่มี `"Resource": "*"`
- [ ] ไม่มี Secrets / Credentials ใน Source Code
- [ ] S3 Buckets ตั้ง Block All Public Access
- [ ] Lambda ไม่มี Layer หรือ Dependency ที่มีช่องโหว่

### Reliability
- [ ] Lambda ทุกตัวมี Timeout ที่เหมาะสม (ไม่ใช่ Default 3 วินาที)
- [ ] SQS มี Dead Letter Queue พร้อม Alarm
- [ ] Step Functions มี Catch + Retry ทุก Task State
- [ ] Lambda ทุกตัวออกแบบให้เป็น Idempotent

### Observability
- [ ] Structured Logging (JSON) ทุก Lambda
- [ ] CloudWatch Dashboard ครอบคลุม Services ทั้งหมด
- [ ] Alarms สำหรับ Error Rate, DLQ, Step Functions Failures
- [ ] Alarm มี Runbook ควบคู่

### Cost
- [ ] ตั้ง AWS Budget Alert ไว้แล้ว
- [ ] S3 Lifecycle Policy สำหรับ Data ที่ไม่ใช้
- [ ] CloudWatch Log Retention ตั้งเป็น 30–90 วัน (ไม่ใช่ Never Expire)
- [ ] Lambda Memory ตั้งให้เหมาะสม ไม่ Over-provision

### Deployment
- [ ] มี Staging Environment แยกจาก Production
- [ ] ใช้ Environment Variables แทน Hard-code ทุกค่า
- [ ] มี Infrastructure as Code (CloudFormation / CDK / Terraform)

---

*เอกสารเฉลยนี้จัดทำสำหรับ ICT24467 · อ.อำนาจ คงเจริญถิ่น · คณะ ICT มหาวิทยาลัยศรีปทุม · ภาคการศึกษา 2/2568*
