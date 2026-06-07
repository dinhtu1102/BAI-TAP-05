# BAI-TAP-05

A.Lý thuyết

1. Docker là gì?

  Docker là nền tảng ảo hóa ở mức hệ điều hành, cho phép đóng gói ứng dụng cùng toàn bộ môi trường chạy (thư viện, dependency, cấu hình, runtime) vào các Container.
  
  Docker giúp ứng dụng hoạt động nhất quán trên nhiều môi trường khác nhau như máy cá nhân, máy chủ vật lý, máy ảo hoặc môi trường Cloud.

* Các thành phần chính của Docker:

  - Docker Engine: dịch vụ chạy Docker. 

  - Docker Image: mẫu (template) dùng để tạo container. 

  - Docker Container: môi trường chạy thực tế của ứng dụng. 

  - Docker Registry: nơi lưu trữ image. 

  - Docker Compose: công cụ quản lý nhiều container bằng một file cấu hình.

2.Các keyword thường dùng trong docker-compose.yml

* Nhóm Service

<img width="387" height="591" alt="image" src="https://github.com/user-attachments/assets/2c87a0eb-7158-41e1-9362-6760684bb754" />

* Nhóm Storage

<img width="321" height="131" alt="image" src="https://github.com/user-attachments/assets/d2f10af9-9ee2-4be7-a6e8-c906f8e24fde" />

* Nhóm Network

<img width="268" height="221" alt="image" src="https://github.com/user-attachments/assets/42dffbd7-7e50-49da-98a2-df4c16631a77" />

* Nhóm Resource

<img width="237" height="186" alt="image" src="https://github.com/user-attachments/assets/c5a57087-3704-4a3e-8b9e-3c83ccadbffc" />

* Nhóm Security

<img width="231" height="186" alt="image" src="https://github.com/user-attachments/assets/3c94c88d-4d6e-46b3-a7f6-07a9b60ab1fe" />

* Nhóm Logging

<img width="223" height="127" alt="image" src="https://github.com/user-attachments/assets/01d54a5f-7f72-4138-94e7-85b4ecc177e0" />

* Nhóm Khai báo ngoài Service

<img width="287" height="212" alt="image" src="https://github.com/user-attachments/assets/6ec22615-d28b-4378-a2e5-668c8070b8b0" />

3. Ưu điểm khi triển khai ứng dụng bằng Docker

  - Đồng nhất môi trường: Ứng dụng hoạt động giống nhau trên mọi máy, tránh lỗi khác biệt môi trường.
  
  - Triển khai nhanh: Chỉ cần tải image và khởi động container thay vì cài đặt thủ công toàn bộ phần mềm.
  
  - Dễ mở rộng: Có thể tăng số lượng container để đáp ứng tải hệ thống.
  
  - Cô lập ứng dụng: Các ứng dụng chạy độc lập, không ảnh hưởng lẫn nhau.
  
  - Tiết kiệm tài nguyên: Container nhẹ hơn máy ảo vì không cần hệ điều hành riêng.
  
  - Dễ bảo trì: Việc cập nhật, thay thế hoặc rollback phiên bản trở nên đơn giản.
  
  - Dễ sao lưu và phục hồi: Dữ liệu có thể lưu trong volume và backup dễ dàng.
  
  - Hỗ trợ DevOps và CI/CD: Phù hợp với quy trình tự động hóa kiểm thử và triển khai phần mềm.

4. Đã tạo và kiểm thử ứng dụng trên laptop, triển khai lên máy chủ thật không có Internet như thế nào?

Khi ứng dụng đã được phát triển và kiểm thử thành công trên máy tính cá nhân, việc triển khai lên máy chủ không có kết nối Internet cần được thực hiện theo quy trình đặc biệt. Do máy chủ không thể tải image hoặc cài đặt các thành phần từ Docker Hub nên toàn 
bộ dữ liệu cần thiết phải được chuẩn bị trước trên máy có Internet.

Bước 1: Hoàn thiện và kiểm thử ứng dụng

Trước khi triển khai, cần đảm bảo ứng dụng hoạt động ổn định trên máy cá nhân. Người phát triển phải kiểm tra đầy đủ các chức năng, kết nối cơ sở dữ liệu, các dịch vụ liên quan và file cấu hình Docker Compose. Việc kiểm thử trước giúp giảm nguy cơ phát sinh 
lỗi khi đưa ứng dụng lên môi trường thực tế.

Bước 2: Đóng gói ứng dụng và các Docker Image

