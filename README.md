# docker204

โปรเจกต์นี้เป็นงานฝึก Docker + Flask + Machine Learning แบบง่าย ๆ\
ทำเว็บ API เล็ก ๆ สำหรับทำนายราคาบ้านจากชุดข้อมูล California Housing
แล้วครอบด้วย Dockerfile ให้รันเป็น container ได้

## โครงสร้างโปรเจกต์

-   `app.py` -- Flask API
-   `train_model.py` -- เทรนโมเดลและเซฟ `model.pkl`
-   `requirements.txt` -- ไลบรารีที่ใช้
-   `Dockerfile` -- ไฟล์สร้าง Docker image

## วิธีรันแบบไม่ใช้ Docker

    pip install -r requirements.txt
    python train_model.py
    python app.py

## API

### `/health`

GET เพื่อเช็คว่าเซิร์ฟเวอร์ทำงานปกติ

### `/predict`

POST พร้อม JSON:

    {
      "features": [8.3252,41,6.9841,1.0238,322,2.5556,37.88,-122.23]
    }

## วิธีรันด้วย Docker

### Build image

    docker build -t docker204 .

### Run container

    docker run -p 5000:5000 docker204

## ทดสอบ

    curl http://localhost:5000/health
    curl -X POST http://localhost:5000/predict   -H "Content-Type: application/json"   -d '{"features":[8.3252,41,6.9841,1.0238,322,2.5556,37.88,-122.23]}'
