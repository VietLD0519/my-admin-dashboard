Kiến trúc tổng quan (Modular Frontend Clean Architecture):

Kiến trúc này thường chia ứng dụng thành các lớp (layers) và các module (features).

Layers (Lớp):

Presentation Layer (Lớp Trình bày): Chứa các UI components (React components), layouts, pages (Next.js pages), và xử lý các tương tác người dùng. Đây là nơi chúng ta sử dụng MUI.
components: Các UI component tái sử dụng (ví dụ: Button, Input, Card).
layouts: Các cấu trúc layout chung cho các trang (ví dụ: AdminLayout, AuthLayout).
pages: Các trang của ứng dụng (Next.js page router hoặc app router).
modules (hoặc features): Chứa các UI component và logic cụ thể cho từng tính năng (ví dụ: users, products, orders). Mỗi module có thể có cấu trúc con riêng (components, hooks, utils).
Domain Layer (Lớp Nghiệp vụ): Chứa các entities (thực thể), use cases (trường hợp sử dụng), và business logic thuần túy, không phụ thuộc vào framework hay UI.
entities: Định nghĩa cấu trúc dữ liệu cốt lõi của ứng dụng (ví dụ: User, Product).
useCases (hoặc interactors): Logic nghiệp vụ chính, điều phối luồng dữ liệu giữa Presentation và Data Layer.
Data Layer (Lớp Dữ liệu): Chịu trách nhiệm về việc lấy và lưu trữ dữ liệu từ các nguồn khác nhau (API, localStorage, etc.).
repositories: Interfaces định nghĩa cách tương tác với dữ liệu.
services (hoặc adapters, dataSources): Implementations của repositories, xử lý việc gọi API, tương tác với localStorage, etc.
models: Cấu trúc dữ liệu trả về từ API (có thể khác với entities).
Modular (Features):

Mỗi tính năng lớn của dashboard (ví dụ: quản lý người dùng, quản lý sản phẩm, phân tích) sẽ là một module riêng biệt.
Mỗi module sẽ có cấu trúc thư mục riêng, chứa các components, pages, use cases, và services liên quan đến tính năng đó. Điều này giúp tách biệt logic và dễ dàng quản lý.

/src
|-- /app (Nếu dùng App Router của Next.js)
|   |-- /api # Route handlers cho backend (nếu cần)
|   |-- /(admin) # Nhóm route cho dashboard admin
|   |   |-- /dashboard
|   |   |   |-- page.tsx
|   |   |-- /users
|   |   |   |-- page.tsx
|   |   |   |-- /components
|   |   |   |-- /[userId]
|   |   |       |-- page.tsx
|   |   |-- layout.tsx # Layout chung cho admin
|   |-- /login
|   |   |-- page.tsx
|   |-- layout.tsx # Root layout
|   |-- globals.css
|-- /components # UI components dùng chung, không thuộc module nào
|   |-- /common
|   |   |-- Button.tsx
|   |   |-- InputField.tsx
|   |-- /layout
|       |-- AdminLayout.tsx
|       |-- AuthLayout.tsx
|-- /contexts # React Contexts (ví dụ: AuthContext, ThemeContext)
|-- /constants # Các hằng số
|-- /core # Các logic cốt lõi, không thuộc module nào cụ thể
|   |-- /domain
|   |   |-- /entities
|   |   |   |-- User.ts
|   |   |-- /useCases # Use cases dùng chung hoặc cơ bản
|   |-- /data
|       |-- /repositories # Interfaces cho repositories
|       |   |-- IAuthRepository.ts
|       |-- /services # Implementations của repositories (API calls)
|       |   |-- AuthService.ts
|       |-- /models # Data models từ API
|-- /features # Hoặc /modules - Chứa các module tính năng
|   |-- /auth
|   |   |-- /components
|   |   |   |-- LoginForm.tsx
|   |   |-- /services # Các hàm gọi API liên quan đến auth
|   |   |-- /hooks # Custom hooks cho auth
|   |   |-- /utils
|   |-- /users
|   |   |-- /components
|   |   |   |-- UserTable.tsx
|   |   |   |-- UserForm.tsx
|   |   |-- /pages (Nếu dùng Pages Router) hoặc các route con trong /app
|   |   |-- /services
|   |   |-- /hooks
|   |   |-- /types
|   |-- /products
|       |-- # (Tương tự users)
|-- /hooks # Custom React hooks dùng chung
|-- /lib # Các thư viện helper, utilities dùng chung
|-- /providers # Providers cho Context, Theme, etc.
|-- /store # (Tùy chọn) Nếu dùng state management library như Redux, Zustand
|   |-- /slices # Ví dụ cho Redux Toolkit
|-- /styles # Global styles, theme configuration
|   |-- theme.ts # MUI theme configuration
|-- /types # Global TypeScript types/interfaces
|-- /utils # Utility functions dùng chung
next.config.js
tsconfig.json
package.json
