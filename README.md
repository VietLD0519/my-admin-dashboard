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
