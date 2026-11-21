# Báo cáo cá nhân — Ngày 11
Họ tên: Nguyễn Thái Dương               Mã học viên: 2A202603207  
Phiên bản CVAT (Help → About): v2.74.1 — CVAT chạy local bằng Docker theo chỉ định của lab coach (không dùng CVAT lớp)  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-21 14:21 (front), 14:33 (fisheye)    Số lần nộp lại sau Rework: 0  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Có | Tạo project `d11-road-nguyenthaiduong` bằng cách dán `configs/road_v1_labels.json` vào tab Raw: lane, road_curb (polyline), crosswalk, drivable (polygon), traffic_light, traffic_sign (rectangle) |
| Thuộc tính và giá trị | Có | Khớp với `python -m road_lab.taxonomy` |
| 4 tag ảnh | Có | camera, timeofday, weather, source — mỗi tag một thuộc tính select `value` |

Cách kết thúc polyline trên bản CVAT này: bấm phím **N** sau điểm cuối.  
Cách đặt tag ảnh trên bản CVAT này: chọn công cụ hình cái nhãn (Setup tag) ở thanh bên trái → chọn label → bấm nút **+** → mở Details của tag trong bảng Objects để chọn `value`.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 23 | 16 | 13 | 21 | 26 | 13 |
| front-extra (đã làm 0 / 4) | 0 | — | — | — | — | — | — |
| fisheye | 8 | 9 | 11 | 10 | 11 | 2 | 2 |
| fisheye-extra (đã làm 0 / 4) | 0 | — | — | — | — | — | — |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | lane L1/R1 | Vẽ L1/R1 hay không | Không vẽ | Đường không có vạch sơn; chỉ vẽ road_curb + drivable. Cần coach xác nhận để miễn QC1-02 |
| A07 | lane L1 | Có L1 hay không | Không vẽ | Bên trái làn là bờ bê tông, không thấy vạch sơn. Cần coach xác nhận |
| A09 | lane R1 | Có R1 hay không | Không vẽ | Bên phải làn là mép vỉa, không có vạch sơn. Cần coach xác nhận |
| A04 | lane L1 vàng đôi | Hai polyline (mỗi nét một đường) hay một polyline | Một polyline, `kind = double` | Guideline: lane là "một vạch kẻ làn"; vạch 1.3 đôi liền là kind double. Đặt polyline giữa hai nét |
| A03 | tag timeofday | day hay dusk | dusk | Trời tối dần, ánh sáng yếu |
| B02 | tag camera | fisheye_rear hay fisheye_front | fisheye_front | Ban đầu nhìn ảnh tưởng camera sau; guideline quy định theo hậu tố tên file (FV → fisheye_front), đáy ảnh là cản trước |
| B03 | lane position | L/R theo ảnh hay theo xe ở camera sau | Theo guideline đã chọn khi gán | Camera sau nhìn ngược, trái ảnh là phải xe; guideline chưa nói rõ |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Lê Trung Tá  Quyết định nhận được: __ (chờ phiếu)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
|  |  |  |  |

Tự kiểm bằng `road_check lint` trước khi nộp (bản cuối): đã sửa toàn bộ lỗi thiếu tag (20 ảnh), sai tag camera (B02, B07, B08) và lane camera hai bên chưa là `other` (B06, B07, B08). Còn lại: QC1-02 ở A05, A07, A09 (không có vạch — xem bảng ca khó) và A06, A08, A10, A12 (chưa kịp bổ sung); QC1-11 edge_zone ở B02, B04; B01 thiếu tag source.

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| nguyenthaiduong-front.zip | Có (road_check lint đọc được) | A01: 8 / 8 | A02: 7 / 7 | Có, 12/12 ảnh |
| nguyenthaiduong-fisheye.zip | Có (road_check lint đọc được) | B01: 4 / 4 | B02: 9 / 9 | Có, 8/8 ảnh |

## 6. Ảnh chụp màn hình
1. Tab Labels của project.

![Tab Labels của project](screenshots/01-labels.png)
<img width="1268" height="487" alt="image" src="https://github.com/user-attachments/assets/d66b4849-665b-4890-b9fa-f72559452bcb" />


2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển).

![Ảnh A01 đã gán đủ](screenshots/02-front-A01.png)
<img width="1368" height="760" alt="image" src="https://github.com/user-attachments/assets/e822d102-3aca-4bf7-8185-6416a4fde6f6" />

3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong.

![Ảnh fisheye, polyline cong](screenshots/03-fisheye.png)
<img width="1255" height="558" alt="image" src="https://github.com/user-attachments/assets/fc4c3373-8cd9-474a-8ada-ef6ee6a1a9c6" />


4. Một đoạn XML có `<polyline label="lane">`.

![Đoạn XML có polyline lane](screenshots/04-xml.png)
<img width="1842" height="282" alt="image" src="https://github.com/user-attachments/assets/8936d8b4-1bc3-471d-b487-b6182eae2691" />


## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20: **QC1-01** — bản export đầu tiên không có tag nào ở cả 20 ảnh vì tôi chỉ vẽ shape mà quên đặt tag, và sau đó còn đặt sai camera ở 3 ảnh fisheye do đoán theo hình thay vì đọc hậu tố tên file. Thứ hai là **QC1-03**: lane ở camera hai bên để L1/R1 thay vì `other`. Cách tránh: đặt 4 tag là bước đầu tiên của mỗi ảnh, camera lấy theo tên file; chạy `road_check lint` sau mỗi task chứ không đợi đến cuối.  
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào: Tag camera được dùng để chia dữ liệu theo loại camera (front / fisheye từng hướng) khi huấn luyện và khi đánh giá. Nếu B07, B08 (camera phải) bị gắn `fisheye_left`, ảnh camera phải sẽ lọt vào tập camera trái: model hoặc bước hậu xử lý sẽ dùng sai tham số hiệu chỉnh méo của ống kính, và số liệu đánh giá theo từng camera bị lệch. Tương tự, lane camera hai bên để L1 sẽ dạy model rằng có "làn của xe mình" trong ảnh camera hông, làm sai đầu ra cho hệ giữ làn.
