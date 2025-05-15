# 🧱 Modular Frontend Clean Architecture

Kiến trúc này chia ứng dụng thành các **layers (lớp)** và **modules (tính năng)** rõ ràng, dễ mở rộng, bảo trì và tái sử dụng. Phù hợp với các ứng dụng phức tạp như dashboard admin, SaaS app, v.v.

---

## 📐 Tổng quan Layered Architecture

### 1. **Presentation Layer (Lớp Trình Bày)**

Chứa tất cả những gì liên quan đến UI, layout và xử lý tương tác người dùng. Đây là nơi sử dụng **React** và thư viện giao diện như **MUI**.

- `components/`: Các UI components dùng chung (Button, Input, Card, ...)
- `layouts/`: Các cấu trúc layout tổng thể (AdminLayout, AuthLayout, ...)
- `pages/` hoặc `app/`: Các trang chính của ứng dụng theo App Router hoặc Pages Router
- `modules/`: Các UI component và logic UI riêng theo từng tính năng (users, products, ...)

---

### 2. **Domain Layer (Lớp Nghiệp Vụ)**

Chứa các **business logic thuần túy**, không phụ thuộc vào UI hay framework.

- `entities/`: Định nghĩa cấu trúc dữ liệu cốt lõi (User, Product, ...)
- `useCases/`: Logic nghiệp vụ, điều phối giữa UI và Data Layer

---

### 3. **Data Layer (Lớp Dữ Liệu)**

Quản lý việc tương tác dữ liệu (API, localStorage, cache, ...)

- `repositories/`: Định nghĩa giao diện tương tác với dữ liệu
- `services/`: Cài đặt thực tế của repositories (API call, localStorage, ...)
- `models/`: Kiểu dữ liệu phản hồi từ API (khác với `entities` ở Domain Layer)

---

## 🧩 Modular Features Structure

Mỗi **module** là một tính năng độc lập (VD: Auth, Users, Products), có thể chứa toàn bộ logic UI, hooks, services, use cases liên quan. Giúp tăng khả năng tái sử dụng, dễ test, dễ scale.

---

## 📁 Cấu trúc thư mục đề xuất

```bash
/src
├── app/                     # Next.js App Router
│   ├── api/                 # Route handlers cho backend (nếu dùng)
│   ├── (admin)/            # Nhóm route cho dashboard admin
│   │   ├── dashboard/page.tsx
│   │   ├── users/
│   │   │   ├── page.tsx
│   │   │   ├── [userId]/page.tsx
│   │   │   └── components/
│   │   └── layout.tsx      # Layout riêng cho admin
│   ├── login/page.tsx
│   ├── layout.tsx          # Root layout
│   └── globals.css
├── components/
│   ├── common/             # UI components dùng chung
│   │   ├── Button.tsx
│   │   └── InputField.tsx
│   └── layout/
│       ├── AdminLayout.tsx
│       └── AuthLayout.tsx
├── constants/              # Các hằng số toàn cục
├── contexts/               # React Contexts (AuthContext, ThemeContext, ...)
├── core/
│   ├── domain/
│   │   ├── entities/       # Business entities (User.ts, Product.ts)
│   │   └── useCases/       # Use cases thuần nghiệp vụ
│   └── data/
│       ├── repositories/   # Giao diện truy xuất dữ liệu (IAuthRepository.ts)
│       ├── services/       # Gọi API, localStorage (AuthService.ts)
│       └── models/         # Kiểu dữ liệu phản hồi từ API
├── features/               # Các module/tính năng độc lập
│   ├── auth/
│   │   ├── components/
│   │   │   └── LoginForm.tsx
│   │   ├── services/
│   │   ├── hooks/
│   │   └── utils/
│   ├── users/
│   │   ├── components/
│   │   │   ├── UserTable.tsx
│   │   │   └── UserForm.tsx
│   │   ├── pages/
│   │   ├── services/
│   │   ├── hooks/
│   │   └── types/
│   └── products/
│       └── # (Tương tự users)
├── hooks/                  # Custom React hooks dùng chung
├── lib/                    # Helper & utility functions
├── providers/              # Các Context Providers (Theme, Auth, ...)
├── store/                  # State management (Redux, Zustand, ...)
│   └── slices/             # Redux slices nếu dùng Redux Toolkit
├── styles/
│   └── theme.ts            # Cấu hình theme MUI
├── types/                  # Các global TypeScript types/interfaces
├── utils/                  # Các hàm tiện ích chung
├── next.config.js
├── tsconfig.json
└── package.json
