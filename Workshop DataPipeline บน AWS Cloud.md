# ICT24467 — การพัฒนาซอฟต์แวร์ระบบประมวลผลคลาวด์และความปลอดภัยของข้อมูล

## คู่มือประกอบการเรียนการสอน: 
# 🚀 AWS Cloud Workshop — Data Pipeline & Serverless Architecture
### แผนการสอน LAB ต่อเนื่อง 4 สัปดาห์ (Week8, 9, 10, 11) · AWS Free Tier ทั้งหมด

---

> **คณะเทคโนโลยีสารสนเทศ (School of Information Technology)**  
> มหาวิทยาลัยศรีปทุม · Sripatum University  
>
> | | |
> |---|---|
> | **รายวิชา** | ICT24467 — Cloud Computing Software Development and Data Security |
> | **ภาคการศึกษา** | 2 / 2568 |
> | **อาจารย์ผู้สอน** | อ.อำนาจ คงเจริญถิ่น |
> | **ระดับชั้น** | นักศึกษาปริญญาตรี คณะ ICT |
> | **ระยะเวลา** | 4 สัปดาห์ · ใช้ AWS Free Tier ทั้งหมด |

> **Prerequisite:** นักเรียนผ่านการเรียน EC2 และ Lambda + API Gateway เบื้องต้นมาแล้ว (Week6-7)

---

## 📑 สารบัญ

