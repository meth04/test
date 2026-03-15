# Handoff triển khai demo storefront POD trung gian — LụaMây Studio

## 1) Đã thay đổi gì
- Dựng cấu trúc theme Online Store 2.0 tối giản gồm:
  - `layout/theme.liquid`
  - `templates/index.json`, `templates/collection.json`, `templates/product.json`
  - Sections: `announcement-bar`, `header`, `home-pod`, `main-collection-pod`, `main-product-pod`, `chatbot-entry`, `footer`
  - `assets/base.css` cho visual hệ thống
  - `config/settings_schema.json` cho cài đặt thương hiệu, bản địa hoá, AI readiness
- Mặc định nội dung tiếng Việt, định vị thương hiệu premium, thân thiện, tin cậy.

## 2) Cấu trúc trang chủ
Trang chủ (`home-pod`) đã gồm:
1. Hero + CTA chuyển đổi
2. Danh mục nổi bật (block động)
3. Quy trình đặt hàng 5 bước cho mô hình trung gian
4. Trust/reassurance cards
5. Inspiration gallery placeholder
6. AI image/mockup placeholder states
7. FAQ preview

## 3) Trang sản phẩm POD
`main-product-pod` hỗ trợ luồng yêu cầu cá nhân hoá:
- Gallery media sản phẩm
- Giá, biến thể, số lượng
- Trường bắt buộc/tuỳ chọn qua **line item properties**:
  - `Link ảnh tham chiếu` (bắt buộc)
  - `Yêu cầu cá nhân hoá` (bắt buộc)
  - `Phong cách`, `Màu chủ đạo`, `Ghi chú thêm` (tuỳ chọn)
- Khối giải thích rõ luồng trung gian: nhận yêu cầu → duyệt → chuyển đối tác → sản xuất → giao hàng
- Placeholder AI states: “đang xử lý ảnh”, “xem trước mockup”, “cần đội ngũ xác nhận”

## 4) Trang collection/catalog
`main-collection-pod` gồm:
- Header collection + mô tả
- UI sắp xếp cơ bản (frontend placeholder)
- Product cards tối ưu mobile, nhất quán visual

## 5) Những gì merchant có thể tự sửa trong Theme Editor
- Tên thương hiệu, thông điệp, CTA, text các section
- Danh mục nổi bật (thêm/xoá/sửa block)
- Announcement bar
- Footer: liên hệ, newsletter, ghi chú bản địa hoá
- Chatbot teaser CTA
- Màu giao diện chính trong Theme settings

## 6) Localization readiness đã chuẩn bị
- `lang` sử dụng `request.locale.iso_code`
- Vị trí nút selector ngôn ngữ/quốc gia ở header
- Ghi chú vận hành trong `settings_schema.json` để dùng Shopify Markets + Translate & Adapt
- Nội dung tổ chức theo section setting để dịch dễ hơn, hạn chế hardcode

## 7) AI chatbot readiness đã chuẩn bị
- Section `chatbot-entry` (floating teaser) tạo sẵn vùng cho app embed/chat launcher
- Bố cục mobile tránh đè CTA mua hàng bằng cách dùng vị trí và khoảng đệm
- Có CTA hỗ trợ để nối vào live chat/manual support trước khi có AI bot

## 8) AI image/mockup readiness đã chuẩn bị
UI/UX đã có placeholder cho các trạng thái:
- Upload ảnh tham chiếu
- Đang xử lý ảnh
- Xem trước mockup
- Chờ đội ngũ xác nhận

### Data flow dự kiến (tương lai)
1. Khách gửi line item properties + link ảnh
2. App/backend nhận payload từ cart/order webhook hoặc cart transform
3. Dịch vụ AI xử lý ảnh, tạo mockup/asset preview
4. Trả trạng thái về customer account/portal hoặc email link duyệt
5. Sau duyệt mới chuyển lệnh cho đối tác sản xuất

## 9) Theme-only vs cần app/backend
### Theme-only (đã làm)
- UI/UX storefront
- Form thu thập yêu cầu custom ở product page
- Timeline/FAQ/trust messaging
- Placeholder chatbot + AI mockup states
- Cấu trúc section setting để merchant tự quản trị

### Cần app/backend (chưa làm, bắt buộc cho production)
- Upload file ảnh thực sự (không chỉ link)
- AI xử lý ảnh + tạo mockup preview
- Quản trị vòng đời duyệt yêu cầu (approve/reject/revision)
- Đồng bộ trạng thái đơn giữa Shopify và đối tác sản xuất
- Chatbot AI hội thoại có ngữ cảnh theo đơn hàng
- Tự động đa ngôn ngữ nâng cao theo thị trường

## 10) Gợi ý bước tiếp theo
1. Cài app upload file + lưu trữ media an toàn
2. Tích hợp backend xử lý AI preview (queue + callback)
3. Xây mini portal cho khách theo dõi “đang duyệt / đang sản xuất”
4. Tích hợp app chat có API webhook tới CRM/CS
5. Chuẩn hoá bản dịch EN/JP/KR cho mở rộng thị trường
