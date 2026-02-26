# ICT24467 — การพัฒนาซอฟต์แวร์ระบบประมวลผลคลาวด์และความปลอดภัยของข้อมูล

## คู่มือประกอบการเรียนการสอน: Serverless Computing บน AWS Cloud ยุค 2026

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
>
> **Services ที่ใช้ตลอดหลักสูตร:**  
> `AWS Lambda` · `API Gateway` · `DynamoDB` · `S3` · `CloudWatch` · `EventBridge` · `Step Functions` · `SNS` · `SQS`

---

## สารบัญ

- [ภาพรวมรายวิชา](#ภาพรวมรายวิชา)
- [สัปดาห์ที่ 1 — Serverless Fundamentals & Lambda Basics](#สัปดาห์ที่-1--serverless-fundamentals--lambda-basics)
- [สัปดาห์ที่ 2 — Serverless REST API](#สัปดาห์ที่-2--serverless-rest-api)
- [สัปดาห์ที่ 3 — Event-Driven & Storage Integration](#สัปดาห์ที่-3--event-driven--storage-integration)
- [สัปดาห์ที่ 4 — Orchestration + Monitoring + Security](#สัปดาห์ที่-4--orchestration--monitoring--security)
- [ภาคผนวก](#ภาคผนวก)

---

---

# ภาพรวมรายวิชา

**ICT24467** มุ่งเน้นให้นักศึกษาเข้าใจและปฏิบัติงานด้าน Serverless Computing บน Amazon Web Services (AWS) ได้จริงในยุคปี 2026 โดยใช้ **Free Tier ทั้งหมด ไม่เสียค่าใช้จ่าย**

---

## จุดประสงค์รายวิชา (Course Objectives)

- อธิบายแนวคิด Serverless Computing และความแตกต่างจาก Traditional Server ได้
- สร้างและ Deploy ฟังก์ชัน AWS Lambda พร้อมกำหนด Trigger Event ต่าง ๆ ได้
- ออกแบบและสร้าง REST API แบบ Serverless ด้วย API Gateway และ Lambda ได้
- ใช้ DynamoDB เป็น NoSQL Database และเชื่อมต่อกับ Serverless Function ได้
- ติดตาม Monitor และ Debug ระบบด้วย CloudWatch ได้
- วิเคราะห์ Cost และ Security ของ Serverless Architecture ได้

---

## ผลลัพธ์การเรียนรู้ที่คาดหวัง (CLOs)

| CLO | คำอธิบาย | สัปดาห์ |
|-----|----------|---------|
| CLO1 | อธิบายและเปรียบเทียบ Cloud Deployment Models และ Serverless Architecture ได้ | 1 |
| CLO2 | สร้าง Lambda Function ที่มี Event-Driven Trigger ได้อย่างถูกต้อง | 1–2 |
| CLO3 | ออกแบบ Serverless REST API ด้วย API Gateway + Lambda + DynamoDB ได้ | 2–3 |
| CLO4 | ใช้ S3, EventBridge และ Step Functions ใน Workflow จริงได้ | 3–4 |
| CLO5 | ติดตาม Monitor ด้วย CloudWatch และวิเคราะห์ Cost + Security ได้ | 4 |

---

## AWS Free Tier ที่ใช้ในรายวิชานี้ (อัปเดต 2026)

| AWS Service | Free Tier Limit | ประเภท | ใช้สัปดาห์ |
|-------------|----------------|--------|-----------|
| AWS Lambda | 1,000,000 requests + 400,000 GB-seconds / เดือน | **Always Free** | 1–4 |
| Amazon API Gateway | 1,000,000 HTTP API calls / เดือน | **Always Free** | 2–4 |
| Amazon DynamoDB | 25 GB storage + 200M requests / เดือน | **Always Free** | 2–4 |
| Amazon S3 | 5 GB + 20,000 GET + 2,000 PUT / เดือน | 12 เดือนแรก | 3–4 |
| Amazon CloudWatch | 5 GB logs + 10 custom metrics / เดือน | 12 เดือนแรก | 1–4 |
| AWS Step Functions | 4,000 state transitions / เดือน | **Always Free** | 4 |
| Amazon EventBridge | 1,000,000 custom events / เดือน | **Always Free** | 3–4 |
| Amazon SNS | 1,000,000 publishes + 1,000 emails / เดือน | **Always Free** | 4 |
| Amazon SQS | 1,000,000 requests / เดือน | **Always Free** | 3–4 |
| AWS IAM | ไม่จำกัด | **Always Free** | 1–4 |

> ⚠️ **ข้อควรระวังเรื่อง Free Tier**
> - ตั้ง **AWS Budget Alert ที่ $1** ทันทีหลังสร้าง Account เพื่อป้องกันค่าใช้จ่ายเกิน
> - หลัง Lab เสร็จทุกครั้ง ลบ Resource ที่ไม่ใช้ โดยเฉพาะ API Gateway และ S3
> - ตั้ง CloudWatch Log Retention ไว้ที่ **7 วัน** สำหรับ Development
> - DynamoDB ใช้ **On-Demand** เสมอ ไม่ใช้ Provisioned Capacity ใน Lab

---

## โครงสร้างหลักสูตร 4 สัปดาห์

| สัปดาห์ | หัวข้อ | Services หลัก | Project ที่สร้าง |
|--------|--------|---------------|----------------|
| **1** | Serverless Fundamentals + Lambda Basics | Lambda, CloudWatch, IAM | Hello Serverless Function |
| **2** | Serverless REST API | API Gateway, Lambda, DynamoDB | Task Manager API |
| **3** | Event-Driven & Storage Integration | S3, EventBridge, SQS, SNS | File Processing Pipeline |
| **4** | Orchestration + Monitoring + Security | Step Functions, CloudWatch, IAM | Complete Serverless App |

> ✅ **เป้าหมายปลายทาง:** นักศึกษามี Serverless Web Application ที่สมบูรณ์ ใช้งานได้จริง ต้นทุน $0 และพร้อมสอบ **AWS Cloud Practitioner** หรือ **Solutions Architect Associate**

---

---

# สัปดาห์ที่ 1 — Serverless Fundamentals & Lambda Basics

> **WEEK 1: พื้นฐาน Serverless และการสร้าง Lambda Function แรก**  
> ทำความเข้าใจ Serverless Computing และสร้าง Function แรกบน AWS · 2026

---

## 🎯 วัตถุประสงค์การเรียนรู้ สัปดาห์ที่ 1

- อธิบายความแตกต่างระหว่าง Traditional Server, IaaS, PaaS และ Serverless ได้
- อธิบาย Execution Model ของ AWS Lambda (Cold Start, Warm Start, Concurrency) ได้
- สร้าง Lambda Function ด้วย Python 3.12 และทดสอบผ่าน Console ได้
- ตั้งค่า CloudWatch Logs และดู Execution Log เพื่อ Debug ได้
- อธิบาย IAM Role และหลักการ Least Privilege สำหรับ Lambda ได้
- ตั้ง AWS Budget Alert เพื่อป้องกันค่าใช้จ่ายเกิน Free Tier ได้

---

## บทที่ 1.1 — Serverless Computing คืออะไร?

Serverless Computing **ไม่ได้แปลว่าไม่มี Server** แต่หมายความว่าผู้พัฒนาไม่ต้องจัดการ Server เลย AWS รับผิดชอบการ Provision, Scale, Patch และ Maintain Server ทั้งหมด ผู้พัฒนาเขียนแค่โค้ดและกำหนด Event ที่ต้องการ

### เปรียบเทียบ Cloud Computing Models

| เปรียบเทียบ | Traditional Server | IaaS (EC2) | PaaS | Serverless (Lambda) |
|------------|-------------------|-----------|------|-------------------|
| จัดการ OS | ✅ ผู้พัฒนา | ✅ ผู้พัฒนา | ❌ AWS | ❌ AWS |
| จัดการ Runtime | ✅ ผู้พัฒนา | ✅ ผู้พัฒนา | ❌ AWS | ❌ AWS |
| Scale อัตโนมัติ | ❌ | ❌ (ต้องตั้งเอง) | ✅ | ✅ (ทันที) |
| จ่ายเมื่อไม่ใช้ | ✅ จ่ายตลอด | ✅ จ่ายตลอด | ✅ จ่ายตลอด | ❌ ไม่จ่าย |
| ค่าใช้จ่าย | สูง | ปานกลาง | ปานกลาง | ต่ำมาก (Pay-per-use) |

---

## บทที่ 1.2 — AWS Lambda Architecture

Lambda ทำงานโดยรับ **Event** จาก Trigger → สร้าง Execution Environment → รัน Handler Function → ส่ง Response กลับ AWS จัดการ Infrastructure ทั้งหมด

### Lambda Execution Model ที่ต้องเข้าใจ

| แนวคิด | คำอธิบาย | ผลกระทบ |
|--------|----------|---------|
| **Cold Start** | Lambda สร้าง Execution Environment ใหม่ครั้งแรก | ใช้เวลา 100ms–2s เพิ่มเติม |
| **Warm Start** | Lambda ใช้ Environment เดิมที่มีอยู่แล้ว | เร็วกว่า Cold Start มาก |
| **Concurrency** | จำนวน Lambda ที่รันพร้อมกัน | Default 1,000 per Region |
| **Timeout** | เวลาสูงสุดที่ Lambda รันได้ | สูงสุด 15 นาที |
| **Memory** | RAM ที่จัดสรรให้ Lambda | 128 MB – 10,240 MB |
| **Ephemeral Storage** | /tmp พื้นที่ Temporary Storage | 512 MB – 10,240 MB |

> 🔑 **Free Tier 2026: AWS Lambda**
> - **1,000,000 Requests** ฟรีต่อเดือน (Always Free — ไม่หมดอายุ)
> - **400,000 GB-seconds** Compute Time ฟรีต่อเดือน
> - ตัวอย่าง: Function 128 MB ทำงาน 1 วินาที = 0.125 GB-second → รันได้ **3,200,000 ครั้ง/เดือน** บน 128 MB ก่อนเสียเงิน
> - ARM (Graviton2) ถูกกว่า x86 ประมาณ **20%** แนะนำใช้สำหรับ Production

---

## LAB 1.1 — ตั้งค่า AWS Account และ Budget Alert

### ⚠️ ทำก่อนทุก Lab!

### ขั้นตอนที่ 1 — ตั้ง AWS Budget Alert

1. เข้า AWS Console → พิมพ์ **Billing** → Cost Management → **Budgets** → Create budget
2. Budget type: **Cost budget**
3. Budget name: `student-free-tier-alert`
4. Budget amount: **$1.00 / Monthly**
5. Alert threshold: **50% ($0.50)** → Email: ใส่ Email ของคุณ
6. กด **Create budget**

> ⚠️ ถ้าได้รับ Email แจ้งเตือน ให้หยุดทำ Lab และตรวจสอบ Resource ที่ใช้อยู่ทันที

---

### ขั้นตอนที่ 2 — สร้าง IAM Role สำหรับ Lambda

1. เข้า **IAM** → Roles → Create role
2. Trusted entity type: AWS service → Use case: **Lambda** → Next
3. ค้นหา Policy: **AWSLambdaBasicExecutionRole** → เลือก → Next
4. Role name: `lambda-basic-role`
5. กด **Create role**

> 🔑 **หลักการ Least Privilege**
> - ให้สิทธิ์เท่าที่จำเป็นเท่านั้น — Lambda ที่ยังไม่ต้องการ DynamoDB อย่าให้สิทธิ์ DynamoDB
> - `AWSLambdaBasicExecutionRole` = อนุญาตแค่การเขียน CloudWatch Logs เท่านั้น
> - เพิ่ม Permission ทีละ Service เมื่อต้องการจริง ๆ

---

## LAB 1.2 — สร้าง Lambda Function แรก

### ขั้นตอนที่ 1 — สร้าง Lambda Function

1. เข้า **Lambda** → Create function
2. Function name: `hello-serverless`
3. Runtime: **Python 3.12**
4. Architecture: **arm64** (Graviton2 — ถูกกว่า x86 ~20%)
5. Execution role: Use an existing role → `lambda-basic-role`
6. กด **Create function**

---

### ขั้นตอนที่ 2 — เขียน Handler Function

ใน **Code tab** → แทนที่โค้ดทั้งหมดด้วย:

```python
import json
import logging
from datetime import datetime, timezone

# ตั้ง Logger — ใช้แทน print() เพื่อให้ CloudWatch จัดการได้
logger = logging.getLogger()
logger.setLevel(logging.INFO)

def lambda_handler(event, context):
    """
    Lambda Entry Point
    event  : ข้อมูลที่ส่งมาจาก Trigger
    context: ข้อมูลเกี่ยวกับ Execution Environment
    """
    # Structured Logging — ค้นหาง่ายใน CloudWatch
    logger.info(json.dumps({
        "event_type": "function_invoked",
        "request_id": context.aws_request_id,
        "function_name": context.function_name,
        "remaining_time_ms": context.get_remaining_time_in_millis(),
        "received_event": event,
        "timestamp": datetime.now(timezone.utc).isoformat()
    }))

    # ดึงชื่อจาก Event (ถ้ามี)
    name = event.get("name", "Serverless World")

    response = {
        "statusCode": 200,
        "message": f"สวัสดี {name}! จาก AWS Lambda 2026",
        "function": context.function_name,
        "memory_mb": context.memory_limit_in_mb,
        "request_id": context.aws_request_id,
        "timestamp": datetime.now(timezone.utc).isoformat()
    }

    logger.info(json.dumps({"event_type": "response_sent", "response": response}))
    return response
```

กด **Deploy** หลังแก้ไขโค้ดเสร็จ

---

### ขั้นตอนที่ 3 — ทดสอบ Function และดู CloudWatch Logs

1. กด **Test** tab → Create new event
2. Event name: `test-hello`
3. วาง JSON นี้เป็น Event body:

```json
{ "name": "นักศึกษา ICT" }
```

4. กด **Test** → ดูผลใน Execution results
5. กด **Monitor** tab → กด **View logs in CloudWatch** → ดู Log stream ล่าสุด

> ✅ **ผลที่คาดว่าจะเห็น**
> - Execution results: `statusCode 200` + message "สวัสดี นักศึกษา ICT!"
> - CloudWatch Log: JSON แต่ละ Event ที่ `logger.info()` บันทึกไว้
> - Duration: ต่ำกว่า 10ms (Warm Start) หรือ 100–300ms (Cold Start)

---

## LAB 1.3 — เข้าใจ Cold Start และ Execution Context

### ขั้นตอนที่ 1 — ทดสอบ Cold Start vs Warm Start

แก้โค้ด Lambda เพิ่มส่วน Init Code **นอก** Handler:

```python
import json, logging
from datetime import datetime, timezone

logger = logging.getLogger()
logger.setLevel(logging.INFO)

# ─── Init Code (รันตอน Cold Start เท่านั้น) ───────────────────────────────
init_time = datetime.now(timezone.utc).isoformat()
invocation_count = 0  # นับจำนวนครั้งที่ Warm Instance ถูกใช้
logger.info(json.dumps({"event": "COLD_START", "init_time": init_time}))
# ──────────────────────────────────────────────────────────────────────────

def lambda_handler(event, context):
    global invocation_count
    invocation_count += 1

    logger.info(json.dumps({
        "event": "INVOCATION",
        "count": invocation_count,
        "init_time": init_time,
        "invoke_time": datetime.now(timezone.utc).isoformat()
    }))

    return {
        "invocation_count": invocation_count,
        "init_time": init_time,
    }
```

- Deploy → **Test 3–4 ครั้งติดกัน** → ดู Log ว่า `COLD_START` ปรากฏแค่ครั้งแรก
- ดู `invocation_count` เพิ่มขึ้นเรื่อย ๆ = Warm Start ใช้ Instance เดิม

---

## สรุปและคำถามท้ายสัปดาห์ที่ 1

### สิ่งที่ได้เรียนรู้
- Serverless ไม่ใช่ไม่มี Server แต่คือ AWS จัดการ Server ให้ทั้งหมด
- Lambda ทำงานแบบ Event-Driven จ่ายเฉพาะตอนที่รันจริงเท่านั้น
- Cold Start เกิดครั้งแรก Warm Start เกิดเมื่อ Instance ยังอยู่ในระบบ
- IAM Role ต้องกำหนดแบบ Least Privilege เสมอ
- Structured Logging ด้วย JSON ทำให้ Debug ใน CloudWatch ง่ายขึ้นมาก

### คำถามทบทวน

1. ถ้า Lambda Function มี Memory 256 MB ทำงาน 500ms ต่อ Request และถูกเรียก 500,000 ครั้ง/เดือน — ยังอยู่ใน Free Tier หรือเปล่า? (แสดงการคำนวณ)
2. Cold Start ส่งผลต่อ User Experience อย่างไร? มีวิธีลด Cold Start อะไรบ้าง?
3. ทำไมต้องใช้ `Logger` แทน `print()`? และ Structured Logging ช่วยอะไร?
4. ถ้าต้องการให้ Lambda เชื่อมต่อ DynamoDB ต้องเพิ่ม Permission อะไรใน IAM Role?

> 📌 **การบ้าน (Assignment 1)**
> - สร้าง Lambda Function ที่รับ JSON input ที่มี list ของตัวเลข
> - คืนค่า: `sum`, `average`, `min`, `max`, และ `count`
> - ต้องมี Error Handling กรณี input ไม่ใช่ตัวเลข
> - ต้องมี Structured Logging ทุก Request
> - ส่ง Screenshot ของ Test Result และ CloudWatch Log ใน LMS

---

---

# สัปดาห์ที่ 2 — Serverless REST API

> **WEEK 2: สร้าง REST API แบบ Serverless ด้วย API Gateway + Lambda + DynamoDB**  
> ต่อยอดจากสัปดาห์ที่ 1 — สร้าง Task Manager API ที่ใช้งานได้จริง

---

## 🎯 วัตถุประสงค์การเรียนรู้ สัปดาห์ที่ 2

- อธิบายความแตกต่างระหว่าง REST API, HTTP API และ WebSocket API ใน API Gateway ได้
- สร้าง HTTP API ใน API Gateway เชื่อมกับ Lambda Function ได้
- ออกแบบ DynamoDB Table แบบ Single-Table Design ได้
- เขียน Lambda ที่ทำ CRUD Operations กับ DynamoDB ด้วย `boto3` ได้
- ตั้งค่า CORS และทดสอบ API ด้วย `curl` / Postman ได้

---

## บทที่ 2.1 — Amazon API Gateway

API Gateway เป็น Managed Service สำหรับสร้าง API โดยไม่ต้องดูแล Server รองรับ REST API, HTTP API และ WebSocket

### เปรียบเทียบ API Gateway Types

| | REST API | HTTP API | WebSocket API |
|--|---------|---------|--------------|
| **ราคา** | $3.50/million | $1.00/million | $1.00/million + connection hrs |
| **Free Tier** | 1M calls (12 เดือน) | 1M calls (**Always Free**) | ไม่มี Free Tier |
| **Features** | ครบที่สุด | เร็ว + ถูก + ง่าย | Real-time bidirectional |
| **JWT Authorizer** | ✅ | ✅ | ❌ |
| **แนะนำใช้** | Legacy / ต้องการ Features ครบ | สร้างใหม่ทั่วไป | Chat, Real-time apps |

> 💡 **Workshop นี้ใช้ HTTP API เพราะ**
> - ราคาถูกกว่า REST API ถึง **71%**
> - Free Tier เป็น Always Free (ไม่หมดอายุ 12 เดือน)
> - เพียงพอสำหรับ CRUD API ทั่วไป และ Latency ต่ำกว่า

---

## บทที่ 2.2 — Amazon DynamoDB

DynamoDB เป็น NoSQL Database แบบ Fully Managed Key-Value + Document Store มี Latency ต่ำมาก (single-digit milliseconds) Scale อัตโนมัติ เหมาะกับ Serverless Architecture มาก

### การออกแบบ DynamoDB Table

| แนวคิด | คำอธิบาย | ใน Project นี้ |
|--------|----------|--------------|
| **Table** | ที่เก็บ Items ทั้งหมด | `tasks` |
| **Partition Key (PK)** | กระจาย Data ไปยัง Partition | `userId` (String) |
| **Sort Key (SK)** | เรียงลำดับใน Partition เดียวกัน | `taskId` (String) |
| **Item** | แต่ละ Record เหมือน Row ใน SQL | Task แต่ละรายการ |
| **Attribute** | Field ของ Item | title, status, createdAt |
| **On-Demand Mode** | จ่ายตาม Request จริง | ใช้ใน Lab (Free Tier ดีสุด) |

---

## LAB 2.1 — สร้าง DynamoDB Table

### ขั้นตอนที่ 1

1. เข้า **DynamoDB** → Create table
2. Table name: `tasks`
3. Partition key: `userId` — Type: **String**
4. Sort key: `taskId` — Type: **String**
5. Table settings: **Customize settings**
6. Table class: DynamoDB Standard
7. Read/write capacity settings: **On-demand** ← สำคัญ ป้องกัน Cost เกิน
8. กด **Create table** → รอ Status เป็น **Active**

---

## LAB 2.2 — สร้าง Task Manager API

### ขั้นตอนที่ 1 — สร้าง IAM Role สำหรับ Lambda + DynamoDB

สร้าง Role ใหม่ (IAM → Roles → Create role → Lambda) พร้อม Inline Policy แบบ Least Privilege:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DynamoDBTasksTable",
      "Effect": "Allow",
      "Action": [
        "dynamodb:GetItem",
        "dynamodb:PutItem",
        "dynamodb:UpdateItem",
        "dynamodb:DeleteItem",
        "dynamodb:Query"
      ],
      "Resource": "arn:aws:dynamodb:ap-southeast-1:*:table/tasks"
    },
    {
      "Sid": "CloudWatchLogs",
      "Effect": "Allow",
      "Action": ["logs:CreateLogGroup","logs:CreateLogStream","logs:PutLogEvents"],
      "Resource": "arn:aws:logs:*:*:*"
    }
  ]
}
```

Role name: `lambda-tasks-api-role` → Create role

---

### ขั้นตอนที่ 2 — สร้าง Lambda Function: `tasks-api`

Lambda → Create function → `tasks-api` → Python 3.12 → arm64 → `lambda-tasks-api-role`

วางโค้ด CRUD API สมบูรณ์:

```python
import json, boto3, uuid, logging
from datetime import datetime, timezone
from boto3.dynamodb.conditions import Key

logger   = logging.getLogger()
logger.setLevel(logging.INFO)

dynamodb = boto3.resource('dynamodb')
table    = dynamodb.Table('tasks')

def cors_headers():
    return {
        'Content-Type': 'application/json',
        'Access-Control-Allow-Origin': '*',
        'Access-Control-Allow-Methods': 'GET,POST,PUT,DELETE,OPTIONS',
        'Access-Control-Allow-Headers': 'Content-Type,Authorization'
    }

def response(code, body):
    return {'statusCode': code, 'headers': cors_headers(),
            'body': json.dumps(body, ensure_ascii=False)}

def lambda_handler(event, context):
    method = event['requestContext']['http']['method']
    path   = event.get('rawPath', '/')
    logger.info(json.dumps({'method': method, 'path': path,
                            'requestId': context.aws_request_id}))

    if method == 'OPTIONS':
        return response(200, {})

    # userId จาก query string (Week 3 จะเปลี่ยนเป็น JWT Claims)
    qs      = event.get('queryStringParameters') or {}
    user_id = qs.get('userId', 'demo-user')

    # GET /tasks — ดึงรายการ Tasks ทั้งหมดของ User
    if method == 'GET' and path == '/tasks':
        result = table.query(
            KeyConditionExpression=Key('userId').eq(user_id)
        )
        return response(200, result['Items'])

    # POST /tasks — สร้าง Task ใหม่
    elif method == 'POST' and path == '/tasks':
        body = json.loads(event.get('body') or '{}')
        now  = datetime.now(timezone.utc).isoformat()
        item = {
            'userId':      user_id,
            'taskId':      str(uuid.uuid4()),
            'title':       body.get('title', 'ไม่มีชื่อ'),
            'description': body.get('description', ''),
            'status':      'pending',
            'priority':    body.get('priority', 'medium'),
            'createdAt':   now,
            'updatedAt':   now,
        }
        table.put_item(Item=item)
        logger.info(json.dumps({'event': 'task_created', 'taskId': item['taskId']}))
        return response(201, item)

    # PUT /tasks/{taskId} — อัปเดต Status
    elif method == 'PUT' and '/tasks/' in path:
        task_id    = path.split('/')[-1]
        body       = json.loads(event.get('body') or '{}')
        new_status = body.get('status', 'done')
        table.update_item(
            Key={'userId': user_id, 'taskId': task_id},
            UpdateExpression='SET #s = :s, updatedAt = :u',
            ExpressionAttributeNames={'#s': 'status'},
            ExpressionAttributeValues={':s': new_status,
                ':u': datetime.now(timezone.utc).isoformat()}
        )
        return response(200, {'message': 'Updated', 'taskId': task_id, 'status': new_status})

    # DELETE /tasks/{taskId} — ลบ Task
    elif method == 'DELETE' and '/tasks/' in path:
        task_id = path.split('/')[-1]
        table.delete_item(Key={'userId': user_id, 'taskId': task_id})
        logger.info(json.dumps({'event': 'task_deleted', 'taskId': task_id}))
        return response(200, {'message': 'Deleted', 'taskId': task_id})

    return response(404, {'error': 'Route not found'})
```

กด **Deploy** → Configuration → General → Timeout: **30 seconds** → Save

---

### ขั้นตอนที่ 3 — สร้าง API Gateway (HTTP API)

1. เข้า **API Gateway** → Create API → **HTTP API** → Build
2. Integration: Lambda → เลือก `tasks-api`
3. API name: `tasks-http-api` → Next → Next → Create

**เพิ่ม Routes:**
- Routes → Create → `GET /tasks`
- Routes → Create → `POST /tasks`
- Routes → Create → `PUT /tasks/{taskId}`
- Routes → Create → `DELETE /tasks/{taskId}`

**ตั้งค่า CORS:** Develop → CORS → Edit
- Allow origins: `*`
- Allow methods: `GET POST PUT DELETE OPTIONS`
- Allow headers: `Content-Type,Authorization`
- กด **Save**

จด **Invoke URL** เช่น: `https://abc123.execute-api.ap-southeast-1.amazonaws.com`

---

### ขั้นตอนที่ 4 — ทดสอบ API

```bash
# 1. สร้าง Task ใหม่
curl -X POST 'https://YOUR-API-URL/tasks?userId=student01' \
  -H 'Content-Type: application/json' \
  -d '{"title": "ทำ Lab AWS Week 2",
       "description": "สร้าง DynamoDB + Lambda API",
       "priority": "high"}'

# 2. ดู Tasks ทั้งหมด
curl 'https://YOUR-API-URL/tasks?userId=student01'

# 3. อัปเดต Status (ใส่ taskId จากผลลัพธ์ข้อ 1)
curl -X PUT 'https://YOUR-API-URL/tasks/TASK-ID?userId=student01' \
  -H 'Content-Type: application/json' \
  -d '{"status": "done"}'

# 4. ลบ Task
curl -X DELETE 'https://YOUR-API-URL/tasks/TASK-ID?userId=student01'
```

---

## คำถามท้ายสัปดาห์ที่ 2

1. HTTP API กับ REST API ใน API Gateway ต่างกันอย่างไร? เหตุใดจึงเลือกใช้ HTTP API ใน Workshop นี้?
2. DynamoDB On-Demand กับ Provisioned Capacity ต่างกันอย่างไร? ในสถานการณ์ใดควรใช้ Provisioned?
3. ทำไม Partition Key สำคัญมากใน DynamoDB? ถ้าผู้ใช้หลายคน Query พร้อมกัน ระบบ Scale อย่างไร?
4. CORS คืออะไร? Browser จะ Block Request ในสถานการณ์ใดบ้าง?

> 📌 **การบ้าน (Assignment 2)**
> - เพิ่ม Endpoint `GET /tasks/stats?userId=...` ที่คืนสถิติ เช่น จำนวน Task แต่ละ Status
> - เพิ่ม Input Validation ตรวจสอบว่า `title` ต้องไม่ว่างเปล่า และ `priority` ต้องเป็น `low/medium/high`
> - เพิ่ม Global Secondary Index (GSI) บน `status` เพื่อ Query Task ตาม Status ได้
> - ส่ง API URL และ Screenshot ของ Test ทุก Endpoint ใน LMS

---

---

# สัปดาห์ที่ 3 — Event-Driven & Storage Integration

> **WEEK 3: การเชื่อมต่อแบบ Event-Driven ด้วย S3, EventBridge, SQS และ SNS**  
> สร้าง File Processing Pipeline — อัปโหลดไฟล์ → ประมวลผลอัตโนมัติ → แจ้งเตือน

---

## 🎯 วัตถุประสงค์การเรียนรู้ สัปดาห์ที่ 3

- อธิบาย Event-Driven Architecture และเปรียบเทียบกับ Request-Response ได้
- สร้าง S3 Bucket และตั้งค่า Event Notification ไปยัง Lambda ได้
- ใช้ Amazon EventBridge สร้าง Rule และ Schedule Event ได้
- เข้าใจ SQS Queue, Message Visibility Timeout และ Dead Letter Queue
- ส่ง Notification ผ่าน SNS ได้ทั้ง Email และ SMS
- ออกแบบ Decoupled Architecture โดยใช้ Queue ระหว่าง Services ได้

---

## บทที่ 3.1 — Event-Driven Architecture

Event-Driven Architecture คือรูปแบบที่ Component ต่าง ๆ สื่อสารกันผ่าน **Event** แทนการเรียกกันโดยตรง ทำให้แต่ละส่วนเป็นอิสระจากกัน (Loose Coupling) Scale ได้ง่าย และทนต่อความล้มเหลว

| Pattern | คำอธิบาย | Service ที่ใช้ | ตัวอย่างในชีวิตจริง |
|---------|----------|--------------|------------------|
| **S3 Event** | เมื่อมีไฟล์ถูก Upload → Trigger Lambda | S3 → Lambda | อัปโหลดรูป → Resize อัตโนมัติ |
| **Schedule Event** | รัน Lambda ตามเวลา เหมือน cron job | EventBridge → Lambda | สร้าง Report ทุกคืน |
| **Message Queue** | ส่งงานผ่าน Queue รองรับ Load สูง | SQS → Lambda | ประมวลผล Order |
| **Pub/Sub** | ส่ง Message ไปหลาย Subscriber พร้อมกัน | SNS → Email/SMS/Lambda | แจ้งเตือนหลาย Channel |

---

## LAB 3.1 — S3 Event Trigger

### ขั้นตอนที่ 1 — สร้าง S3 Buckets

เข้า **S3** → Create bucket (สร้าง 2 อัน):

- **Bucket 1 (รับไฟล์):** `ict-uploads-[ชื่อ]-2026`
- **Bucket 2 (เก็บผล):** `ict-processed-[ชื่อ]-2026`
- Region: `ap-southeast-1` | Block all public access: ✅

สร้าง Folder ใน Bucket แรก:
- `files/` — สำหรับรับไฟล์ทั่วไป
- `reports/` — สำหรับรับ CSV รายงาน

> ⚠️ **ทำไมต้องแยก 2 Bucket?**  
> ถ้า Lambda อ่านและเขียนกลับ Bucket เดียวกัน จะเกิด **Recursive Loop!**  
> กฎ: **Input Bucket ≠ Output Bucket** เสมอ

---

### ขั้นตอนที่ 2 — สร้าง Lambda: `file-processor`

Lambda → Create function → `file-processor` → Python 3.12 → arm64

เพิ่ม IAM Policy สำหรับ S3:

```json
[
  {
    "Sid": "S3Read",
    "Effect": "Allow",
    "Action": ["s3:GetObject"],
    "Resource": "arn:aws:s3:::ict-uploads-[ชื่อ]-2026/*"
  },
  {
    "Sid": "S3Write",
    "Effect": "Allow",
    "Action": ["s3:PutObject"],
    "Resource": "arn:aws:s3:::ict-processed-[ชื่อ]-2026/*"
  }
]
```

โค้ด Lambda สำหรับประมวลผลไฟล์:

```python
import json, boto3, csv, io, logging
from datetime import datetime, timezone

logger = logging.getLogger()
logger.setLevel(logging.INFO)
s3 = boto3.client('s3')
PROCESSED_BUCKET = 'ict-processed-[ชื่อ]-2026'

def lambda_handler(event, context):
    for record in event['Records']:
        bucket = record['s3']['bucket']['name']
        key    = record['s3']['object']['key']
        size   = record['s3']['object']['size']

        logger.info(json.dumps({
            'event': 'file_received', 'bucket': bucket,
            'key': key, 'size_bytes': size
        }))

        # อ่านไฟล์จาก S3
        obj     = s3.get_object(Bucket=bucket, Key=key)
        content = obj['Body'].read().decode('utf-8')

        # ประมวลผลตามประเภทไฟล์
        if key.lower().endswith('.csv'):
            result = process_csv(content, key)
        else:
            result = {'type': 'text', 'chars': len(content), 'lines': content.count('\n')}

        # บันทึกผลลัพธ์
        out_key = f"results/{datetime.now(timezone.utc).strftime('%Y/%m/%d')}/{key.split('/')[-1]}.json"
        s3.put_object(
            Bucket=PROCESSED_BUCKET, Key=out_key,
            Body=json.dumps(result, ensure_ascii=False, indent=2),
            ContentType='application/json'
        )
        logger.info(json.dumps({'event': 'file_processed', 'output': out_key}))
    return {'statusCode': 200}

def process_csv(content, filename):
    reader = csv.DictReader(io.StringIO(content))
    rows   = list(reader)
    return {
        'filename': filename,
        'type': 'csv',
        'total_rows': len(rows),
        'columns': list(rows[0].keys()) if rows else [],
        'processed_at': datetime.now(timezone.utc).isoformat()
    }
```

---

### ขั้นตอนที่ 3 — ตั้งค่า S3 Event Trigger

ใน Lambda `file-processor` → Configuration → **Triggers** → Add trigger

- Trigger: **S3** → Bucket: `ict-uploads-[ชื่อ]-2026`
- Event types: **All object create events**
- **Prefix: `files/`** ← สำคัญมาก ป้องกัน Recursive Loop
- ✅ Acknowledge recursive invocation warning → **Add**

---

## LAB 3.2 — EventBridge Scheduled Rules

### ขั้นตอนที่ 1 — สร้าง Scheduled Lambda: `daily-summary`

สร้าง Lambda Function: `daily-summary` → Python 3.12 → arm64

```python
import json, boto3, logging
from datetime import datetime, timezone

logger = logging.getLogger()
logger.setLevel(logging.INFO)
dynamodb = boto3.resource('dynamodb')
table    = dynamodb.Table('tasks')

def lambda_handler(event, context):
    logger.info(json.dumps({
        'event': 'scheduled_run',
        'source': event.get('source', 'eventbridge'),
        'time': event.get('time', datetime.now(timezone.utc).isoformat())
    }))

    result    = table.scan()
    all_tasks = result['Items']

    summary = {
        'total':   len(all_tasks),
        'pending': sum(1 for t in all_tasks if t.get('status') == 'pending'),
        'done':    sum(1 for t in all_tasks if t.get('status') == 'done'),
        'generated_at': datetime.now(timezone.utc).isoformat()
    }
    logger.info(json.dumps({'event': 'summary_generated', 'summary': summary}))
    return summary
```

---

### ขั้นตอนที่ 2 — สร้าง EventBridge Rule

1. เข้า **EventBridge** → Rules → Create rule
2. Rule name: `daily-task-summary`
3. Rule type: **Schedule**
4. Schedule pattern: Rate expression → Rate: **1 day**
5. Target: Lambda function → `daily-summary` → Create rule

> 💡 **Cron Expression ที่ควรรู้**
> | Expression | ความหมาย |
> |------------|---------|
> | `cron(0 0 * * ? *)` | ทุกวัน เที่ยงคืน UTC |
> | `cron(0 9 * * ? *)` | ทุกวัน 09:00 UTC (16:00 น. ไทย) |
> | `cron(0 9 ? * MON *)` | ทุกวันจันทร์ 09:00 UTC |
> | `rate(5 minutes)` | ทุก 5 นาที (ดีสำหรับทดสอบ) |

---

## LAB 3.3 — SQS + SNS Notification

### ขั้นตอนที่ 1 — สร้าง SNS Topic

1. เข้า **SNS** → Topics → Create topic → **Standard** → Name: `task-notifications`
2. Create subscription → Protocol: **Email** → Endpoint: `[ใส่ Email ของคุณ]`
3. เช็ค Email → กด **Confirm subscription**

### ขั้นตอนที่ 2 — สร้าง SQS Queue

1. เข้า **SQS** → Create queue → **Standard** → Name: `task-processing-queue`
2. Visibility timeout: **30 seconds**
3. Message retention: 4 days
4. **Receive message wait time: 20 seconds** ← Long Polling ประหยัด Cost
5. Create queue

---

### ขั้นตอนที่ 3 — Lambda ส่งข้อความผ่าน SNS

เพิ่มโค้ดใน `tasks-api` Lambda (POST route) ให้ส่ง SNS เมื่อสร้าง Task สำเร็จ:

```python
import boto3
sns = boto3.client('sns', region_name='ap-southeast-1')
SNS_ARN = 'arn:aws:sns:ap-southeast-1:[ACCOUNT-ID]:task-notifications'

# เพิ่มใน POST handler หลัง table.put_item():
try:
    sns.publish(
        TopicArn=SNS_ARN,
        Subject=f'Task ใหม่: {item["title"]}',
        Message=json.dumps({
            'message': 'สร้าง Task ใหม่แล้ว',
            'taskId':  item['taskId'],
            'title':   item['title'],
            'userId':  user_id
        }, ensure_ascii=False),
    )
    logger.info('SNS notification sent')
except Exception as e:
    logger.warning(f'SNS publish failed: {e}')  # ไม่ block main flow
```

- เพิ่ม `sns:Publish` Permission ใน IAM Role ของ `tasks-api` Lambda ด้วย
- Deploy → ทดสอบสร้าง Task → รอดู Email แจ้งเตือน

---

## คำถามท้ายสัปดาห์ที่ 3

1. ทำไม S3 Event Trigger ถึงต้องตั้ง Prefix? ถ้าไม่ตั้งจะเกิดอะไรขึ้น?
2. SQS Long Polling กับ Short Polling ต่างกันอย่างไร? ทำไม Long Polling ถึงประหยัดกว่า?
3. SNS กับ SQS ต่างกันอย่างไร? ในสถานการณ์ใดควรใช้ SNS? สถานการณ์ใดควรใช้ SQS?
4. ถ้า Lambda ที่รับ SQS Message ล้มเหลว 3 ครั้ง Message จะไปไหน? Dead Letter Queue คืออะไร?

> 📌 **การบ้าน (Assignment 3)**
> - ออกแบบ Event-Driven Pipeline สำหรับระบบ E-commerce: User อัปโหลด Product Image → อะไรเกิดขึ้นต่อ?
> - วาด Architecture Diagram แสดง S3, Lambda, SQS, SNS และ DynamoDB
> - เขียน Lambda Function อย่างน้อย 1 ตัวใน Pipeline นั้น
> - ส่งเป็น PDF พร้อม Diagram และโค้ดใน LMS

---

---

# สัปดาห์ที่ 4 — Orchestration + Monitoring + Security

> **WEEK 4: Step Functions · CloudWatch Dashboard · IAM Best Practices**  
> สรุป Architecture ที่สมบูรณ์ และวิเคราะห์ Cost + Security

---

## 🎯 วัตถุประสงค์การเรียนรู้ สัปดาห์ที่ 4

- สร้าง Step Functions State Machine เพื่อ Orchestrate Lambda หลายตัวได้
- สร้าง CloudWatch Dashboard แสดง Metrics สำคัญของ Serverless App ได้
- ตั้ง CloudWatch Alarm แจ้งเตือนเมื่อเกิด Error ได้
- อธิบาย IAM Best Practices สำหรับ Serverless ได้
- วิเคราะห์ Cost ของ Serverless Architecture และ Optimize ได้
- เปรียบเทียบ Serverless กับ Traditional Architecture ในมิติต่าง ๆ ได้

---

## บทที่ 4.1 — AWS Step Functions

Step Functions ช่วย **Orchestrate Lambda Functions** หลายตัวเข้าเป็น Workflow ที่มี Visual Diagram แทนที่จะให้ Lambda เรียก Lambda กันเองโดยตรง

| เปรียบเทียบ | Lambda เรียก Lambda โดยตรง | Step Functions |
|------------|--------------------------|---------------|
| มองเห็น Flow | ❌ ยาก ต้องดู Log ทีละตัว | ✅ Visual Diagram ชัดเจน |
| Error Handling | ต้องเขียน try-catch ทุก Lambda | ✅ Catch และ Retry ใน State Machine |
| Timeout แต่ละ Step | ❌ ควบคุมยาก | ✅ กำหนดได้ทุก State |
| Parallel Processing | ต้องเขียน Code เอง | ✅ Parallel State รองรับได้เลย |
| ราคา Free Tier | ฟรี (ตาม Lambda invocations) | **4,000 transitions/เดือน ฟรี** |

---

## LAB 4.1 — สร้าง Step Functions: File Processing Workflow

### ขั้นตอนที่ 1 — สร้าง Lambda Functions สำหรับแต่ละ Step

สร้าง Lambda 3 ตัว (Python 3.12, arm64):

**Lambda 1: `validate-file`**
```python
def lambda_handler(event, context):
    filename = event.get('filename', '')
    size     = event.get('size_bytes', 0)
    valid    = filename.endswith(('.csv', '.txt', '.json')) and size > 0
    return {**event,
            'is_valid': valid,
            'validation_msg': 'OK' if valid else 'Invalid file type or empty'}
```

**Lambda 2: `process-file`**
```python
import json
from datetime import datetime, timezone

def lambda_handler(event, context):
    return {**event,
            'processed': True,
            'result_key': f"results/{event['filename']}.json",
            'processed_at': datetime.now(timezone.utc).isoformat()}
```

**Lambda 3: `notify-result`**
```python
import json, boto3
sns = boto3.client('sns', region_name='ap-southeast-1')
SNS_ARN = 'arn:aws:sns:ap-southeast-1:[ACCOUNT-ID]:task-notifications'

def lambda_handler(event, context):
    status = 'สำเร็จ' if event.get('processed') else 'ล้มเหลว'
    sns.publish(
        TopicArn=SNS_ARN,
        Subject=f"ประมวลผลไฟล์ {status}: {event.get('filename')}",
        Message=json.dumps(event, ensure_ascii=False)
    )
    return {**event, 'notification_sent': True}
```

---

### ขั้นตอนที่ 2 — สร้าง Step Functions State Machine

เข้า **Step Functions** → Create state machine → **Write your workflow in code** → Standard

วาง Amazon States Language (ASL):

```json
{
  "Comment": "File Processing Workflow — ICT24467 Lab",
  "StartAt": "ValidateFile",
  "States": {
    "ValidateFile": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:validate-file",
      "TimeoutSeconds": 30,
      "Retry": [{
        "ErrorEquals": ["Lambda.ServiceException"],
        "IntervalSeconds": 2,
        "MaxAttempts": 3,
        "BackoffRate": 2
      }],
      "Catch": [{"ErrorEquals": ["States.ALL"],
                 "Next": "HandleError", "ResultPath": "$.error"}],
      "Next": "CheckValidation"
    },
    "CheckValidation": {
      "Type": "Choice",
      "Choices": [{
        "Variable": "$.is_valid",
        "BooleanEquals": true,
        "Next": "ProcessFile"
      }],
      "Default": "NotifyFailure"
    },
    "ProcessFile": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:process-file",
      "TimeoutSeconds": 120,
      "Next": "NotifySuccess"
    },
    "NotifySuccess": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:notify-result",
      "Next": "WorkflowComplete"
    },
    "NotifyFailure": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:[ACCOUNT-ID]:function:notify-result",
      "Next": "WorkflowFailed"
    },
    "WorkflowComplete": {"Type": "Succeed"},
    "WorkflowFailed":   {"Type": "Fail", "Error": "ValidationFailed"},
    "HandleError":      {"Type": "Fail", "Error": "ProcessingError"}
  }
}
```

State machine name: `FileProcessingWorkflow` → Create

> ✅ **ทดสอบ State Machine**
> - กด Start execution → Input: `{"filename": "report.csv", "size_bytes": 1024}`
> - ดู Visual Diagram — State ที่กำลังทำงาน = สีฟ้า / สำเร็จ = สีเขียว / ล้มเหลว = สีแดง
> - ทดสอบ Invalid: `{"filename": "image.jpg", "size_bytes": 5000}` → ควรไปเส้น `NotifyFailure`

---

## LAB 4.2 — CloudWatch Monitoring Dashboard

### ขั้นตอนที่ 1 — สร้าง Dashboard

เข้า **CloudWatch** → Dashboards → Create dashboard → `ict24467-dashboard`

เพิ่ม Widgets:

| Widget | Metric | ประเภท |
|--------|--------|-------|
| Lambda Invocations | Lambda → Invocations → tasks-api, file-processor, daily-summary | Line Chart |
| Lambda Errors | Lambda → Errors → (functions เดียวกัน) | Line Chart |
| Lambda Duration P99 | Lambda → Duration → Statistic: **p99** | Line Chart |
| API Gateway Requests | API Gateway → tasks-http-api → Count | Number |
| DynamoDB Capacity | DynamoDB → ConsumedReadCapacityUnits + ConsumedWriteCapacityUnits | Line Chart |

กด **Save dashboard**

---

### ขั้นตอนที่ 2 — ตั้ง CloudWatch Alarm

1. CloudWatch → Alarms → Create alarm
2. Select metric → Lambda → `tasks-api` → **Errors**
3. Statistic: Sum | Period: 1 minute | Threshold: Greater than **5**
4. Action: Send notification → SNS Topic `task-notifications`
5. Alarm name: `api-error-alarm` → Create alarm

**ทดสอบ Alarm:**
```python
# แก้ tasks-api Lambda ให้ Error ชั่วคราว:
raise Exception('Test Error for Alarm Demo')
# Deploy → เรียก API 6 ครั้ง → รอ 1-2 นาที → ดู Email
```

---

## บทที่ 4.2 — Security Best Practices สำหรับ Serverless

> 🔑 **IAM Security Best Practices 2026**
> 1. **Least Privilege** — ให้สิทธิ์เฉพาะที่ Lambda นั้น ๆ ต้องการ ไม่ใช้ `AdministratorAccess`
> 2. **Resource-level Policy** — ระบุ ARN เจาะจง ไม่ใช้ `"Resource": "*"`
> 3. **แยก Role** ต่างหากสำหรับแต่ละ Lambda Function
> 4. **ไม่เก็บ Secret** ใน Environment Variables แบบ Plaintext
> 5. ใช้ **AWS Secrets Manager** หรือ **Parameter Store** สำหรับ Credentials
> 6. เปิด **AWS CloudTrail** เพื่อ Audit Log ทุกการเข้าถึง

### Security Risk ที่ต้องระวัง

| Security Risk | สาเหตุ | วิธีป้องกัน |
|--------------|--------|-----------|
| Over-permissive IAM | ให้สิทธิ์กว้างเกินไป | Least Privilege + ระบุ Resource ARN |
| Secret ใน Code | Hard-code Password ใน Source | ใช้ AWS Secrets Manager |
| Lambda ไม่มี Timeout | ค้างอยู่นาน เสียเงิน | ตั้ง Timeout เหมาะสม (30–60 วินาที) |
| ไม่มี Input Validation | SQL/Code Injection | Validate + Sanitize ทุก Input |
| Log มี Sensitive Data | Log ที่มี Password, Credit Card | Filter/Mask ก่อน Log |
| Public S3 Bucket | ข้อมูลรั่วไหล | Block All Public Access เสมอ |

---

## บทที่ 4.3 — Cost Analysis และ Optimization

### ตัวอย่างการคำนวณ Cost (100 Users, 10 req/คน/วัน)

| Service | การใช้งาน/เดือน | Free Tier | ค่าใช้จ่าย |
|---------|---------------|---------|---------|
| Lambda | 30,000 req × 100ms × 128MB = 3,750 GB-s | 400,000 GB-s | **$0.00** |
| API Gateway | 30,000 HTTP requests | 1,000,000 req | **$0.00** |
| DynamoDB | 30,000 write + 90,000 read ops | 200M req/เดือน | **$0.00** |
| S3 | 100 MB storage + 1,000 requests | 5 GB + 20K GET | **$0.00** |
| CloudWatch | 500 MB logs | 5 GB | **$0.00** |
| SNS | 30,000 notifications | 1M publishes | **$0.00** |
| **รวม** | | | **$0.00 / เดือน** ✅ |

> 💡 **Cost Optimization Tips**
> - ใช้ **ARM (Graviton2)** — ถูกกว่า x86 ~20%: Configuration → Architecture → arm64
> - ตั้ง **Memory ให้เหมาะสม** — 128MB เพียงพอสำหรับ API ทั่วไป
> - ตั้ง **Timeout สั้นที่สุด** — ถ้า Function ค้างจะเสียเงินนานขึ้น
> - ตั้ง **CloudWatch Log Retention** — 7 วัน (Dev), 30 วัน (Prod)
> - ใช้ **HTTP API** แทน REST API — ถูกกว่า 71%

---

## สรุปภาพรวม Architecture ทั้ง 4 สัปดาห์

```
        ┌───────────────────────────────────────────────────────────────┐
        │          ICT24467 — Serverless Architecture 2026               │
        └───────────────────────────────────────────────────────────────┘

  [Browser / Mobile App]
         │  HTTPS
         ▼
  [API Gateway HTTP API] ──── JWT Authorizer ────> [Cognito]
         │
         ▼
  [Lambda: tasks-api] ──── Logs ────> [CloudWatch Dashboard]
         │                                    │
         ├──> [DynamoDB: tasks]         [CloudWatch Alarms]
         │                                    │
         └──> [SNS: notifications] <─── [Alarm Triggered]
                    │
              [Email / SMS]

  [S3: ict-uploads/]
         │  ObjectCreated Event (prefix: files/)
         ▼
  [Lambda: file-processor] ──> [Step Functions: FileProcessingWorkflow]
         │  ValidateFile → CheckValidation → ProcessFile → NotifyResult
         ▼
  [S3: ict-processed/] + [SNS: result notification]

  [EventBridge] ──── Scheduled ────> [Lambda: daily-summary]
                      (rate: 1 day)
```

---

## คำถามท้ายสัปดาห์ที่ 4

1. Orchestration กับ Choreography ต่างกันอย่างไร? Step Functions ใช้แนวคิดไหน?
2. ถ้า Lambda Function ถูกเรียก 5 ล้านครั้ง/เดือน Memory 256 MB ทำงานเฉลี่ย 200ms — ต้องจ่ายเงินเท่าไหร่?
3. ทำไม IAM Role ของ Lambda ไม่ควรมี `"Resource": "*"` ใน Policy? มีความเสี่ยงอะไร?
4. จงออกแบบ Serverless Architecture สำหรับระบบจองห้องเรียน SPU (วาด Diagram + ระบุ Service ที่ใช้)

> 📌 **โครงการปลายภาค (Final Project)**
> - สร้าง Serverless Application ที่มี: Lambda ≥ 3 functions, API Gateway, DynamoDB
> - ต้องมี Event-Driven Trigger อย่างน้อย 1 อย่าง (S3 / EventBridge / SQS)
> - ต้องมี CloudWatch Dashboard แสดง Metrics ของทุก Service
> - ต้องมี IAM Roles แบบ Least Privilege พร้อมอธิบายได้
> - เขียน Report อธิบาย Architecture, Security Consideration และ Cost Analysis
> - **Demo ต่อ Presentation Panel** พร้อม Live Demo บน AWS Console

---

---

# ภาคผนวก

## ภาคผนวก A — Serverless vs Traditional: เปรียบเทียบสมบูรณ์

| มิติ | Traditional Server | Serverless (Lambda) |
|-----|--------------------|-------------------|
| การจัดการ Server | ผู้พัฒนาดูแลเอง (OS, Patch, Update) | AWS ดูแลทั้งหมด |
| การ Scale | Manual หรือ Auto Scaling Group | อัตโนมัติ ทันที ไม่จำกัด |
| ค่าใช้จ่าย | จ่ายตลอดเวลา แม้ไม่มี Traffic | จ่ายเฉพาะตอนรันจริง |
| เวลา Deploy | นาที–ชั่วโมง | วินาที |
| Cold Start | ไม่มี | มี (100ms–2s) |
| Stateful | รองรับ (RAM, Disk) | Stateless (ต้องใช้ DB/Cache) |
| Timeout | ไม่จำกัด | สูงสุด 15 นาที |
| เหมาะกับ | Long-running, Stateful Apps | Event-driven, API, Short tasks |

---

## ภาคผนวก B — AWS Free Tier Quick Reference 2026

| Service | Always Free | 12-Month Free | หมายเหตุ |
|---------|------------|--------------|---------|
| Lambda | 1M req + 400K GB-s/เดือน | — | ไม่หมดอายุ |
| DynamoDB | 25 GB + 200M req/เดือน | — | On-Demand เหมาะ Dev |
| API Gateway HTTP | 1M calls/เดือน | — | ไม่หมดอายุ |
| CloudFront | 1 TB + 10M req/เดือน | — | ไม่หมดอายุ (2026) |
| S3 | — | 5 GB + 20K GET | หมดหลัง 12 เดือน |
| CloudWatch | 5 GB logs + 10 metrics | — | เกินเสีย $0.50/GB |
| SNS | 1M publish + 1K email | — | ไม่หมดอายุ |
| SQS | 1M req/เดือน | — | ไม่หมดอายุ |
| Step Functions | 4,000 transitions/เดือน | — | ไม่หมดอายุ |
| EventBridge | 1M custom events/เดือน | — | ไม่หมดอายุ |
| IAM | ไม่จำกัด | — | ฟรีเสมอ |

---

## ภาคผนวก C — Python boto3 Quick Reference

### Lambda → DynamoDB

```python
import boto3
from boto3.dynamodb.conditions import Key, Attr

dynamodb = boto3.resource('dynamodb')
table    = dynamodb.Table('TABLE_NAME')

# Query (แนะนำ — ใช้ PK เร็วกว่า Scan)
result = table.query(KeyConditionExpression=Key('userId').eq('user01'))

# Put Item
table.put_item(Item={'userId': 'u01', 'taskId': 't01', 'title': 'Test'})

# Update Item
table.update_item(
    Key={'userId': 'u01', 'taskId': 't01'},
    UpdateExpression='SET #s = :s',
    ExpressionAttributeNames={'#s': 'status'},
    ExpressionAttributeValues={':s': 'done'}
)

# Delete Item
table.delete_item(Key={'userId': 'u01', 'taskId': 't01'})
```

### Lambda → S3

```python
import boto3
s3 = boto3.client('s3')

# อ่านไฟล์
obj     = s3.get_object(Bucket='my-bucket', Key='path/file.txt')
content = obj['Body'].read().decode('utf-8')

# เขียนไฟล์
s3.put_object(
    Bucket='my-bucket',
    Key='output/result.json',
    Body=json.dumps(data),
    ContentType='application/json'
)
```

### Lambda → SNS

```python
import boto3
sns = boto3.client('sns', region_name='ap-southeast-1')

sns.publish(
    TopicArn='arn:aws:sns:ap-southeast-1:ACCOUNT:topic-name',
    Subject='แจ้งเตือน',
    Message='เนื้อหาการแจ้งเตือน'
)
```

### Lambda → Step Functions

```python
import boto3, json
sfn = boto3.client('stepfunctions', region_name='ap-southeast-1')

sfn.start_execution(
    stateMachineArn='arn:aws:states:ap-southeast-1:ACCOUNT:stateMachine:MyWorkflow',
    name='execution-unique-id',
    input=json.dumps({'key': 'value'})
)
```

---

## ภาคผนวก D — การประเมินผล (Grading Rubric)

| ส่วนที่ประเมิน | คะแนน | รายละเอียด |
|--------------|------|-----------|
| Assignment 1–3 (Lab Work) | 30% | ส่ง Screenshot + Code ทุก Lab ครบถ้วนและทำงานได้จริง |
| Quiz ประจำสัปดาห์ | 20% | คำถามท้าย Lab ส่งตาม LMS ภายใน 1 สัปดาห์ |
| Final Project | 40% | Serverless App ครบองค์ประกอบ + Architecture Report + Demo |
| การเข้าร่วมกิจกรรม | 10% | เข้าร่วม Lab และมีส่วนร่วมในการอภิปราย |

---

## ภาคผนวก E — แหล่งเรียนรู้เพิ่มเติม

| แหล่ง | URL |
|-------|-----|
| AWS Lambda Documentation | https://docs.aws.amazon.com/lambda/ |
| AWS Serverless Land | https://serverlessland.com/ |
| AWS Free Tier Dashboard | https://aws.amazon.com/free/ |
| AWS Well-Architected Framework | https://aws.amazon.com/architecture/well-architected/ |
| Python boto3 Documentation | https://boto3.amazonaws.com/v1/documentation/api/latest/ |
| AWS Skill Builder (ฟรี) | https://skillbuilder.aws/ |
| AWS Cloud Practitioner Certification | https://aws.amazon.com/certification/certified-cloud-practitioner/ |

---

> ✅ **ข้อความถึงนักศึกษา**
>
> Serverless Computing ไม่ใช่แค่เทคโนโลยี — มันเป็นแนวคิดการออกแบบระบบที่ช่วยลดภาระ
> การดูแล Infrastructure และให้ผู้พัฒนาโฟกัสที่สิ่งสำคัญที่สุด: **Business Logic**
>
> ทักษะ AWS Serverless ที่ได้จากรายวิชานี้ตรงกับความต้องการของตลาดงาน 2026 มาก
> ขอให้นักศึกษาทุกคนสนุกกับการเรียนรู้ และอย่าลังเลที่จะทดลองสร้างสิ่งใหม่ ๆ
>
> — *อ.อำนาจ คงเจริญถิ่น  ·  คณะเทคโนโลยีสารสนเทศ  ·  มหาวิทยาลัยศรีปทุม*  
> *ภาคการศึกษา 2/2568*