| | หัวข้อ |
|---|---|
| **ภาพรวม** | |
| | [ภาพรวมหลักสูตร](#-ภาพรวมหลักสูตร) |
| | [Architecture Overview](#architecture-overview-final--หลังทำครบ-4-สัปดาห์) |
| **Week 1** | [Event-Driven with S3 + Lambda](#-week-1--event-driven-with-s3--lambda) |
| | [STEP 1 — สร้าง S3 Buckets](#-step-1--สร้าง-s3-buckets) |
| | [STEP 2 — สร้าง IAM Role สำหรับ Lambda](#-step-2--สร้าง-iam-role-สำหรับ-lambda) |
| | [STEP 3 — สร้าง Lambda Function](#-step-3--สร้าง-lambda-function) |
| | [STEP 4 — ตั้งค่า S3 Event Trigger](#-step-4--ตั้งค่า-s3-event-trigger) |
| | [STEP 5 — สร้างไฟล์ CSV ทดสอบ](#-step-5--สร้างไฟล์-csv-ทดสอบ) |
| | [STEP 6 — ทดสอบ Pipeline](#-step-6--ทดสอบ-pipeline) |
| | [STEP 7 — ทดสอบ Lambda โดยตรง (Manual Test)](#-step-7--ทดสอบ-lambda-โดยตรง-manual-test) |
| | [แบบฝึกหัดเพิ่มเติม Week 1](#-แบบฝึกหัดเพิ่มเติม-week-1) |
| **Week 2** | [Message Queue with SQS](#-week-2--message-queue-with-sqs) |
| | [STEP 1 — สร้าง Dead Letter Queue ก่อน](#-step-1--สร้าง-dead-letter-queue-ก่อน) |
| | [STEP 2 — สร้าง Main Queue](#-step-2--สร้าง-main-queue) |
| | [STEP 3 — อัปเดต IAM Policy](#-step-3--อัปเดต-iam-policy) |
| | [STEP 4 — อัปเดต Lambda Validator ให้ส่ง Message ไป SQS](#-step-4--อัปเดต-lambda-validator-ให้ส่ง-message-ไป-sqs) |
| | [STEP 5 — สร้าง Lambda Consumer (csv-processor)](#-step-5--สร้าง-lambda-consumer-csv-processor) |
| | [STEP 6 — เชื่อม SQS กับ Lambda Consumer](#-step-6--เชื่อม-sqs-กับ-lambda-consumer) |
| | [STEP 7 — ทดสอบ End-to-End Pipeline](#-step-7--ทดสอบ-end-to-end-pipeline) |
| | [STEP 8 — ทดสอบ Dead Letter Queue](#-step-8--ทดสอบ-dead-letter-queue) |
| | [แบบฝึกหัดเพิ่มเติม Week 2](#-แบบฝึกหัดเพิ่มเติม-week-2) |
| **Week 3** | [Orchestration with Step Functions](#-week-3--orchestration-with-step-functions) |
| | [STEP 1 — สร้าง Lambda Functions สำหรับแต่ละ Step](#-step-1--สร้าง-lambda-functions-สำหรับแต่ละ-step) |
| | [STEP 2 — อัปเดต IAM Policy](#-step-2--อัปเดต-iam-policy) |
| | [STEP 3 — สร้าง State Machine](#-step-3--สร้าง-state-machine) |
| | [STEP 4 — อัปเดต SQS Consumer ให้เริ่ม Step Functions](#-step-4--อัปเดต-sqs-consumer-ให้เริ่ม-step-functions) |
| | [STEP 5 — ทดสอบ State Machine](#-step-5--ทดสอบ-state-machine) |
| | [แบบฝึกหัดเพิ่มเติม Week 3](#-แบบฝึกหัดเพิ่มเติม-week-3) |
| **Week 4** | [Notification & Recap](#-week-4--notification--recap) |
| | [STEP 1 — สร้าง SNS Topic](#-step-1--สร้าง-sns-topic) |
| | [STEP 2 — อัปเดต IAM Policy เพิ่ม SNS](#-step-2--อัปเดต-iam-policy-เพิ่ม-sns) |
| | [STEP 3 — สร้าง Lambda Notification](#-step-3--สร้าง-lambda-notification) |
| | [STEP 4 — อัปเดต Step Functions State Machine](#-step-4--อัปเดต-step-functions-state-machine) |
| | [STEP 5 — สร้าง CloudWatch Dashboard](#-step-5--สร้าง-cloudwatch-dashboard) |
| | [STEP 6 — ตั้ง CloudWatch Alarms](#-step-6--ตั้ง-cloudwatch-alarms) |
| | [STEP 7 — End-to-End Test สมบูรณ์](#-step-7--end-to-end-test-สมบูรณ์) |
| | [แบบฝึกหัดเพิ่มเติม Week 4](#-แบบฝึกหัดเพิ่มเติม-week-4) |
| **สรุป** | [Final Architecture & Summary](#️-final-architecture--summary) |
| | [Services สรุปทั้ง 4 สัปดาห์](#services-สรุปทั้ง-4-สัปดาห์) |
| | [Design Patterns ที่เรียนมาตลอด 4 สัปดาห์](#design-patterns-ที่เรียนมาตลอด-4-สัปดาห์) |
| | [Next Steps — ต่อยอดจากที่เรียน](#-next-steps--ต่อยอดจากที่เรียน) |

---

## 📋 ภาพรวมหลักสูตร

หลักสูตรนี้จะพานักเรียนสร้าง **Data Pipeline อัตโนมัติ** แบบ Serverless เต็มตัว โดยไม่มี Server เดียว ตั้งแต่รับไฟล์ → ประมวลผล → คิว → Orchestrate → แจ้งเตือน ทุกอย่างต่อกันเป็น Project เดียวคือ **"CSV Report Processor"** — ระบบที่รับไฟล์ CSV อัปโหลดขึ้น S3 แล้วประมวลผลและส่งผลลัพธ์ทาง Email อัตโนมัติ

| สัปดาห์ | หัวข้อ | Services หลัก | เวลาโดยประมาณ |
|--------|--------|---------------|--------------|
| Week 1 | Event-Driven with S3 + Lambda | S3, Lambda, IAM | 2–3 ชั่วโมง |
| Week 2 | Message Queue with SQS | SQS, Lambda | 2–3 ชั่วโมง |
| Week 3 | Orchestration with Step Functions | Step Functions, Lambda | 2–3 ชั่วโมง |
| Week 4 | Notification & Recap | SNS, CloudWatch, Architecture Review | 2–3 ชั่วโมง |

### 🎯 เป้าหมายปลายทาง
- นักเรียนมี **Data Pipeline อัตโนมัติ** ที่รับไฟล์ → ประมวลผล → แจ้งเตือน โดยไม่มี Server เลย
- ต้นทุน **$0** ตลอดหลักสูตร (AWS Free Tier ทั้งหมด)
- เข้าใจ Pattern สำคัญ: **Event-Driven, Decoupling, Orchestration, Observability**
- ต่อยอดสู่ Production Pipeline จริงได้

### 🛠️ สิ่งที่ต้องเตรียมก่อนเริ่ม
- AWS Account (Free Tier)
- Python 3.x ติดตั้งในเครื่อง
- VS Code หรือ Editor ที่ถนัด
- ไฟล์ CSV ตัวอย่างสำหรับทดสอบ (สร้างเองได้ง่ายๆ)
- Email จริงสำหรับรับ SNS Notification (Week 4)

### ⚠️ Free Tier Limits ที่ควรรู้
| Service | Free Tier |
|---------|-----------|
| S3 | 5 GB storage, 20,000 GET, 2,000 PUT /เดือน |
| Lambda | 1 million invocations, 400,000 GB-seconds /เดือน ตลอดชีพ |
| SQS | 1 million requests /เดือน ตลอดชีพ |
| Step Functions | 4,000 state transitions /เดือน ตลอดชีพ |
| SNS | 1 million publishes, 1,000 email deliveries /เดือน ตลอดชีพ |
| CloudWatch | 5 GB log ingest, 10 custom metrics /เดือน (12 เดือนแรก) |

---

## Architecture Overview (Final — หลังทำครบ 4 สัปดาห์)

```
[User] ──Upload CSV──> [S3: raw-uploads/]
                              │
                    S3 Event Trigger
                              │
                              ▼
                     [Lambda: Validator]
                              │
                    ส่ง Message เข้า Queue
                              │
                              ▼
                       [SQS Queue]
                              │
                  SQS Trigger (Polling)
                              │
                              ▼
                  [Step Functions: Workflow]
                    ┌──────────────────┐
                    │  1. Parse CSV    │
                    │  2. Transform    │
                    │  3. Save Result  │
                    │  4. Notify       │
                    └──────────────────┘
                              │
                    ┌─────────┴─────────┐
                    ▼                   ▼
           [S3: processed/]      [SNS Topic]
                                        │
                                        ▼
                                 [Email / SMS]

[CloudWatch] ──── Monitors ────> ทุก Service
```

---

---

# 📅 WEEK 1 — Event-Driven with S3 + Lambda

> **หัวข้อ:** สร้าง Trigger อัตโนมัติเมื่อ Upload ไฟล์ขึ้น S3

---

## 🎓 วัตถุประสงค์การเรียนรู้
- อธิบาย Event-Driven Architecture และประโยชน์เทียบกับ Polling ได้
- สร้าง S3 Bucket และตั้งค่า Event Notification ไปยัง Lambda
- เขียน Lambda ที่รับ S3 Event และประมวลผลไฟล์ CSV
- ตั้งค่า IAM Role ให้ Lambda มีสิทธิ์ถูกต้องตาม Least Privilege
- ดู CloudWatch Logs เพื่อ Debug Lambda

---

## 📖 ความรู้พื้นฐาน (Lecture — 30 นาที)

### Event-Driven Architecture คืออะไร?

แทนที่จะให้ระบบ "ถามซ้ำๆ" ว่ามีงานใหม่ไหม (Polling) Event-Driven Architecture ให้ระบบ "ตอบสนองเมื่อมีเหตุการณ์เกิดขึ้น" ทันที

**เปรียบเทียบ:**
- **Polling:** เหมือนโทรถามร้านอาหารทุก 5 นาทีว่าอาหารพร้อมยัง
- **Event-Driven:** เหมือนให้ร้านโทรหาเมื่ออาหารพร้อม

**ข้อดีของ Event-Driven:**
- ประหยัด Resource — ทำงานเฉพาะเมื่อจำเป็น
- Scale ได้ดี — หลาย Event เกิดพร้อมกันได้
- Loose Coupling — แต่ละส่วนไม่รู้จักกันโดยตรง
- ต้นทุนต่ำ — Lambda จ่ายตามการใช้งานจริง

### S3 Events คืออะไร?
S3 สามารถส่ง Notification ไปยัง Lambda, SQS, หรือ SNS ได้อัตโนมัติเมื่อ:
- `s3:ObjectCreated:*` — มีไฟล์ถูก Upload
- `s3:ObjectRemoved:*` — มีไฟล์ถูกลบ
- `s3:ObjectRestore:*` — มีไฟล์ถูก Restore จาก Glacier

### Project ที่จะสร้างใน Week 1

```
[ผู้ใช้ Upload sales_data.csv] 
        │
        ▼
[S3 Bucket: raw-uploads/]
        │
  S3 Event Trigger (ObjectCreated)
        │
        ▼
[Lambda: csv-validator]
   - ตรวจสอบว่าเป็น .csv จริงไหม
   - นับจำนวน rows
   - Log ผลลัพธ์ใน CloudWatch
```

---

## 🔧 LAB Step-by-Step

---

### ✅ STEP 1 — สร้าง S3 Buckets

เราจะสร้าง 2 Buckets แยกกันชัดเจน:

**Bucket 1: สำหรับรับไฟล์ดิบ**

1. เข้า **AWS Console** → ค้นหา **S3** → **Create bucket**
2. กรอกข้อมูล:
   ```
   Bucket name: pipeline-raw-[ชื่อคุณ]-[random4digits]
   Region: ap-southeast-1 (Singapore)
   Block all public access: ✅ เปิดไว้ทั้งหมด (default)
   Versioning: Disable
   ```
3. กด **Create bucket**

**Bucket 2: สำหรับเก็บผลลัพธ์**

1. สร้าง Bucket ใหม่อีกอัน:
   ```
   Bucket name: pipeline-processed-[ชื่อคุณ]-[random4digits]
   Region: ap-southeast-1 (Singapore)
   (Settings อื่นเหมือนกัน)
   ```

**สร้าง Folder Structure ใน Bucket แรก:**

1. กดเข้า `pipeline-raw-...`
2. กด **Create folder** → ชื่อ `uploads/` → Create
3. กด **Create folder** อีกอัน → ชื่อ `failed/` → Create

> 💡 **ทำไมต้องแยก Bucket?** เพื่อป้องกัน Recursive Loop — ถ้า Lambda อ่านจาก Bucket เดียวกับที่มัน Write ลง จะเกิด Event Loop ไม่สิ้นสุด และค่าใช้จ่ายพุ่งทันที!

---

### ✅ STEP 2 — สร้าง IAM Role สำหรับ Lambda

Lambda ต้องมีสิทธิ์ถูกต้องในการเข้าถึง S3 — เราจะสร้างแบบ Least Privilege

1. เข้า **IAM** → **Policy** → **สร้าง Custom Policy ก่อน** (แทนที่จะใช้ Managed Policy กว้างๆ):
   - คลิก **Create policy** (เปิด Tab ใหม่)
   - เลือก **JSON** tab → วางโค้ดนี้:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ReadFromRawBucket",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:HeadObject"
      ],
      "Resource": "arn:aws:s3:::pipeline-raw-[ชื่อคุณ]-*/*"
    },
    {
      "Sid": "WriteToProcessedBucket",
      "Effect": "Allow",
      "Action": [
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::pipeline-processed-[ชื่อคุณ]-*/*"
    },
    {
      "Sid": "CloudWatchLogs",
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents"
      ],
      "Resource": "arn:aws:logs:*:*:*"
    }
  ]
}
```

2. Policy name: `pipeline-lambda-policy` → **Create policy**
3. กลับไปหน้า **IAM** → **Roles** → **Create role**
4. **Trusted entity:** AWS service → **Lambda** → Next Create Role → ค้นหา `pipeline-lambda-policy` → เลือก → Next
5. Role name: `pipeline-lambda-role` → **Create role**

> 🔒 **Security Note:** เราระบุ Resource ARN แบบเจาะจง ไม่ใช้ `"Resource": "*"` เพราะถ้า Lambda ถูก Compromise จะได้ไม่เข้า Resource อื่นได้

---

### ✅ STEP 3 — สร้าง Lambda Function

1. เข้า **Lambda** → **Create function**
2. กรอกข้อมูล:
   ```
   Function name: csv-validator
   Runtime: Python 3.12
   Architecture: x86_64
   Execution role: Use an existing role → pipeline-lambda-role
   ```
3. กด **Create function**
4. ใน **Code** tab → แทนที่โค้ดทั้งหมดด้วย:

```python
import json
import boto3
import csv
import io
import logging
from datetime import datetime

# ตั้งค่า Logger
logger = logging.getLogger()
logger.setLevel(logging.INFO)

s3 = boto3.client('s3')

def lambda_handler(event, context):
    """
    รับ S3 Event เมื่อมีไฟล์ถูก Upload
    ตรวจสอบว่าเป็น CSV ที่ถูกต้อง และ Log ข้อมูลสำคัญ
    """
    
    logger.info(f"Received event: {json.dumps(event)}")
    
    results = []
    
    for record in event['Records']:
        # ดึงข้อมูลไฟล์จาก Event
        bucket_name = record['s3']['bucket']['name']
        object_key = record['s3']['object']['key']
        file_size = record['s3']['object']['size']
        event_time = record['eventTime']
        
        logger.info(json.dumps({
            "event": "file_received",
            "bucket": bucket_name,
            "key": object_key,
            "size_bytes": file_size,
            "timestamp": event_time
        }))
        
        # ตรวจสอบนามสกุลไฟล์
        if not object_key.lower().endswith('.csv'):
            logger.warning(f"File {object_key} is not a CSV file. Skipping.")
            results.append({
                "file": object_key,
                "status": "rejected",
                "reason": "Not a CSV file"
            })
            continue
        
        # ดาวน์โหลดและอ่านไฟล์จาก S3
        try:
            response = s3.get_object(Bucket=bucket_name, Key=object_key)
            content = response['Body'].read().decode('utf-8')
            
            # Parse CSV
            csv_reader = csv.DictReader(io.StringIO(content))
            rows = list(csv_reader)
            headers = csv_reader.fieldnames
            
            # ตรวจสอบว่ามีข้อมูลหรือเปล่า
            if len(rows) == 0:
                logger.warning(f"File {object_key} is empty (no data rows)")
                results.append({
                    "file": object_key,
                    "status": "rejected",
                    "reason": "Empty file"
                })
                continue
            
            # สรุปข้อมูลไฟล์
            summary = {
                "event": "file_validated",
                "file": object_key,
                "bucket": bucket_name,
                "status": "valid",
                "total_rows": len(rows),
                "headers": list(headers) if headers else [],
                "file_size_bytes": file_size,
                "processed_at": datetime.now().isoformat()
            }
            
            logger.info(json.dumps(summary))
            
            results.append({
                "file": object_key,
                "status": "valid",
                "rows": len(rows),
                "headers": list(headers) if headers else []
            })
            
        except Exception as e:
            logger.error(json.dumps({
                "event": "processing_error",
                "file": object_key,
                "error": str(e)
            }))
            results.append({
                "file": object_key,
                "status": "error",
                "reason": str(e)
            })
    
    logger.info(f"Processing complete. Results: {json.dumps(results)}")
    
    return {
        "statusCode": 200,
        "body": json.dumps({
            "message": f"Processed {len(results)} file(s)",
            "results": results
        })
    }
```

5. กด **Deploy**

**ตั้งค่า Timeout:**
- **Configuration** tab → **General configuration** → **Edit**
- Timeout: **30 seconds** (default 3 วินาทีสั้นเกินไปสำหรับ CSV ขนาดใหญ่)
- Memory: **256 MB**
- กด **Save**

---

### ✅ STEP 4 — ตั้งค่า S3 Event Trigger

1. ยังอยู่ใน Lambda → **Configuration** tab → **Triggers** → **Add trigger**
2. เลือก **S3**
3. กรอกข้อมูล:
   ```
   Bucket: pipeline-raw-[ชื่อคุณ]
   Event types: All object create events
   Prefix: uploads/          ← สำคัญมาก! รับเฉพาะจาก folder นี้
   Suffix: .csv              ← รับเฉพาะไฟล์ .csv
   ```
4. ✅ Acknowledge recursive warning → **Add**

> ⚠️ **สำคัญมาก:** การตั้ง Prefix `uploads/` ทำให้ Lambda trigger เฉพาะไฟล์ที่อยู่ใน folder นี้เท่านั้น ป้องกัน Recursive Loop ในกรณีที่เขียนกลับมายัง Bucket เดียวกัน

---

### ✅ STEP 5 — สร้างไฟล์ CSV ทดสอบ

สร้างไฟล์ `sample_sales.csv` ในเครื่อง:

```csv
order_id,customer_name,product,quantity,price,date
ORD001,สมชาย ใจดี,Widget A,5,250.00,2024-01-15
ORD002,สมหญิง รักเรียน,Widget B,2,450.00,2024-01-15
ORD003,วิชัย มานะ,Widget A,10,250.00,2024-01-16
ORD004,นิดา สุขใจ,Widget C,1,1200.00,2024-01-16
ORD005,ประสิทธิ์ ดีงาม,Widget B,3,450.00,2024-01-17
```

---

### ✅ STEP 6 — ทดสอบ Pipeline

**อัปโหลดไฟล์:**
1. เข้า S3 → `pipeline-raw-...` → เข้า folder `uploads/`
2. กด **Upload** → Add files → เลือก `sample_sales.csv` → **Upload**

**ตรวจสอบ CloudWatch Logs:**
1. เข้า **CloudWatch** → **Log groups** → `/aws/lambda/csv-validator`
2. กด Log Stream ล่าสุด
3. ควรเห็น Log แบบนี้:

```json
{
  "event": "file_validated",
  "file": "uploads/sample_sales.csv",
  "status": "valid",
  "total_rows": 5,
  "headers": ["order_id", "customer_name", "product", "quantity", "price", "date"],
  "file_size_bytes": 312
}
```

**ทดสอบกรณี Error:**
1. อัปโหลดไฟล์ที่ไม่ใช่ CSV เช่น `test.txt` ไปที่ `uploads/`
2. ดู Log — ควรเห็น `"status": "rejected", "reason": "Not a CSV file"`

---

### ✅ STEP 7 — ทดสอบ Lambda โดยตรง (Manual Test)

ก่อน Trigger จาก S3 ควรทดสอบ Lambda โดยตรงก่อน:

1. ใน Lambda → **Test** tab → **Create new event**
2. Event name: `test-s3-event`
3. วาง JSON นี้เป็น Event:

```json
{
  "Records": [
    {
      "eventVersion": "2.1",
      "eventSource": "aws:s3",
      "eventTime": "2024-01-15T10:00:00.000Z",
      "eventName": "ObjectCreated:Put",
      "s3": {
        "bucket": {
          "name": "pipeline-raw-[ชื่อคุณ]-[random]"
        },
        "object": {
          "key": "uploads/sample_sales.csv",
          "size": 312
        }
      }
    }
  ]
}
```

4. กด **Test** → ดูผลลัพธ์ใน Execution results

---

### 📝 แบบฝึกหัดเพิ่มเติม Week 1

1. **แก้ไข Lambda** ให้ตรวจสอบว่าไฟล์มี Column `order_id` อยู่หรือเปล่า ถ้าไม่มีให้ Reject
2. **เพิ่ม Metric:** ใช้ `boto3` ส่ง Custom Metric ไป CloudWatch เพื่อนับจำนวนไฟล์ที่ Valid/Invalid ต่อวัน
3. **ทดลอง** Upload ไฟล์ CSV ขนาดใหญ่ (1,000 rows) แล้วดูว่า Duration เพิ่มขึ้นเท่าไหร่

### ❓ คำถามท้าย LAB Week 1

1. ทำไม S3 Event Trigger ถึงไม่รับประกันว่าจะ Trigger **ครั้งเดียว** เสมอ? แล้วจะออกแบบ Lambda ให้รองรับ Duplicate Events ได้ยังไง? (Idempotency)
2. Lambda มี Concurrency Limit เท่าไหร่ใน Default? ถ้า Upload ไฟล์พร้อมกัน 1,000 ไฟล์จะเกิดอะไรขึ้น?
3. Prefix `uploads/` ใน S3 Trigger ป้องกัน Recursive Loop ได้จริงหรือเปล่า? มีกรณีที่ยังเกิด Loop ได้ไหม?

---

---

# 📅 WEEK 2 — Message Queue with SQS

> **หัวข้อ:** เพิ่ม SQS เพื่อ Decouple ระบบและรองรับ High Volume

---

## 🎓 วัตถุประสงค์การเรียนรู้
- อธิบาย Decoupling และประโยชน์ของ Message Queue ได้
- เข้าใจความแตกต่างระหว่าง Standard Queue กับ FIFO Queue
- เชื่อม Lambda (Producer) → SQS → Lambda (Consumer)
- จัดการ Dead Letter Queue (DLQ) เพื่อจัดการ Message ที่ Process ไม่สำเร็จ
- เข้าใจ SQS Visibility Timeout และ Retry Mechanism

---

## 📖 ความรู้พื้นฐาน (Lecture — 30 นาที)

### ทำไมต้องมี Queue?

ลองนึกถึงสถานการณ์นี้: Upload ไฟล์ 500 ไฟล์พร้อมกัน Lambda Validator ถูก Trigger 500 ครั้งพร้อมกัน ทุกตัวพยายามเรียก Service ถัดไปพร้อมกัน → Service ถัดไปรับไม่ไหว → ระบบล่ม

**SQS แก้ปัญหานี้ด้วย:**
```
500 files uploaded → [SQS Queue] → Consumer Lambda อ่านทีละ 10 messages
                                    → ค่อยๆ ประมวลผลตามความสามารถ
                                    → ไม่ overflow ระบบถัดไป
```

### Standard Queue vs FIFO Queue

| | Standard Queue | FIFO Queue |
|---|---|---|
| Ordering | Best-effort (ไม่รับประกัน) | รับประกัน First-In-First-Out |
| Throughput | Unlimited | 300–3,000 msg/sec |
| Delivery | At least once (อาจ duplicate) | Exactly once |
| ราคา | ถูกกว่า | แพงกว่าเล็กน้อย |
| ใช้เมื่อ | ประมวลผลลำดับไม่สำคัญ | ต้องรักษาลำดับ |

> สำหรับ Project นี้ใช้ **Standard Queue** เพราะเราจะทำ Idempotent Processing

### Dead Letter Queue (DLQ) คืออะไร?

เมื่อ Consumer Lambda ประมวลผล Message ล้มเหลวซ้ำๆ (เกิน maxReceiveCount) SQS จะย้าย Message นั้นไปยัง DLQ แทนที่จะทิ้ง ทำให้เราสามารถ:
- Debug ว่า Message ไหนมีปัญหา
- ส่งไปประมวลผลใหม่ทีหลัง
- แจ้งเตือน Operator เมื่อมี Message ค้างใน DLQ

### Architecture ที่จะสร้างใน Week 2

```
[S3 Event] → [Lambda: csv-validator] → [SQS: main-queue]
                                               │
                                   SQS Trigger (Batch)
                                               │
                                               ▼
                                    [Lambda: csv-processor]
                                       - Parse CSV
                                       - คำนวณ Summary
                                       - Save ไปยัง S3 processed/
                                               │
                                     (ถ้า Error > 3 ครั้ง)
                                               ▼
                                    [SQS: dead-letter-queue]
```

---

## 🔧 LAB Step-by-Step

---

### ✅ STEP 1 — สร้าง Dead Letter Queue ก่อน

เสมอสร้าง DLQ ก่อน Main Queue:

1. เข้า **SQS** → **Create queue**
2. กรอกข้อมูล:
   ```
   Type: Standard
   Name: pipeline-dlq
   
   Configuration:
   Visibility timeout: 30 seconds
   Message retention period: 14 days   ← เก็บนาน เผื่อ Debug
   Maximum message size: 256 KB
   Delivery delay: 0
   ```
3. กด **Create queue**
4. จด **Queue ARN** ไว้ใช้ต่อ (รูปแบบ: `arn:aws:sqs:ap-southeast-1:123456789:pipeline-dlq`)

---

### ✅ STEP 2 — สร้าง Main Queue

1. กด **Create queue** อีกครั้ง
2. กรอกข้อมูล:
   ```
   Type: Standard
   Name: pipeline-main-queue
   
   Configuration:
   Visibility timeout: 60 seconds      ← ต้องมากกว่า Lambda timeout
   Message retention period: 4 days
   Maximum message size: 256 KB
   Delivery delay: 0
   Receive message wait time: 20 seconds  ← Long Polling ประหยัด Cost
   ```
3. **Dead-letter queue section:**
   - Enabled: ✅
   - Dead-letter queue: เลือก `pipeline-dlq`
   - Maximum receives: `3` (ลองใหม่ 3 ครั้งแล้วค่อยส่ง DLQ)
4. กด **Create queue**

> 💡 **Long Polling คืออะไร?** แทนที่ SQS จะตอบกลับทันทีว่า "ไม่มี Message" (Short Polling → เสียเงินแต่เปล่า) Long Polling จะรอนานสูงสุด 20 วินาทีก่อนตอบ — ลดค่าใช้จ่ายได้มาก

---

### ✅ STEP 3 — อัปเดต IAM Policy

Lambda ต้องมีสิทธิ์ส่ง/รับ Message จาก SQS:

1. เข้า **IAM** → **Policies** → ค้นหา `pipeline-lambda-policy` → **Edit**
2. เพิ่ม Statement ใหม่เข้าไปใน JSON:

```json
{
  "Sid": "SQSPermissions",
  "Effect": "Allow",
  "Action": [
    "sqs:SendMessage",
    "sqs:ReceiveMessage",
    "sqs:DeleteMessage",
    "sqs:GetQueueAttributes",
    "sqs:ChangeMessageVisibility"
  ],
  "Resource": [
    "arn:aws:sqs:ap-southeast-1:[ACCOUNT-ID]:pipeline-main-queue",
    "arn:aws:sqs:ap-southeast-1:[ACCOUNT-ID]:pipeline-dlq"
  ]
}
```

3. กด **Save changes**

---

### ✅ STEP 4 — อัปเดต Lambda Validator ให้ส่ง Message ไป SQS

แก้ไข `csv-validator` Lambda:

```python
import json
import boto3
import csv
import io
import logging
from datetime import datetime

logger = logging.getLogger()
logger.setLevel(logging.INFO)

s3 = boto3.client('s3')
sqs = boto3.client('sqs', region_name='ap-southeast-1')

# ใส่ Queue URL ของคุณ
QUEUE_URL = 'https://sqs.ap-southeast-1.amazonaws.com/[ACCOUNT-ID]/pipeline-main-queue'
PROCESSED_BUCKET = 'pipeline-processed-[ชื่อคุณ]-[random]'

def lambda_handler(event, context):
    logger.info(f"Received {len(event['Records'])} S3 event(s)")
    
    results = []
    
    for record in event['Records']:
        bucket_name = record['s3']['bucket']['name']
        object_key = record['s3']['object']['key']
        file_size = record['s3']['object']['size']
        
        # ตรวจสอบนามสกุล
        if not object_key.lower().endswith('.csv'):
            logger.warning(f"Skipping non-CSV file: {object_key}")
            continue
        
        try:
            # อ่านและตรวจสอบไฟล์
            response = s3.get_object(Bucket=bucket_name, Key=object_key)
            content = response['Body'].read().decode('utf-8')
            
            csv_reader = csv.DictReader(io.StringIO(content))
            rows = list(csv_reader)
            headers = list(csv_reader.fieldnames) if csv_reader.fieldnames else []
            
            if len(rows) == 0:
                logger.warning(f"Empty file: {object_key}")
                continue
            
            # สร้าง Message สำหรับ SQS
            message = {
                "job_id": f"job-{datetime.now().strftime('%Y%m%d%H%M%S')}-{object_key.split('/')[-1]}",
                "source_bucket": bucket_name,
                "source_key": object_key,
                "destination_bucket": PROCESSED_BUCKET,
                "file_size_bytes": file_size,
                "row_count": len(rows),
                "headers": headers,
                "submitted_at": datetime.now().isoformat()
            }
            
            # ส่ง Message ไป SQS
            sqs_response = sqs.send_message(
                QueueUrl=QUEUE_URL,
                MessageBody=json.dumps(message),
                MessageAttributes={
                    'job_type': {
                        'DataType': 'String',
                        'StringValue': 'csv_processing'
                    }
                }
            )
            
            logger.info(json.dumps({
                "event": "message_queued",
                "job_id": message["job_id"],
                "message_id": sqs_response['MessageId'],
                "file": object_key,
                "rows": len(rows)
            }))
            
            results.append({
                "file": object_key,
                "status": "queued",
                "job_id": message["job_id"],
                "message_id": sqs_response['MessageId']
            })
            
        except Exception as e:
            logger.error(json.dumps({
                "event": "error",
                "file": object_key,
                "error": str(e),
                "error_type": type(e).__name__
            }))
            results.append({"file": object_key, "status": "error", "reason": str(e)})
    
    return {"statusCode": 200, "body": json.dumps({"results": results})}
```

กด **Deploy**

---

### ✅ STEP 5 — สร้าง Lambda Consumer (csv-processor)

1. **Lambda** → **Create function**
2. กรอกข้อมูล:
   ```
   Function name: csv-processor
   Runtime: Python 3.12
   Execution role: pipeline-lambda-role
   ```
3. วางโค้ด:

```python
import json
import boto3
import csv
import io
import logging
from datetime import datetime
from collections import defaultdict

logger = logging.getLogger()
logger.setLevel(logging.INFO)

s3 = boto3.client('s3')

def lambda_handler(event, context):
    """
    Consumer Lambda — อ่าน Message จาก SQS และประมวลผล CSV
    """
    logger.info(f"Processing {len(event['Records'])} SQS message(s)")
    
    processed = []
    failed = []
    
    for record in event['Records']:
        message_id = record['messageId']
        receipt_handle = record['receiptHandle']
        
        try:
            body = json.loads(record['body'])
            job_id = body['job_id']
            source_bucket = body['source_bucket']
            source_key = body['source_key']
            dest_bucket = body['destination_bucket']
            
            logger.info(json.dumps({
                "event": "processing_started",
                "job_id": job_id,
                "message_id": message_id
            }))
            
            # ดาวน์โหลดไฟล์จาก S3
            response = s3.get_object(Bucket=source_bucket, Key=source_key)
            content = response['Body'].read().decode('utf-8')
            
            # Parse CSV
            csv_reader = csv.DictReader(io.StringIO(content))
            rows = list(csv_reader)
            
            # ประมวลผล: คำนวณ Summary Statistics
            summary = calculate_summary(rows, job_id, source_key)
            
            # บันทึกผลลัพธ์ไปยัง S3
            filename = source_key.split('/')[-1].replace('.csv', '')
            output_key = f"processed/{datetime.now().strftime('%Y/%m/%d')}/{filename}_summary.json"
            
            s3.put_object(
                Bucket=dest_bucket,
                Key=output_key,
                Body=json.dumps(summary, ensure_ascii=False, indent=2),
                ContentType='application/json'
            )
            
            logger.info(json.dumps({
                "event": "processing_complete",
                "job_id": job_id,
                "output_key": output_key,
                "total_rows": summary['total_rows'],
                "total_revenue": summary.get('total_revenue', 0)
            }))
            
            processed.append(job_id)
            
        except Exception as e:
            logger.error(json.dumps({
                "event": "processing_failed",
                "message_id": message_id,
                "error": str(e),
                "error_type": type(e).__name__
            }))
            # ถ้า raise Exception → SQS จะ retry และส่ง DLQ หลัง 3 ครั้ง
            failed.append(message_id)
            raise  # Re-raise เพื่อให้ SQS รู้ว่า Message ยังไม่ได้ถูก Process สำเร็จ
    
    logger.info(f"Batch complete: {len(processed)} processed, {len(failed)} failed")
    
    return {
        "batchItemFailures": [
            {"itemIdentifier": mid} for mid in failed
        ]
    }


def calculate_summary(rows, job_id, source_key):
    """คำนวณ Summary Statistics จาก CSV rows"""
    
    if not rows:
        return {"job_id": job_id, "source": source_key, "total_rows": 0}
    
    summary = {
        "job_id": job_id,
        "source_file": source_key,
        "processed_at": datetime.now().isoformat(),
        "total_rows": len(rows),
        "columns": list(rows[0].keys())
    }
    
    # ถ้ามี Column ตัวเลข ลองคำนวณ Stats
    numeric_columns = {}
    for col in rows[0].keys():
        try:
            values = [float(row[col]) for row in rows if row[col]]
            if values:
                numeric_columns[col] = {
                    "min": min(values),
                    "max": max(values),
                    "sum": round(sum(values), 2),
                    "avg": round(sum(values) / len(values), 2),
                    "count": len(values)
                }
        except (ValueError, TypeError):
            pass  # ไม่ใช่ตัวเลข ข้ามไป
    
    if numeric_columns:
        summary["numeric_stats"] = numeric_columns
    
    # นับค่าซ้ำในแต่ละ Column (สำหรับ Categorical)
    categorical_stats = {}
    for col in rows[0].keys():
        if col not in numeric_columns:
            counts = defaultdict(int)
            for row in rows:
                counts[row[col]] += 1
            categorical_stats[col] = dict(counts)
    
    if categorical_stats:
        summary["categorical_stats"] = categorical_stats
    
    return summary
```

4. ตั้งค่า:
   - Timeout: **60 seconds**
   - Memory: **256 MB**
5. กด **Deploy**

---

### ✅ STEP 6 — เชื่อม SQS กับ Lambda Consumer

1. ใน Lambda `csv-processor` → **Configuration** → **Triggers** → **Add trigger**
2. เลือก **SQS**
3. กรอกข้อมูล:
   ```
   SQS queue: pipeline-main-queue
   Batch size: 5               ← อ่านครั้งละ 5 messages
   Batch window: 10 seconds    ← รอสะสม messages สูงสุด 10 วินาที
   Report batch item failures: ✅ Enable
   ```
4. กด **Add**

> 💡 **Batch Item Failures คืออะไร?** แทนที่ถ้า Message ใดใน Batch ล้มเหลวจะ retry ทั้ง Batch ใหม่หมด เราส่งกลับเฉพาะ Message ID ที่ล้มเหลว SQS จะ retry เฉพาะอัน นั้น ประหยัดมาก

---

### ✅ STEP 7 — ทดสอบ End-to-End Pipeline

1. **อัปโหลด** `sample_sales.csv` ไปยัง `uploads/` ใน S3 Bucket แรก
2. **ตรวจสอบ** SQS Console → `pipeline-main-queue` → Messages available จะขึ้นชั่วคราวแล้วหายไป
3. **ตรวจสอบ** CloudWatch Logs:
   - `/aws/lambda/csv-validator` → ควรเห็น `"event": "message_queued"`
   - `/aws/lambda/csv-processor` → ควรเห็น `"event": "processing_complete"`
4. **ตรวจสอบ** S3 `pipeline-processed-...` → เข้า folder `processed/` → ควรเห็นไฟล์ `..._summary.json`
5. ดาวน์โหลดไฟล์ JSON มาดูผลลัพธ์

---

### ✅ STEP 8 — ทดสอบ Dead Letter Queue

ทดสอบว่า DLQ ทำงานถูกต้อง:

1. แก้ `csv-processor` ให้ Raise Error เสมอชั่วคราว:
```python
def lambda_handler(event, context):
    raise Exception("Simulated failure for DLQ testing")
```
2. Deploy และอัปโหลดไฟล์ CSV ใหม่
3. รอประมาณ 2–3 นาที (SQS จะ retry 3 ครั้งตาม maxReceiveCount)
4. เข้า SQS → `pipeline-dlq` → **Messages available** ควรเพิ่มขึ้น
5. กด **Send and receive messages** → **Poll for messages** → ดูเนื้อหา Message
6. แก้โค้ด Lambda กลับเป็นปกติแล้ว Deploy

---

### 📝 แบบฝึกหัดเพิ่มเติม Week 2

1. **เพิ่ม CloudWatch Alarm** แจ้งเตือนเมื่อ `pipeline-dlq` มี Message มากกว่า 0 (แสดงว่ามี Processing Error)
2. **ทดสอบ High Volume:** เขียน Script อัปโหลด CSV 20 ไฟล์พร้อมกัน ดูว่า SQS จัดการ Queue อย่างไร
3. **เพิ่ม Message Deduplication ID:** แก้โค้ดให้ไม่ประมวลผลไฟล์เดิมซ้ำ (Idempotency Key)

### ❓ คำถามท้าย LAB Week 2

1. ถ้าตั้ง Visibility Timeout สั้นกว่า Lambda Timeout จะเกิดอะไรขึ้น?
2. SQS Standard Queue อาจ Deliver Message มากกว่า 1 ครั้ง — เราออกแบบ `csv-processor` ให้รองรับกรณีนี้ได้ยังไง? (Hint: ดูที่ output_key)
3. Long Polling กับ Short Polling ต่างกันยังไงในแง่ Cost และ Latency?

---

---

# 📅 WEEK 3 — Orchestration with Step Functions

> **หัวข้อ:** แทนที่ Chain Lambda ตรงๆ ด้วย State Machine ที่ดูแลได้ง่าย

---

## 🎓 วัตถุประสงค์การเรียนรู้
- อธิบาย Orchestration vs Choreography ใน Microservices ได้
- สร้าง Step Functions State Machine ด้วย Amazon States Language (ASL)
- เชื่อม Lambda หลายตัวเข้า Workflow ที่มี Error Handling
- ใช้ Parallel State และ Choice State
- Monitor Execution History ใน Step Functions Console

---

## 📖 ความรู้พื้นฐาน (Lecture — 30 นาที)

### Orchestration vs Choreography

**Choreography (แบบที่ทำใน Week 1–2):**
```
Lambda A ────ส่ง Event────> SQS ────trigger────> Lambda B
Lambda B ────ส่ง Event────> SNS ────trigger────> Lambda C
```
- แต่ละ Service รู้จักกันน้อยที่สุด
- ยากที่จะ Debug เมื่อมีปัญหา ("ไฟล่องหนไปไหน?")
- ไม่มีที่เดียวที่เห็น Flow ทั้งหมด

**Orchestration (Step Functions):**
```
Step Functions ──────────> Lambda A
              ──────────> Lambda B (ถ้า A สำเร็จ)
              ──────────> Lambda C (ถ้า B สำเร็จ)
              ──Error───> Notify (ถ้ามี Error)
```
- มีที่เดียวที่ควบคุม Flow ทั้งหมด
- เห็น Visual Diagram และ Execution History
- Error Handling และ Retry ในที่เดียว
- Timeout แต่ละ Step ได้

### Amazon States Language (ASL)

ASL เป็น JSON-based Language สำหรับกำหนด State Machine:

```json
{
  "Comment": "ตัวอย่าง State Machine",
  "StartAt": "Step1",
  "States": {
    "Step1": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:...:function:my-lambda",
      "Next": "Step2",
      "Catch": [
        {
          "ErrorEquals": ["States.ALL"],
          "Next": "HandleError"
        }
      ]
    },
    "Step2": {
      "Type": "Task",
      "Resource": "...",
      "End": true
    },
    "HandleError": {
      "Type": "Fail",
      "Error": "ProcessingFailed"
    }
  }
}
```

### State Types ที่สำคัญ

| State Type | ใช้ทำอะไร | ตัวอย่าง |
|-----------|-----------|---------|
| Task | เรียก Lambda / Service | ประมวลผลไฟล์ |
| Choice | แยกเส้นทางตามเงื่อนไข | ถ้า rows > 1000 ทำ A ไม่งั้นทำ B |
| Parallel | ทำหลาย Tasks พร้อมกัน | Transform + Validate พร้อมกัน |
| Wait | รอเวลา | รอ 5 นาทีก่อน Retry |
| Succeed | จบสำเร็จ | End State |
| Fail | จบแบบ Error | Error State |
| Pass | ส่งต่อข้อมูลโดยไม่ทำอะไร | Debug / Testing |

### Architecture ที่จะสร้างใน Week 3

```
[SQS Consumer Lambda] ─starts─> [Step Functions: ProcessCSVWorkflow]
                                          │
                            ┌─────────────┼─────────────┐
                            ▼             ▼             ▼
                      [Parse CSV]  [Validate Schema] [Check Size]
                      (Parallel States — ทำพร้อมกัน)
                            │
                            ▼
                      [Choice: Valid?]
                         /         \
                    Yes              No
                     │               │
              [Transform Data]  [Move to failed/]
                     │
                     ▼
               [Save Results]
                     │
                     ▼
                [Notify SNS]   ← จะทำใน Week 4
                     │
                     ▼
                  [Success]
```

---

## 🔧 LAB Step-by-Step

---

### ✅ STEP 1 — สร้าง Lambda Functions สำหรับแต่ละ Step

เราจะสร้าง Lambda 4 ตัวแยกกัน แต่ละตัวทำหน้าที่เดียว (Single Responsibility):

**Lambda 1: parse-csv**

1. **Lambda** → **Create function** → `parse-csv` → Python 3.12 → `pipeline-lambda-role`

```python
import json
import boto3
import csv
import io
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)
s3 = boto3.client('s3')

def lambda_handler(event, context):
    """
    Step 1: อ่านและ Parse ไฟล์ CSV จาก S3
    Input: {"source_bucket": "...", "source_key": "...", "job_id": "..."}
    Output: เพิ่ม rows และ headers เข้าไปใน event
    """
    source_bucket = event['source_bucket']
    source_key = event['source_key']
    job_id = event['job_id']
    
    logger.info(f"Parsing {source_key} for job {job_id}")
    
    response = s3.get_object(Bucket=source_bucket, Key=source_key)
    content = response['Body'].read().decode('utf-8')
    
    csv_reader = csv.DictReader(io.StringIO(content))
    rows = list(csv_reader)
    headers = list(csv_reader.fieldnames) if csv_reader.fieldnames else []
    
    logger.info(f"Parsed {len(rows)} rows, {len(headers)} columns")
    
    # ส่งต่อข้อมูลไปยัง Step ถัดไป
    return {
        **event,  # ส่งข้อมูลเดิมต่อทั้งหมด
        "rows": rows,
        "headers": headers,
        "row_count": len(rows),
        "parse_status": "success"
    }
```

**Lambda 2: validate-schema**

1. สร้าง Lambda `validate-schema` → Python 3.12 → `pipeline-lambda-role`

```python
import json
import logging

logger = logging.getLogger()
logger.setLevel(logging.INFO)

# กำหนด Schema ที่ต้องการ
REQUIRED_COLUMNS = ['order_id', 'customer_name', 'product', 'quantity', 'price', 'date']

def lambda_handler(event, context):
    """
    Step 2: ตรวจสอบว่า CSV มี Column ครบถ้วนตาม Schema
    """
    headers = event.get('headers', [])
    job_id = event['job_id']
    
    missing_columns = [col for col in REQUIRED_COLUMNS if col not in headers]
    extra_columns = [col for col in headers if col not in REQUIRED_COLUMNS]
    
    is_valid = len(missing_columns) == 0
    
    logger.info(json.dumps({
        "job_id": job_id,
        "is_valid": is_valid,
        "missing_columns": missing_columns,
        "extra_columns": extra_columns,
        "headers_found": headers
    }))
    
    return {
        **event,
        "schema_valid": is_valid,
        "missing_columns": missing_columns,
        "extra_columns": extra_columns,
        "validation_status": "passed" if is_valid else "failed"
    }
```

**Lambda 3: transform-data**

1. สร้าง Lambda `transform-data` → Python 3.12 → `pipeline-lambda-role`

```python
import json
import boto3
import logging
from datetime import datetime
from collections import defaultdict

logger = logging.getLogger()
logger.setLevel(logging.INFO)
s3 = boto3.client('s3')

def lambda_handler(event, context):
    """
    Step 3: แปลงและวิเคราะห์ข้อมูล
    """
    rows = event['rows']
    job_id = event['job_id']
    dest_bucket = event['destination_bucket']
    source_key = event['source_key']
    
    logger.info(f"Transforming {len(rows)} rows for job {job_id}")
    
    # คำนวณ Revenue
    total_revenue = 0
    product_summary = defaultdict(lambda: {"quantity": 0, "revenue": 0, "orders": 0})
    
    transformed_rows = []
    for row in rows:
        try:
            qty = float(row.get('quantity', 0))
            price = float(row.get('price', 0))
            revenue = qty * price
            total_revenue += revenue
            
            product = row.get('product', 'Unknown')
            product_summary[product]['quantity'] += qty
            product_summary[product]['revenue'] += revenue
            product_summary[product]['orders'] += 1
            
            transformed_rows.append({
                **row,
                'revenue': round(revenue, 2),
                'processed_at': datetime.now().isoformat()
            })
        except (ValueError, TypeError) as e:
            logger.warning(f"Error processing row {row}: {e}")
    
    result = {
        "job_id": job_id,
        "source_file": source_key,
        "processed_at": datetime.now().isoformat(),
        "summary": {
            "total_rows": len(rows),
            "total_revenue": round(total_revenue, 2),
            "average_order_value": round(total_revenue / len(rows), 2) if rows else 0,
            "product_breakdown": {k: {**v, "revenue": round(v["revenue"], 2)} 
                                  for k, v in product_summary.items()}
        },
        "data": transformed_rows
    }
    
    # บันทึกไปยัง S3
    filename = source_key.split('/')[-1].replace('.csv', '')
    output_key = f"processed/{datetime.now().strftime('%Y/%m/%d')}/{filename}_result.json"
    
    s3.put_object(
        Bucket=dest_bucket,
        Key=output_key,
        Body=json.dumps(result, ensure_ascii=False, indent=2),
        ContentType='application/json'
    )
    
    logger.info(json.dumps({
        "event": "transform_complete",
        "job_id": job_id,
        "total_revenue": result['summary']['total_revenue'],
        "output_key": output_key
    }))
    
    return {
        **event,
        "transform_status": "success",
        "output_key": output_key,
        "total_revenue": result['summary']['total_revenue'],
        "summary": result['summary']
    }
```

**Lambda 4: move-to-failed**

1. สร้าง Lambda `move-to-failed` → Python 3.12 → `pipeline-lambda-role`

```python
import json
import boto3
import logging
from datetime import datetime

logger = logging.getLogger()
logger.setLevel(logging.INFO)
s3 = boto3.client('s3')

def lambda_handler(event, context):
    """
    เมื่อ Schema Invalid — ย้ายไฟล์ไปยัง failed/ folder พร้อม error log
    """
    source_bucket = event['source_bucket']
    source_key = event['source_key']
    job_id = event['job_id']
    missing_columns = event.get('missing_columns', [])
    
    # Copy ไปยัง failed/ folder
    filename = source_key.split('/')[-1]
    failed_key = f"failed/{datetime.now().strftime('%Y/%m/%d')}/{filename}"
    
    s3.copy_object(
        Bucket=source_bucket,
        CopySource={'Bucket': source_bucket, 'Key': source_key},
        Key=failed_key,
        Metadata={
            'job_id': job_id,
            'reason': f"Missing columns: {', '.join(missing_columns)}",
            'failed_at': datetime.now().isoformat()
        },
        MetadataDirective='REPLACE'
    )
    
    logger.warning(json.dumps({
        "event": "file_moved_to_failed",
        "job_id": job_id,
        "original_key": source_key,
        "failed_key": failed_key,
        "reason": f"Missing columns: {missing_columns}"
    }))
    
    return {
        **event,
        "failed_key": failed_key,
        "move_status": "success"
    }
```

Deploy ทุก Lambda

---

### ✅ STEP 2 — อัปเดต IAM Policy

Lambda ต้องมีสิทธิ์เรียก Step Functions และ Copy Object ใน S3:

เพิ่ม Statement ใน `pipeline-lambda-policy`:

```json
	{
			"Sid": "S3CopyObject",
			"Effect": "Allow",
			"Action": [
				"s3:*"
			],
  "Resource": "arn:aws:s3:::pipeline-raw-[ชื่อคุณ]-*/*"
},
{
  "Sid": "StepFunctionsStart",
  "Effect": "Allow",
  "Action": ["states:StartExecution"],
  "Resource": "*"
}
```

**สร้าง IAM Role สำหรับ Step Functions:**

1. **IAM** → **Roles** → **Create role**
2. Trusted entity: **AWS service** → เลื่อนลงหา **Step Functions** → Next
3. ค้นหา `AWSLambdaRole` (อนุญาตให้ Step Functions เรียก Lambda) → เพิ่ม
4. Role name: `pipeline-stepfunctions-role` → Create

---

### ✅ STEP 3 — สร้าง State Machine

1. เข้า **Step Functions** → **State machines** → **Create state machine**
2. เลือก **Write your workflow in code**
3. Type: **Standard** (Express เหมาะกับ High Volume / Short Duration)
4. วาง ASL JSON นี้:

```json
{
  "Comment": "CSV Processing Pipeline — Week 3 LAB",
  "StartAt": "ParseCSV",
  "States": {
    "ParseCSV": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:parse-csv",
      "TimeoutSeconds": 60,
      "Retry": [
        {
          "ErrorEquals": ["Lambda.ServiceException", "Lambda.AWSLambdaException", "Lambda.SdkClientException"],
          "IntervalSeconds": 2,
          "MaxAttempts": 3,
          "BackoffRate": 2
        }
      ],
      "Catch": [
        {
          "ErrorEquals": ["States.ALL"],
          "Next": "HandleError",
          "ResultPath": "$.error"
        }
      ],
      "Next": "ValidateSchema"
    },
    
    "ValidateSchema": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:validate-schema",
      "TimeoutSeconds": 30,
      "Catch": [
        {
          "ErrorEquals": ["States.ALL"],
          "Next": "HandleError",
          "ResultPath": "$.error"
        }
      ],
      "Next": "CheckValidation"
    },
    
    "CheckValidation": {
      "Type": "Choice",
      "Choices": [
        {
          "Variable": "$.schema_valid",
          "BooleanEquals": true,
          "Next": "TransformData"
        },
        {
          "Variable": "$.schema_valid",
          "BooleanEquals": false,
          "Next": "MoveToFailed"
        }
      ],
      "Default": "HandleError"
    },
    
    "TransformData": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:transform-data",
      "TimeoutSeconds": 120,
      "Retry": [
        {
          "ErrorEquals": ["States.ALL"],
          "IntervalSeconds": 5,
          "MaxAttempts": 2,
          "BackoffRate": 2
        }
      ],
      "Catch": [
        {
          "ErrorEquals": ["States.ALL"],
          "Next": "HandleError",
          "ResultPath": "$.error"
        }
      ],
      "Next": "ProcessingComplete"
    },
    
    "MoveToFailed": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:move-to-failed",
      "TimeoutSeconds": 30,
      "Next": "ValidationFailed"
    },
    
    "ProcessingComplete": {
      "Type": "Succeed",
      "Comment": "Pipeline completed successfully"
    },
    
    "ValidationFailed": {
      "Type": "Fail",
      "Error": "ValidationFailed",
      "Cause": "CSV schema validation failed — file moved to failed folder"
    },
    
    "HandleError": {
      "Type": "Fail",
      "Error": "ProcessingError",
      "Cause": "An error occurred during pipeline processing"
    }
  }
}
```

5. **แทนที่ `[ACCOUNT-ID]`** ด้วย AWS Account ID จริงของคุณ (หาได้จาก AWS Console บนขวา)
6. กด **Next** → State machine name: `ProcessCSVWorkflow`
7. Execution role: `pipeline-stepfunctions-role`
8. กด **Create state machine**

---

### ✅ STEP 4 — อัปเดต SQS Consumer ให้เริ่ม Step Functions

แก้ไข Lambda `csv-processor` (ที่สร้างใน Week 2) ให้ Start Step Functions Execution แทนการประมวลผลเอง:

```python
import json
import boto3
import logging
from datetime import datetime

logger = logging.getLogger()
logger.setLevel(logging.INFO)

sfn = boto3.client('stepfunctions', region_name='ap-southeast-1')

# ใส่ State Machine ARN ของคุณ
STATE_MACHINE_ARN = 'arn:aws:states:ap-southeast-1:[ACCOUNT-ID]:stateMachine:ProcessCSVWorkflow'

def lambda_handler(event, context):
    """
    อ่าน Message จาก SQS และเริ่ม Step Functions Execution
    """
    logger.info(f"Processing {len(event['Records'])} SQS message(s)")
    
    batch_failures = []
    
    for record in event['Records']:
        message_id = record['messageId']
        
        try:
            body = json.loads(record['body'])
            job_id = body['job_id']
            
            # เตรียม Input สำหรับ Step Functions
            sfn_input = {
                "job_id": job_id,
                "source_bucket": body['source_bucket'],
                "source_key": body['source_key'],
                "destination_bucket": body['destination_bucket'],
                "submitted_at": body['submitted_at'],
                "row_count_estimate": body.get('row_count', 0)
            }
            
            # Start Step Functions Execution
            response = sfn.start_execution(
                stateMachineArn=STATE_MACHINE_ARN,
                name=f"execution-{job_id}",  # ต้อง Unique
                input=json.dumps(sfn_input)
            )
            
            logger.info(json.dumps({
                "event": "execution_started",
                "job_id": job_id,
                "execution_arn": response['executionArn'],
                "message_id": message_id
            }))
            
        except Exception as e:
            logger.error(f"Failed to start execution for message {message_id}: {e}")
            batch_failures.append({"itemIdentifier": message_id})
    
    return {"batchItemFailures": batch_failures}
```

กด **Deploy**

---

### ✅ STEP 5 — ทดสอบ State Machine

**ทดสอบโดยตรงจาก Step Functions Console:**

1. เข้า **Step Functions** → `ProcessCSVWorkflow` → **Start execution**
2. Input:
```json
{
  "job_id": "test-job-001",
  "source_bucket": "pipeline-raw-[ชื่อคุณ]-[random]",
  "source_key": "uploads/sample_sales.csv",
  "destination_bucket": "pipeline-processed-[ชื่อคุณ]-[random]",
  "submitted_at": "2024-01-15T10:00:00"
}
```
3. กด **Start execution**

**ดู Visual Execution:**
- จะเห็น Diagram แสดง State ที่กำลัง Execute อยู่ (สีฟ้า = กำลังทำงาน, สีเขียว = สำเร็จ, สีแดง = ล้มเหลว)
- กดแต่ละ State เพื่อดู Input/Output

**ทดสอบ Validation Failed Path:**
1. สร้างไฟล์ `bad_schema.csv` ที่ไม่มี Column `order_id`:
```csv
name,product,qty,amount
Alice,Widget A,5,250
```
2. Upload ขึ้น S3 `uploads/`
3. Start execution ด้วย `source_key: "uploads/bad_schema.csv"`
4. สังเกต Flow จะไปเส้น `MoveToFailed` → `ValidationFailed`

---

### 📝 แบบฝึกหัดเพิ่มเติม Week 3

1. **เพิ่ม Parallel State:** รัน `validate-schema` และ **ตรวจสอบ File Size** พร้อมกัน (สร้าง Lambda `check-file-size` ง่ายๆ)
2. **เพิ่ม Wait State:** ถ้า File Size > 1 MB ให้รอ 30 วินาทีก่อน Transform (จำลอง Rate Limiting)
3. **Map State:** ถ้า CSV มีหลาย Products ให้ประมวลผลแต่ละ Product แบบ Parallel ด้วย Map State

### ❓ คำถามท้าย LAB Week 3

1. Standard Workflow กับ Express Workflow ใน Step Functions ต่างกันยังไง? เลือกใช้อะไรเมื่อไหร่?
2. Retry ใน ASL ทำงานยังไง? `BackoffRate: 2` หมายความว่าอะไร?
3. ถ้า Execution หนึ่งใช้เวลานานมาก จะ Cancel ได้ยังไง? มี Side Effects อะไรบ้าง?

---

---

# 📅 WEEK 4 — Notification & Recap

> **หัวข้อ:** เพิ่ม SNS แจ้งเตือน + CloudWatch Dashboard + สรุป Architecture และ Cost

---

## 🎓 วัตถุประสงค์การเรียนรู้
- สร้าง SNS Topic และส่ง Email/SMS Notification
- เชื่อม SNS เข้ากับ Step Functions (จบ Pipeline ด้วยการแจ้งเตือน)
- สร้าง CloudWatch Dashboard แสดง Metrics ของทุก Service
- ตั้ง CloudWatch Alarm แจ้งเตือนเมื่อมี Pipeline Failure
- วิเคราะห์ Architecture ทั้งหมดและ Cost Estimation

---

## 📖 ความรู้พื้นฐาน (Lecture — 20 นาที)

### Amazon SNS (Simple Notification Service) คืออะไร?

SNS เป็น Pub/Sub Messaging Service — ผู้ส่ง (Publisher) ส่ง Message ไปยัง Topic โดยไม่รู้ว่าใครรับ ผู้รับ (Subscriber) รับ Message จาก Topic ที่ Subscribe ไว้

```
[Lambda ส่งผล] ──publish──> [SNS Topic: pipeline-notifications]
                                          │
                         ┌────────────────┼────────────────┐
                         ▼                ▼                ▼
                    [Email Sub]     [SMS Sub]      [Lambda Sub]
                  (ส่ง Email)      (ส่ง SMS)     (trigger อื่น)
```

**SNS vs SQS:**
| | SNS | SQS |
|---|---|---|
| Pattern | Push (Pub/Sub) | Pull (Queue) |
| Delivery | Fan-out (ทุก Subscriber) | One consumer per message |
| Retention | ไม่เก็บ | เก็บตามที่ตั้งค่า |
| Use case | Notification, Fan-out | Work Queue, Decoupling |

### Architecture ที่จะสร้างใน Week 4

```
[Step Functions: TransformData] 
              │
              ▼
     [Lambda: send-notification]
              │
              ▼
       [SNS Topic: pipeline-notifications]
         │              │
         ▼              ▼
      [Email]         [SQS]  ← สำหรับ Integration อื่นๆ ในอนาคต

[CloudWatch] ──── Monitor ────> ทุก Service ใน Pipeline
                                 + Dashboard + Alarms
```

---

## 🔧 LAB Step-by-Step

---

### ✅ STEP 1 — สร้าง SNS Topic

1. เข้า **SNS** → **Topics** → **Create topic**
2. กรอกข้อมูล:
   ```
   Type: Standard
   Name: pipeline-notifications
   Display name: CSV Pipeline
   ```
3. กด **Create topic**
4. จด **Topic ARN** ไว้ (รูปแบบ: `arn:aws:sns:ap-southeast-1:...:pipeline-notifications`)

**สร้าง Email Subscription:**
1. กด Topic ที่สร้าง → **Create subscription**
2. กรอก:
   ```
   Protocol: Email
   Endpoint: [ใส่ Email ของคุณ]
   ```
3. กด **Create subscription**
4. เช็ค Email → กด **Confirm subscription** ใน Email ที่ได้รับ
5. กลับมาที่ SNS Console → Status ควรเปลี่ยนเป็น `Confirmed`

---

### ✅ STEP 2 — อัปเดต IAM Policy เพิ่ม SNS

เพิ่มใน `pipeline-lambda-policy`:

```json
{
  "Sid": "SNSPublish",
  "Effect": "Allow",
  "Action": ["sns:Publish"],
  "Resource": "arn:aws:sns:ap-southeast-1:[ACCOUNT-ID]:pipeline-notifications"
}
```

---

### ✅ STEP 3 — สร้าง Lambda Notification

1. **Lambda** → **Create function** → `send-notification` → Python 3.12 → `pipeline-lambda-role`

```python
import json
import boto3
import logging
from datetime import datetime

logger = logging.getLogger()
logger.setLevel(logging.INFO)

sns = boto3.client('sns', region_name='ap-southeast-1')

SNS_TOPIC_ARN = 'arn:aws:sns:ap-southeast-1:[ACCOUNT-ID]:pipeline-notifications'

def lambda_handler(event, context):
    """
    ส่ง Notification เมื่อ Pipeline เสร็จสิ้น (สำเร็จหรือล้มเหลว)
    """
    job_id = event.get('job_id', 'unknown')
    status = event.get('transform_status', event.get('move_status', 'unknown'))
    source_key = event.get('source_key', 'unknown')
    summary = event.get('summary', {})
    
    is_success = status == 'success'
    
    # สร้าง Message
    if is_success:
        subject = f"✅ Pipeline สำเร็จ — {source_key.split('/')[-1]}"
        message = build_success_message(job_id, source_key, summary, event)
    else:
        subject = f"❌ Pipeline ล้มเหลว — {source_key.split('/')[-1]}"
        message = build_failure_message(job_id, source_key, event)
    
    # ส่ง SNS
    response = sns.publish(
        TopicArn=SNS_TOPIC_ARN,
        Subject=subject[:100],  # Subject จำกัด 100 ตัวอักษร
        Message=message,
        MessageAttributes={
            'job_id': {'DataType': 'String', 'StringValue': job_id},
            'status': {'DataType': 'String', 'StringValue': 'success' if is_success else 'failed'}
        }
    )
    
    logger.info(json.dumps({
        "event": "notification_sent",
        "job_id": job_id,
        "status": "success" if is_success else "failed",
        "message_id": response['MessageId']
    }))
    
    return {
        **event,
        "notification_status": "sent",
        "notification_message_id": response['MessageId']
    }


def build_success_message(job_id, source_key, summary, event):
    filename = source_key.split('/')[-1]
    total_rows = summary.get('total_rows', event.get('row_count', 0))
    total_revenue = summary.get('total_revenue', 0)
    output_key = event.get('output_key', 'N/A')
    
    return f"""
🎉 CSV Pipeline ประมวลผลสำเร็จ!
{'='*50}

📁 ไฟล์ที่ประมวลผล: {filename}
🆔 Job ID: {job_id}
⏰ เสร็จเมื่อ: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')} UTC

📊 สรุปผลลัพธ์:
   - จำนวนแถว: {total_rows:,} แถว
   - รายได้รวม: {total_revenue:,.2f} บาท

💾 ผลลัพธ์บันทึกที่:
   {output_key}

---
AWS Data Pipeline Notification
    """.strip()


def build_failure_message(job_id, source_key, event):
    filename = source_key.split('/')[-1]
    missing_cols = event.get('missing_columns', [])
    failed_key = event.get('failed_key', 'N/A')
    
    return f"""
⚠️ CSV Pipeline พบปัญหา

📁 ไฟล์: {filename}
🆔 Job ID: {job_id}
⏰ เวลา: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')} UTC

❌ สาเหตุ: Schema ไม่ตรงตามที่กำหนด
   Column ที่ขาดหาย: {', '.join(missing_cols) if missing_cols else 'N/A'}

📂 ไฟล์ถูกย้ายไปที่: {failed_key}

---
กรุณาตรวจสอบและแก้ไขไฟล์ก่อนอัปโหลดใหม่
AWS Data Pipeline Notification
    """.strip()
```

กด **Deploy**

---

### ✅ STEP 4 — อัปเดต State Machine เพิ่ม Notification Step

แก้ไข State Machine `ProcessCSVWorkflow` — เพิ่ม `SendNotification` และ `SendFailureNotification`:

1. เข้า **Step Functions** → `ProcessCSVWorkflow` → **Edit**
2. แทนที่ ASL ด้วยเวอร์ชันใหม่:

```json
{
  "Comment": "CSV Processing Pipeline — Week 4 (with Notifications)",
  "StartAt": "ParseCSV",
  "States": {
    "ParseCSV": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:parse-csv",
      "TimeoutSeconds": 60,
      "Retry": [
        {
          "ErrorEquals": ["Lambda.ServiceException", "Lambda.AWSLambdaException"],
          "IntervalSeconds": 2,
          "MaxAttempts": 3,
          "BackoffRate": 2
        }
      ],
      "Catch": [
        {
          "ErrorEquals": ["States.ALL"],
          "Next": "HandleError",
          "ResultPath": "$.error"
        }
      ],
      "Next": "ValidateSchema"
    },

    "ValidateSchema": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:validate-schema",
      "TimeoutSeconds": 30,
      "Catch": [
        {
          "ErrorEquals": ["States.ALL"],
          "Next": "HandleError",
          "ResultPath": "$.error"
        }
      ],
      "Next": "CheckValidation"
    },

    "CheckValidation": {
      "Type": "Choice",
      "Choices": [
        {
          "Variable": "$.schema_valid",
          "BooleanEquals": true,
          "Next": "TransformData"
        },
        {
          "Variable": "$.schema_valid",
          "BooleanEquals": false,
          "Next": "MoveToFailed"
        }
      ],
      "Default": "HandleError"
    },

    "TransformData": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:transform-data",
      "TimeoutSeconds": 120,
      "Retry": [
        {
          "ErrorEquals": ["States.ALL"],
          "IntervalSeconds": 5,
          "MaxAttempts": 2,
          "BackoffRate": 2
        }
      ],
      "Catch": [
        {
          "ErrorEquals": ["States.ALL"],
          "Next": "HandleError",
          "ResultPath": "$.error"
        }
      ],
      "Next": "SendSuccessNotification"
    },

    "SendSuccessNotification": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:send-notification",
      "TimeoutSeconds": 30,
      "Next": "ProcessingComplete"
    },

    "MoveToFailed": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:move-to-failed",
      "TimeoutSeconds": 30,
      "Next": "SendFailureNotification"
    },

    "SendFailureNotification": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:send-notification",
      "TimeoutSeconds": 30,
      "Next": "ValidationFailed"
    },

    "ProcessingComplete": {
      "Type": "Succeed"
    },

    "ValidationFailed": {
      "Type": "Fail",
      "Error": "ValidationFailed",
      "Cause": "Schema validation failed"
    },

    "HandleError": {
      "Type": "Fail",
      "Error": "ProcessingError",
      "Cause": "Unexpected error during pipeline processing"
    }
  }
}
```

3. กด **Save** → **Save anyway** (ถ้ามี warning)

---

### ✅ STEP 5 — สร้าง CloudWatch Dashboard

1. เข้า **CloudWatch** → **Dashboards** → **Create dashboard**
2. Name: `csv-pipeline-dashboard` → **Create dashboard**
3. เพิ่ม Widgets ตามลำดับ:

**Widget 1: Lambda Invocations Overview (Line Chart)**
- Add widget → Line
- Metric: Lambda → By Function Name
- เลือก: `csv-validator`, `csv-processor`, `parse-csv`, `transform-data`, `send-notification`
- Metric name: Invocations
- Title: "Lambda Invocations"

**Widget 2: Lambda Errors (Line Chart)**
- เหมือนกัน แต่ Metric: Errors
- Title: "Lambda Errors"

**Widget 3: SQS Queue Depth (Line Chart)**
- Metric: SQS → ApproximateNumberOfMessagesVisible
- Queue: pipeline-main-queue
- Title: "SQS Queue Depth"

**Widget 4: DLQ Messages (Number)**
- Metric: SQS → ApproximateNumberOfMessagesVisible
- Queue: pipeline-dlq
- Title: "Dead Letter Queue"

**Widget 5: Step Functions Executions (Line Chart)**
- Metric: Step Functions → ExecutionsStarted, ExecutionsSucceeded, ExecutionsFailed
- Title: "Step Functions Executions"

4. กด **Save dashboard**

---

### ✅ STEP 6 — ตั้ง CloudWatch Alarms

**Alarm 1: Lambda Error Rate สูง**

1. **CloudWatch** → **Alarms** → **Create alarm**
2. Select metric → Lambda → By Function Name → `transform-data` → Errors
3. กำหนด:
   ```
   Statistic: Sum
   Period: 5 minutes
   Threshold: Greater than 2
   Datapoints to alarm: 1 out of 1
   ```
4. Notification: ส่งไป SNS Topic `pipeline-notifications`
5. Alarm name: `pipeline-transform-errors`

**Alarm 2: DLQ มี Messages**

1. Create alarm → SQS → `pipeline-dlq` → ApproximateNumberOfMessagesVisible
2. กำหนด:
   ```
   Statistic: Maximum
   Period: 1 minute  
   Threshold: Greater than 0
   ```
3. Notification: ส่งไป SNS Topic เดิม
4. Alarm name: `pipeline-dlq-messages`

**Alarm 3: Step Functions Failures**

1. Create alarm → Step Functions → `ProcessCSVWorkflow` → ExecutionsFailed
2. กำหนด:
   ```
   Statistic: Sum
   Period: 5 minutes
   Threshold: Greater than 0
   ```
3. Alarm name: `pipeline-execution-failures`

---

### ✅ STEP 7 — End-to-End Test สมบูรณ์

ทดสอบ Full Pipeline ทั้งหมด:

**Test Case 1: Happy Path (ไฟล์ถูกต้อง)**
1. อัปโหลด `sample_sales.csv` ไปที่ `uploads/`
2. รอ ~30 วินาที
3. ตรวจสอบ:
   - [ ] CloudWatch Logs: `csv-validator` → queued
   - [ ] CloudWatch Logs: `csv-processor` → execution started
   - [ ] Step Functions: Execution สำเร็จ (สีเขียวทั้งหมด)
   - [ ] S3 `processed/`: มีไฟล์ `_result.json`
   - [ ] Email: ได้รับ Notification ✅

**Test Case 2: Schema Error**
1. อัปโหลด CSV ที่ขาด Column
2. ตรวจสอบ:
   - [ ] Step Functions: ไปเส้น `MoveToFailed`
   - [ ] S3: ไฟล์ถูกย้ายไป `failed/`
   - [ ] Email: ได้รับ Notification ❌ พร้อมสาเหตุ

**Test Case 3: ทดสอบ DLQ**
1. ทำให้ `parse-csv` Lambda Error ชั่วคราว
2. อัปโหลดไฟล์
3. ตรวจสอบ:
   - [ ] SQS DLQ: มี Message
   - [ ] CloudWatch Alarm: ถูก Trigger
   - [ ] Email Alert: ได้รับ Alarm notification

---

### 📝 แบบฝึกหัดเพิ่มเติม Week 4

1. **เพิ่ม SMS Notification:** สร้าง SNS Subscription แบบ SMS (ใช้เบอร์มือถือจริง)
2. **สร้าง CloudWatch Metric Filter:** ดึง Custom Metric จาก Log เช่น นับ `"event": "file_validated"` ต่อชั่วโมง
3. **เพิ่ม S3 Lifecycle Policy:** ตั้งให้ไฟล์ใน `failed/` ถูกลบอัตโนมัติหลัง 30 วัน

### ❓ คำถามท้าย LAB Week 4

1. SNS Subscription แบบ Email กับแบบ SQS ต่างกันยังไงในแง่ Reliability? อะไรเกิดขึ้นถ้า Email Server Down?
2. CloudWatch Alarm มีกี่ State? แต่ละ State หมายความว่าอะไร?
3. ถ้าต้องการ Monitor Latency ของ Pipeline ทั้งหมด (ตั้งแต่ Upload จนถึง Email ส่ง) จะวัดได้ยังไง?

---

---

# 🏗️ Final Architecture & Summary

---

## Architecture Diagram (สมบูรณ์)

```
┌─────────────────────────────────────────────────────────────────┐
│                    AWS Data Pipeline Architecture                │
│                      (All Serverless, Free Tier)                 │
└─────────────────────────────────────────────────────────────────┘

[User]
  │  Upload CSV
  ▼
[S3: raw-uploads/]                         [CloudWatch]
  │  ObjectCreated Event                        │
  │                                    Monitors everything
  ▼                                             │
[Lambda: csv-validator]  ──Logs──────────────> │
  │  Validate + Send Message                    │
  ▼                                             │
[SQS: pipeline-main-queue]  ─Metrics─────────> │
  │  (DLQ: pipeline-dlq)                        │
  │  SQS Trigger                                │
  ▼                                             │
[Lambda: csv-processor]  ──Logs──────────────> │
  │  Start Execution                            │
  ▼                                             │
[Step Functions: ProcessCSVWorkflow]  ─────> Execution Metrics
  │
  ├─[Lambda: parse-csv]
  │
  ├─[Lambda: validate-schema]
  │         │
  │    ┌────┴────┐
  │  Valid    Invalid
  │    │         │
  │    ▼         ▼
  │ [Lambda:  [Lambda:
  │  transform] move-to-failed]
  │    │         │
  │    └────┬────┘
  │         │
  ▼         ▼
[Lambda: send-notification]
  │
  ▼
[SNS: pipeline-notifications]
  │              │
  ▼              ▼
[Email]       [SMS / Lambda / SQS ...]

Output: [S3: processed/YYYY/MM/DD/*.json]
Failed: [S3: raw-uploads/failed/YYYY/MM/DD/*.csv]
```

---

## Services สรุปทั้ง 4 สัปดาห์

| AWS Service | ใช้ทำอะไร | สัปดาห์ | Free Tier |
|-------------|-----------|---------|-----------|
| S3 | รับไฟล์ดิบ, เก็บผลลัพธ์ | Week 1 | 5 GB / เดือน |
| Lambda | Business Logic ทุก Step | Week 1–4 | 1M invocations / เดือน |
| IAM | จัดการสิทธิ์ (Least Privilege) | Week 1 | ฟรีเสมอ |
| SQS | Decouple + Queue | Week 2 | 1M requests / เดือน |
| Step Functions | Orchestrate Workflow | Week 3 | 4,000 transitions / เดือน |
| SNS | Notification | Week 4 | 1M publishes / เดือน |
| CloudWatch | Monitor + Alert | Week 4 | 5 GB logs / เดือน |

---

## Cost Estimation (หลัง Free Tier หมด)

สมมติ Pipeline ประมวลผลไฟล์ 100 ไฟล์/วัน:

| Service | Estimated Usage | Estimated Cost |
|---------|----------------|----------------|
| S3 | 1 GB storage + transfers | ~$0.02/เดือน |
| Lambda | 5 functions × 100 files × 30 days = 15,000 invocations | ฟรี (ต่ำกว่า 1M) |
| SQS | 100 messages/วัน = 3,000/เดือน | ฟรี (ต่ำกว่า 1M) |
| Step Functions | 100 executions × 7 transitions = 700/เดือน | ฟรี (ต่ำกว่า 4,000) |
| SNS | 100 emails/วัน = 3,000/เดือน | ฟรี (ต่ำกว่า 1,000 — ถ้าเกิน ~$0.002/notification) |
| CloudWatch | Logs + Metrics | ~$0.50/เดือน |
| **รวม** | | **< $1/เดือน** |

> 💰 Pipeline แบบนี้ถูกมากเพราะ Serverless — จ่ายตามการใช้งานจริง ไม่มีค่า Server ตลอดเวลา

---

## Design Patterns ที่เรียนมาตลอด 4 สัปดาห์

### 1. Event-Driven Pattern (Week 1)
```
Trigger ──> Function ──> Output
```
ใช้เมื่อ: ต้องตอบสนองต่อเหตุการณ์ที่เกิดขึ้นโดยอัตโนมัติ

### 2. Message Queue Pattern (Week 2)
```
Producer ──> Queue ──> Consumer
```
ใช้เมื่อ: ต้องการ Decouple ระบบ หรือจัดการ Load ที่ไม่สม่ำเสมอ

### 3. Orchestration Pattern (Week 3)
```
Orchestrator ──> Step A ──> Step B ──> Step C
```
ใช้เมื่อ: มี Workflow หลายขั้นตอนที่ซับซ้อน ต้องการ Error Handling รวมศูนย์

### 4. Fan-out Notification Pattern (Week 4)
```
Event ──> SNS ──> [Email, SMS, Lambda, SQS, ...]
```
ใช้เมื่อ: ต้องการแจ้งเตือนหลาย Channel พร้อมกัน

---

## 🚀 Next Steps — ต่อยอดจากที่เรียน

- **EventBridge:** แทน S3 Events ด้วย EventBridge Rules สำหรับ Multi-Source Events
- **Kinesis Data Streams:** รับข้อมูลแบบ Real-time Stream (ไม่ใช่ File-based)
- **Glue + Athena:** Query ข้อมูลใน S3 ด้วย SQL โดยไม่ต้อง Load เข้า Database
- **DynamoDB:** เก็บ Job Status และ Metadata ให้ Query ได้
- **API Gateway:** เพิ่ม REST API เพื่อ Trigger Pipeline หรือดูสถานะ Job
- **CDK (Cloud Development Kit):** เขียน Infrastructure เป็น Code แทนการคลิก Console
- **X-Ray:** Distributed Tracing ดู Latency ของแต่ละ Step

---

## 🏆 สิ่งที่ทำได้แล้วหลังเรียนครบ 4 สัปดาห์

- ✅ มี Data Pipeline อัตโนมัติ 100% Serverless — ไม่มี Server ดูแลเลย
- ✅ เข้าใจ 4 Design Patterns สำคัญในระบบ Distributed
- ✅ เขียน Lambda Python ที่มี Structured Logging และ Error Handling
- ✅ ออกแบบ IAM Policy แบบ Least Privilege ได้
- ✅ Debug ด้วย CloudWatch Logs และ Step Functions Visual Execution
- ✅ พร้อมสอบ **AWS Cloud Practitioner** หรือ **AWS Solutions Architect Associate**

---

*เอกสารนี้จัดทำสำหรับการเรียนการสอน AWS Cloud · Free Tier · 4 สัปดาห์*
