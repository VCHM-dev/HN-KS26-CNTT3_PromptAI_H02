# BÀI LÀM PHA 2 – HACKATHON 02

- **Mã đề:** 09
- **Họ tên:** Nguyễn Thái Hoàng
- **Lớp:** CNTT3
- **Link repository Pha2:** https://github.com/VCHM-dev/HN-KS26-CNTT3_PromptAI_H02
- **Công cụ AI đã dùng (ChatGPT/Claude/Gemini):** Gemini ( gehihi :cat: )

> Pha 2 (20 phút cuối). Mỗi mục: mở cuộc trò chuyện mới, gửi nguyên văn prompt đã viết trong bai_lam_pha1.md, dán câu trả lời và link chia sẻ vào đây. Xong, kéo thả file này vào repository Pha2.

## 4.2. Trích xuất tin nhắn đặt chỗ workshop ra JSON

**KET QUA AI**

```text
[
  {
    "ma_lop": "NANTAY",
    "ngay_hoc": "2026-12-13",
    "nguoi_lon": 2,
    "tre_em": 1,
    "ca_hoc": "chieu",
    "ghi_chu": null
  },
  {
    "ma_lop": "BANXOAY",
    "ngay_hoc": "2027-01-10",
    "nguoi_lon": 3,
    "tre_em": 0,
    "ca_hoc": null,
    "ghi_chu": "1 người bị đau cổ tay"
  },
  {
    "ma_lop": "VEGOM",
    "ngay_hoc": null,
    "nguoi_lon": 4,
    "tre_em": 0,
    "ca_hoc": "sang",
    "ghi_chu": "1 bạn đi xe lăn"
  }
]
```

**Link trò chuyện:** https://share.gemini.google/OrI1rSLCTGnu

## 4.3. Báo giá bằng Chain-of-Thought

**KET QUA AI**

```text
```python
adult_price = 550000
adults = 5
children_6_12 = 2 # 8 and 12 years old
children_under_6 = 1 # 4 years old

adult_total = adults * adult_price
child_price = 0.7 * adult_price
child_total = children_6_12 * child_price + children_under_6 * 0
tuition_total = adult_total + child_total

discount = 0.05 * tuition_total if adults >= 5 else 0
tuition_after_discount = tuition_total - discount

shipping_fee = 4 * 80000
grand_total = tuition_after_discount + shipping_fee

print(f"adult_total: {adult_total:,.0f}")
print(f"child_total: {child_total:,.0f}")
print(f"tuition_total: {tuition_total:,.0f}")
print(f"discount: {discount:,.0f}")
print(f"tuition_after_discount: {tuition_after_discount:,.0f}")
print(f"shipping_fee: {shipping_fee:,.0f}")
print(f"grand_total: {grand_total:,.0f}")


```

```text
adult_total: 2,750,000
child_total: 770,000
tuition_total: 3,520,000
discount: 176,000
tuition_after_discount: 3,344,000
shipping_fee: 320,000
grand_total: 3,664,000


```

1. **Tiền người lớn:**
5 × 550.000 = 2.750.000 đồng
2. **Tiền trẻ em:**
2 trẻ em (8 tuổi và 12 tuổi, thuộc nhóm 6–12 tuổi) tính 70% giá người lớn; 1 bé 4 tuổi (dưới 6 tuổi) miễn phí:
2 × (550.000 × 70%) + 1 × 0 = 2 × 385.000 + 0 = 770.000 đồng
3. **Tiền học:**
2.750.000 + 770.000 = 3.520.000 đồng
4. **Giảm giá nhóm:**
Nhóm có đủ 5 người lớn nên được giảm 5% trên tổng tiền học:
3.520.000 × 5% = 176.000 đồng
5. **Phí nung và giao:**
4 × 80.000 = 320.000 đồng
6. **Tổng tiền:**
(3.520.000 − 176.000) + 320.000 = 3.344.000 + 320.000 = 3.664.000 đồng

[RESULT: 3.664.000 đồng]
```

**Link trò chuyện:** https://share.gemini.google/YGVIFznM9Lt1

### b) Kiểm tra kết quả AI

AI đúng

## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
```json
{
  "loai_su_co": "hong_san_pham",
  "so_khach": 3,
  "so_san_pham_bi_hong": 5,
  "tom_tat": "Hoàn 750.000 đồng cho 5 sản phẩm bị nứt vỡ, cần Quản lý xưởng duyệt trước khi gửi khách."
}

```
```

**Link trò chuyện:** https://share.gemini.google/AzeKrv35ULVJ

## 4.5. Prompt chấm bài theo Rubric

**KET QUA AI**

```text
| Tiêu chí | Điểm | Minh chứng | Đề xuất sửa |
| --- | --- | --- | --- |
| **Đúng thông tin (50%)** | 0/5.0 | Báo sai giá ("200k" thay vì 250.000 đồng/người lớn) và sai chính sách đổi lịch ("đổi trước 1 ngày thì free" trong khi đổi trước 24 giờ nằm trong khung 12 đến dưới 48 giờ, mất phí 30.000 đồng/người). | Sửa lại chính xác: Giá lớp vẽ gốm (VEGOM) là **250.000 đồng/người lớn**; đổi lịch trước giờ học **1 ngày (24 giờ)** sẽ áp dụng phí **30.000 đồng/người** (chỉ miễn phí khi đổi trước từ 48 giờ trở lên). |
| **Đầy đủ (30%)** | 1.5/3.0 | Đã trả lời được 2 ý hỏi của khách (dù sai thông tin) nhưng **thiếu** phần mời khách cung cấp ngày học, ca học và số lượng người để đặt chỗ. | Bổ sung lời mời đặt chỗ ở cuối tin nhắn: *"Chị vui lòng cho em xin thông tin về ngày học, ca học và số lượng người tham gia để bên em hỗ trợ giữ chỗ cho mình nhé."* |
| **Giọng điệu (20%)** | 0.5/2.0 | Sử dụng nhiều từ ngữ suồng sã, thiếu chuyên nghiệp (*"Hi chị ơi"*, *"200k thôi nè"*, *"vui lắm luôn"*, *"free nha chị"*, *"nhắn em nha"*). | Chuyển sang văn phong lịch sự, chuẩn mực: dùng *"Dạ chào chị"*, *"250.000 đồng"*, *"miễn phí"*, *"liên hệ với bên em ạ"*. |

**Tổng điểm: 2.0/10**
```

**Link trò chuyện:** https://share.gemini.google/2yM1Q6cWGFrH