Sau khi ứng dụng hoạt động ổn định, tiến hành build Docker Image cho ứng dụng và xác định toàn bộ các image mà hệ thống sử dụng như Web Server, Database, Monitoring hoặc các dịch vụ hỗ trợ khác. Các image này được xuất ra thành các file lưu trữ để có thể mang 
sang máy chủ không có Internet. Đồng thời cần chuẩn bị đầy đủ mã nguồn, file cấu hình, file docker-compose.yml và dữ liệu sao lưu nếu có.

Bước 3: Chuyển dữ liệu sang máy chủ

Toàn bộ image Docker, mã nguồn và các file cấu hình được sao chép sang máy chủ bằng USB, ổ cứng di động hoặc thông qua mạng nội bộ. Đây là bước quan trọng vì máy chủ không thể tự tải dữ liệu từ Internet. Mọi thành phần cần thiết cho việc vận hành hệ thống phải được chuẩn bị đầy đủ từ trước.

Bước 4: Cài đặt Docker và triển khai hệ thống

Trên máy chủ, tiến hành cài đặt Docker và Docker Compose bằng bộ cài offline đã chuẩn bị sẵn. Sau đó nạp các Docker Image vào hệ thống, kiểm tra lại cấu hình mạng, volume và các biến môi trường. Khi mọi thứ đã sẵn sàng, sử dụng Docker Compose để khởi động toàn bộ ứng dụng

Bước 5: Kiểm tra và vận hành

Sau khi triển khai thành công, cần kiểm tra trạng thái hoạt động của các container, khả năng kết nối giữa các dịch vụ và khả năng truy cập từ người dùng. Nếu ứng dụng sử dụng cơ sở dữ liệu, cần khôi phục dữ liệu từ các bản sao lưu đã chuẩn bị trước. Cuối cùng cấu hình cơ chế tự khởi động và sao lưu định kỳ để đảm bảo hệ thống hoạt động ổn định trong thời gian dài.

# B. THỰC HÀNH ÁP DỤNG

  APP MONITOR + ALERT DATA REALTIME

1. Mô hình hệ thống cần làm

  Hệ thống gồm các service:
  
  Node-RED
  
  MariaDB
  
  InfluxDB
  
  Grafana
  
  Flask API
  
  Nginx
  
  Frontend HTML + JS + CSS
  
  Telegram Bot
  
  Luồng hoạt động:
  
  Node-RED lấy dữ liệu realtime
          ↓
  Lưu giá trị mới nhất vào MariaDB
          ↓
  Lưu lịch sử vào InfluxDB
          ↓
  Flask API đọc dữ liệu mới nhất từ MariaDB
          ↓
  Nginx chạy web HTML + JS + CSS
          ↓
  Web gọi API Flask để hiển thị dữ liệu realtime
          ↓
  Grafana đọc InfluxDB để vẽ biểu đồ lịch sử
          ↓
  Node-RED kiểm tra bất thường
          ↓
  Nếu ALERT thì gửi Telegram

Bước1. Kiểm tra mạng Ubuntu

  Trong Ubuntu chạy:
  
  Hostname -I
  
  Ghi lại IP của Ubuntu,:

<img width="601" height="77" alt="image" src="https://github.com/user-attachments/assets/b1c44e4c-037d-4717-93db-96a12d69b21a" />

Bước 2. Cài Docker trên Ubuntu

  Chạy lần lượt:
  
    sudo apt update
    
    sudo apt install -y docker.io docker-compose-plugin git nano curl

<img width="691" height="242" alt="image" src="https://github.com/user-attachments/assets/db16aac4-04cd-4c1a-b6e8-5c4449b3ce36" />

Bật Docker:

  sudo systemctl enable docker
  
  sudo systemctl start docker

<img width="691" height="80" alt="image" src="https://github.com/user-attachments/assets/15c8bd40-7330-45a3-8f8e-38332a719aa3" />

Kiểm tra:

  docker --version
  
  docker compose version

<img width="522" height="162" alt="image" src="https://github.com/user-attachments/assets/43c7686d-6a34-48a3-a564-8155e2375c03" />

Cho user hiện tại dùng Docker không cần sudo:

  sudo usermod -aG docker $USER

Sau đó logout Ubuntu rồi login lại, hoặc chạy:

  newgrp docker

Kiểm tra:

  docker ps

<img width="692" height="174" alt="image" src="https://github.com/user-attachments/assets/e2581d7b-124c-432d-8cc2-658248a4110b" />

Bước 3. Tạo thư mục project trên Ubuntu

  cd ~
  
  mkdir bt5_monitor_realtime
  
  cd bt5_monitor_realtime
  
  mkdir flask-api frontend nginx

Kiểm tra:

  Ls

