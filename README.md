# Web thuê gia sư online và mua khóa học

Ứng dụng web kết nối học viên với gia sư. Project gồm:

- **Frontend:** React + Vite
- **Backend:** Java 21 + Spring Boot
- **Database:** PostgreSQL chạy bằng Docker

## Cần cài trước

- [Node.js](https://nodejs.org/) (18 trở lên)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- Java 21 (không cần cài Maven riêng vì project có Maven Wrapper)

## Cài đặt lần đầu

### 1. Cấu hình backend

Tạo file `.env` trong thư mục `Backend\Web thue gia su online` với nội dung sau. Thay các giá trị viết trong dấu `<...>` bằng thông tin được cấp; không chia sẻ hoặc đưa các thông tin này lên Git:

```env
URL=jdbc:postgresql://localhost:5434/giasu
USERNAME=postgres
PASSWORD=123456
FRONTEND_URL=http://localhost:3000
BACKEND_URL=http://localhost:10000/giasu
SIGNER_KEY=<chuoi-bi-mat-ngau-nhien-it-nhat-32-ky-tu>
MAIL_FROM=<email-gui>
GMAIL_CLIENT_ID=<gmail-client-id>
GMAIL_CLIENT_SECRET=<gmail-client-secret>
GMAIL_REFRESH_TOKEN=<gmail-refresh-token>
```

Các giá trị database ở trên khớp với cấu hình Docker có sẵn. Các giá trị Gmail và `SIGNER_KEY` cần được cấp hoặc tạo theo hướng dẫn của nhóm dự án.

### 2. Cài thư viện frontend

Mở Terminal tại thư mục gốc của project và chạy:

```powershell
cd "Frontend\Web-thue-gia-su-fe"
npm install
```

## Chạy project

Mở **hai cửa sổ Terminal** tại thư mục gốc project.

### Terminal 1: Database và backend

```powershell
cd "Backend\Web thue gia su online"
docker compose up -d postgres
.\mvnw.cmd spring-boot:run
```

Lần đầu chạy, Docker sẽ tạo PostgreSQL và nạp dữ liệu khởi tạo. Giữ cửa sổ này mở để backend tiếp tục hoạt động.

### Terminal 2: Frontend

```powershell
cd "Frontend\Web-thue-gia-su-fe"
npm run dev
```

Mở ứng dụng tại **http://localhost:3000**. Frontend sẽ chuyển các API request đến backend đang chạy tại **http://localhost:10000/giasu**.

## Tắt project

- Nhấn `Ctrl + C` trong từng cửa sổ Terminal để dừng backend và frontend.
- Tắt PostgreSQL bằng lệnh sau (chạy tại thư mục backend):

```powershell
docker compose down
```

## Nếu gặp lỗi

- Kiểm tra Docker Desktop đang mở và cổng `5434`, `3000`, `10000` không bị ứng dụng khác sử dụng.
- Nếu backend báo thiếu cấu hình, kiểm tra file `.env` nằm đúng trong thư mục backend và đã điền đủ giá trị.
- Nếu frontend báo thiếu package, chạy lại `npm install` trong thư mục frontend.
