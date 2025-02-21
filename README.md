my-web-k8s/
│
├── Dockerfile
├── index.html
├── deployment.yaml
├── service.yaml
└── README.md


# Web Bare OS with Nginx on Kubernetes

## ขั้นตอนการทำงาน

1. **สร้างไฟล์ `index.html`**  
    - ไฟล์ HTML ที่ใช้แสดงหน้าเว็บ "About Me"

2. **สร้าง Dockerfile**  
    - ใช้ `nginx:alpine` เป็น base image
    - คัดลอกไฟล์ `index.html` ไปที่ Docker image

3. **สร้าง Kubernetes Deployment**  
    - สร้าง Deployment เพื่อให้รัน Pod สำหรับเว็บ Nginx

4. **สร้าง Kubernetes Service**  
    - เปิดการเข้าถึงเว็บผ่าน LoadBalancer

## การทดสอบ
1. ใช้คำสั่ง `kubectl get pods` และ `kubectl get svc` เพื่อตรวจสอบว่า Pod และ Service ทำงาน
2. ใช้ `kubectl port-forward` เพื่อทดสอบในเครื่องผ่าน `localhost:8080`

## การเข้าถึงเว็บ
- สามารถเข้าเว็บผ่าน `http://localhost:8080` (ถ้าใช้ port forwarding)
- หรือ `http://localhost:30297` (ถ้าใช้ LoadBalancer)

## สรุป
-สร้าง Dockerfile และคัดลอก index.html เข้าไปใน container
-สร้าง Docker image โดยใช้คำสั่ง docker build
-รัน container โดยใช้คำสั่ง docker run และ mount directory
-ทดสอบการเข้าถึงเว็บ ผ่าน localhost:8080
-สร้างไฟล์ index.html 2 เวอร์ชัน (เช่น index_v1.html และ index_v2.html)
-อัปเดต Dockerfile เพื่อใช้ไฟล์ index.html ที่แตกต่างกัน
-สร้าง Docker image สำหรับทั้งสองเวอร์ชัน (v1 และ v2)
-สร้าง Deployment ใน Kubernetes โดยใช้ Docker image เวอร์ชันแรก (v1)
-ใช้คำสั่ง kubectl set image เพื่อทำ Rolling Update และอัปเดตเป็นเวอร์ชันที่สอง (v2)
-ใช้คำสั่ง kubectl rollout undo หากต้องการทำ Rollback ไปยังเวอร์ชันก่อนหน้า