<img width="691" height="125" alt="image" src="https://github.com/user-attachments/assets/26a82a92-543c-4702-8868-8f341e025907" />

Bước 4. Tạo file docker-compose.yml

  nano docker-compose.yml

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/c80e570c-8e98-4bbf-9984-035f3a614996" />

Bước 5. Tạo database MariaDB

  nano flask-api/init.sql

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/110c602f-a34d-49d8-97ca-cde61ea07f27" />

Bước 6. Tạo Flask API

  nano flask-api/app.py

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/a7b30f53-1901-4e70-9143-cc38fe1ca4f6" />

* Tao file : nano flask-api/requirements.txt

<img width="642" height="331" alt="image" src="https://github.com/user-attachments/assets/8251d900-d587-4cd7-bbde-a8a2ff16d32f" />

* Tạo file : nano flask-api/Dockerfile

<img width="692" height="467" alt="image" src="https://github.com/user-attachments/assets/da6043bf-8f49-42e9-b7ad-fe9eac42438d" />

Bước 7. Tạo Nginx config

  nano nginx/default.conf

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/a956657b-1b06-447a-968c-f61a7d5c776a" />

Bước 8. Tạo web HTML + CSS + JS

  nano frontend/index.html

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/c232eac2-3c48-4eed-9b84-c2f322bfd31c" />

8 Tạo file : nano frontend/style.css

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/a62aabd9-af70-477c-b55a-90cc660956f7" />

* Tạo file : nano frontend/script.js

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/b6aaba31-501d-43fc-bc45-d03aa2dda196" />

Bước 9. Chạy hệ thống

Trong thư mục bt5_monitor_realtime:

  docker compose up -d --build

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/b46e13c4-3287-4c23-89b5-70f521bd44c9" />

Kiểm tra:

  docker ps

<img width="691" height="134" alt="image" src="https://github.com/user-attachments/assets/d36c9051-0a1c-4a6f-aaef-14bc4931ac36" />

Bước 10. Truy cập từ máy Windows

  1.Web Frontend (Nginx)
  
    http://192.168.173.101:8080

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/389cc03d-8332-47d6-ad05-dac19f892b96" />

2.Node-RED

    http://192.168.173.101:1880

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/87aca66c-7f5d-4f81-bee9-16c117c1e892" />

3.Grafana

  http://192.168.173.101:300
  
    Tài khoản mặc định thường là:

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/80607fe1-9abc-4bd0-b3b6-911a71fda69f" />

  user: admin
  
  pass: admin

4.Flask API

    http://192.168.173.101:5000/api/realtime

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/9757323b-e0f3-4a0b-b7b9-f6fa698e6a55" />

5.InfluxDB

  http://192.168.173.101:8086

<img width="692" height="390" alt="image" src="https://github.com/user-attachments/assets/f8db3e03-f586-4265-9d29-b72439f09bfa" />

6.MariaDB

  MariaDB không phải web nên không mở bằng trình duyệt.
    
    Kết nối bằng:
 
    Host: 192.168.173.101
      
      Port: 3306

Bước 11. Cấu hình Node-RED

Mở:

  http://192.168.173.101:1880

Cài node:

  Menu → Manage palette → Install
  
    node-red-node-mysql

<img width="692" height="375" alt="image" src="https://github.com/user-attachments/assets/735a3786-d959-4e28-847d-9e1e8fc76c92" />

  node-red-contrib-influxdb

<img width="691" height="350" alt="image" src="https://github.com/user-attachments/assets/8de5aefd-44ea-4a49-b934-c12fd06fb0eb" />

  node-red-contrib-telegrambot

<img width="691" height="324" alt="image" src="https://github.com/user-attachments/assets/f1f54acc-0dcd-41d0-a8a5-0d6e3b047f42" />

* Tạo flow:

inject → http request → function → mysql
                      ↓
                    function → influxdb
                      ↓
                    function → telegram sender

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/ebac6217-e35f-4cb0-ad3e-3c7576e66efc" />

Bước 12. Kiểm tra MariaDB

  docker exec -it bt5_mariadb mariadb -u monitor_user -p

Password:
  
  monitor123

Chạy:

  USE monitor_db;
  
    SELECT * FROM realtime_data;

<img width="691" height="372" alt="image" src="https://github.com/user-attachments/assets/124d5269-1871-40ce-b590-e62b57e8172f" />

Bước 13. Cấu hình InfluxDB trong Node-RED

* Function trước InfluxDB:

<img width="692" height="389" alt="image" src="https://github.com/user-attachments/assets/774dec11-6615-4268-b1d5-b0a4959f2c39" />

* InfluxDB config:

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/b467da0c-c69d-4c05-8a78-37d6dcc6a631" />

