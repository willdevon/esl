# ESL – Trang thông tin sản phẩm

Trang web tĩnh (GitHub Pages) mà **mã QR trên nhãn giá E-ink** trỏ tới. Thuộc Đồ án 2: *Hệ thống cập nhật thông tin và mã QR sản phẩm trên màn hình E-ink ứng dụng mạng Bluetooth Mesh*.

- Trang: **https://willdevon.github.io/esl/** (danh sách sản phẩm)
- Một sản phẩm: `https://willdevon.github.io/esl/?SP001` — đây là chuỗi gateway nạp vào QR trên nhãn
- Hiển thị: tên, giá (gạch giá cũ khi đang khuyến mãi), ngày sản xuất, hạn sử dụng (còn bao nhiêu ngày), xuất xứ, thành phần

```
Nhãn E-ink (QR) ──quét bằng 4G──► index.html ──đọc──► products.json
                                                        ▲
Web gateway (Node 1) ── "Xuất dữ liệu cho GitHub Pages" ┘  (upload thủ công)
```

## Nội dung repo

| File | Vai trò |
|---|---|
| `index.html` | Hiển thị sản phẩm theo `?<mã>`; không có mã thì liệt kê tất cả. Giá KM tự hết hiệu lực theo ngày trên máy khách |
| `products.json` | Dữ liệu sản phẩm xuất từ web gateway. **Không chứa giá vốn** hay dữ liệu nội bộ |

Repo này **chỉ** chứa trang công khai. Code firmware, web gateway và tài liệu nằm ở repo private của nhóm (`Phuhungk23/Doan2`, thư mục `github_pages/` là bản nguồn của trang này).

## Cập nhật dữ liệu sau khi đổi giá / thông tin

1. Web gateway (`http://192.168.4.1`) → tab **Cập nhật giá** → **Xuất dữ liệu cho GitHub Pages (products.json)**.
2. Repo này → **Add file → Upload files** → kéo thả `products.json` (ghi đè) → **Commit changes**.
3. Khoảng 30–60 giây sau trang hiện dữ liệu mới.

## Đổi địa chỉ trang

QR trên nhãn = `CONFIG_ESL_QR_BASE_URL` + mã SP (menuconfig gateway → *ESL Gateway → Web*), hiện là `https://willdevon.github.io/esl/?`. Chuỗi QR tối đa 64 ký tự. Đổi xong: nạp lại gateway, rồi import lại file Excel có **cột QR để trống** để các nhãn nhận QR mới.