Bước 14. Cấu hình Grafana

  Mở:
  
    http://192.168.173.101:3000

Đăng nhập:

  Admin
  
  admin123

<img width="691" height="387" alt="image" src="https://github.com/user-attachments/assets/e0fe7237-8582-409a-91d6-db7be3566b22" />

Thêm Data Source:

  InfluxDB

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/f1a0d55f-18a4-4178-bfd8-77c164cd5ef1" />

* Kết nối Grafana

<img width="691" height="369" alt="image" src="https://github.com/user-attachments/assets/64e1766f-326c-4b3d-908c-f91bf00783bd" />

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/bf03b43b-b0fc-4864-92da-488e18e2fedc" />

Bước 15: Telegram Alert

  Tạo bot bằng:
  
  @BotFather
  
    Thêm bot vào group.

Thêm thành viên:

    1875746636

Lấy chat_id:

    https://api.telegram.org/botTOKEN_CUA_BAN/getUpdates
    
    Function Telegram trong Node-RED:

<img width="692" height="395" alt="image" src="https://github.com/user-attachments/assets/3e55efd6-b49e-4318-b54c-1a8876336e50" />

Node telegrams

<img width="691" height="387" alt="image" src="https://github.com/user-attachments/assets/86a53b16-c076-4923-91de-8bd41216084f" />

* Kết quả chả về

<img width="567" height="434" alt="image" src="https://github.com/user-attachments/assets/67eb47f3-7f56-4c6a-a4b9-a073eb0e4273" />

Bước 16. Xuất image ra file nén

  docker images

<img width="692" height="226" alt="image" src="https://github.com/user-attachments/assets/f4cf2006-6eb4-4405-a525-1dddb4a9bd57" />

  docker save -o bt5_images.tar \
  
  mariadb:latest \
  
  influxdb:2.7 \
  
  grafana/grafana:latest \
  
  nodered/node-red:latest \
  
  nginx:latest \
  
  bt5-flask-api:latest

<img width="647" height="182" alt="image" src="https://github.com/user-attachments/assets/0ac5ebaf-b5a5-4498-bba7-ce1217778519" />

gzip bt5_images.tar

<img width="622" height="127" alt="image" src="https://github.com/user-attachments/assets/0ddd8440-44e4-43a6-a933-af2241950223" />

Bước 17. Xóa container

  Lệnh 1: Dừng và xóa toàn bộ các dịch vụ định nghĩa trong file compose
  
    docker compose down

<img width="691" height="119" alt="image" src="https://github.com/user-attachments/assets/063567b9-4c26-4a2e-bb91-0ab7e6c27618" />

  Lệnh 2 : Cưỡng chế xóa sạch toàn bộ container rác còn sót lại
  
    docker rm -f $(docker ps -aq)

<img width="693" height="275" alt="image" src="https://github.com/user-attachments/assets/89338f60-62cd-4839-a5cd-7da211c6d1cb" />

docker ps -a

<img width="691" height="134" alt="image" src="https://github.com/user-attachments/assets/7f9a94b8-a2c1-430c-b250-7bef7978c5a9" />

Bước 18. Load lại image và khôi phục

  Lệnh 1: Giải nén file .tar.gz về lại file .tar
  
    gunzip bt5_images.tar.gz

<img width="691" height="107" alt="image" src="https://github.com/user-attachments/assets/4f820ffd-b7e2-4905-b159-cb767319e074" />

  Lệnh 2: Nạp (Load) các Image từ file .tar vào Docker
  
    docker load -i bt5_images.tar

<img width="691" height="85" alt="image" src="https://github.com/user-attachments/assets/59eee6e9-b58f-4042-b6e8-8bb912ab65e2" />

  docker compose up -d
  
  docker ps

<img width="691" height="114" alt="image" src="https://github.com/user-attachments/assets/92103809-93f4-49cf-bd57-39e36bd7958f" />

* Kết quả đạt được

<img width="691" height="347" alt="image" src="https://github.com/user-attachments/assets/d85e8351-5088-45c6-9c41-0676d4e98fad" />

* Sửa dữ liệu grafana

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/a7561311-54da-40d9-b5dc-06a9240b7e13" />

* Cấu hình domain

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/72f946a0-97d8-4446-b048-d3e8d96c1312" />

# Két quả đạt được cuối cùng 

<img width="691" height="389" alt="image" src="https://github.com/user-attachments/assets/77080143-1b41-4efe-a0f6-ea6dc6073bfe" />

* Biểu đồ hiển thị lịch sử 

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/cd28d3df-1154-4d9a-b881-bff30389fbad" />




































