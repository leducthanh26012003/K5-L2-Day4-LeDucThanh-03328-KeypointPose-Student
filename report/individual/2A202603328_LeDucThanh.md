# Báo cáo cá nhân — LeDucThanh-2A202603328

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên:Lê Đức Thanh
- MSSV:2A202603328
- Email:leducthanh26012003@gmail.com
- Link repository: https://github.com/leducthanh26012003/K5-L2-Day4-LeDucThanh-03328-KeypointPose-Student
- Phiên bản CVAT (Help → About): 2.74.1
- Máy: hệ điều hành Windows · RAM 15.7 GB · chạy CVAT chế độ đầy đủ
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có (MSSV 2A202603328, pool `d04-k5-v2`)
- Giờ bắt đầu:16:30
- Giờ kết thúc:18:00

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` | Skeleton | 17 | Có | Có | 19 |
| `face` | Skeleton | 13 | Có | Có | 13 |

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? Có

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu):

- Right click chọn `occluded` / `outside` hoặc trỏ chuột vào chỗ cần chọn rồi bấm `Q` / `O`.

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 | 5 | | | 10|
| `occluded` | 3 |7 | | | 5|
| `back` | 2 | 3| | | 10|
| `small` | 1 |1 | 2| 0|5|
| `crowd` | 1 | 3| 0|0|15|
| `faces` | 8 |8| — |0|30|

- Số ảnh người đã xong ở mốc phút 105: 10 / 10
- Thời gian thực tế (phút): CP1 60 · CP2 30 · CP3 15
- Ảnh tốn thời gian nhất là 000000193879.jpg vì có nhiều người gán, phải quan sát kĩ và đoán nhiều.

## 3. Bảng ca khó (CP1, CP2)

Mỗi điểm bạn phân vân một dòng, nhất là phân vân giữa `v = 1` và `v = 0`, hoặc không chắc hướng người.

| Ảnh | Người / mặt | Điểm | Cờ đã chọn | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
| 000000431988.jpg| person271| left_eye| right_ear|0 |không thể xác định vị trí |
| 000000365099.jpg| | | | | |
| | | | | | |

## 4. Bảng tự review (CP3)

Đi từ ảnh cuối về ảnh đầu. 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Ít nhất 8 dòng, kể cả dòng `ok`. Ghi lỗi trước, sửa sau.

Mã lỗi dùng đúng một trong: `lr_swap`, `vis_flag`, `position`, `missing`, `extra`, `ok`.

| Ảnh | Người / mặt | Điểm | Mã lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|---|
| face_294580.jpg| face| 1| vis_flag| |Đã sửa |
| 000000043719.jpg| | | ok| | |
| 000000122199.jpg| | | ok| | |
| 000000150192.jpg| | | ok| | |
| 000000184224.jpg| | |ok | | |
| 000000193879.jpg| | | ok| | |
| face_257657.jpg| | | ok| | |
| face_356144.jpg| | | ok| | |

Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
|---:|---:|---:|---:|---:|---:|
| | 1| | | | |

Điểm còn phân vân giữa `v = 1` và `v = 0` (ghi cả hai lựa chọn và lý do chọn):

...

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Tự kiểm tay trong file JSON:

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `LeDucThanh_persons.zip` | `000000122199.jpg`, người #1 | 51 | Có (2 điểm `v = 0`, 4 điểm `v = 1`, 11 điểm `v = 2`) | Có: 15 = 4 + 11 |
| `LeDucThanh_persons.zip` | `000000043719.jpg` (quay lưng), người #1 | 51 | Có (7 điểm `outside` ra `v = 0`: mũi, mắt trái, tai trái, 2 cổ tay, 2 cổ chân) | Có: 10 |
| `LeDucThanh_faces.zip` | `face_178208.jpg` (kính trong), mặt #1 | 39 | Có (13 điểm `v = 2`) | Có: 13 |

Sau khi xuất, CVAT ghi `occluded` thành `v = 1` và `outside` thành `v = 0`. Tọa độ của điểm `outside` trong file là `0, 0` hay tọa độ cũ? Tọa độ cũ (ví dụ `270.13, 375.16, 0` ở `000000122199.jpg` người #1), nên chỉ dựa vào `v` để biết điểm có được dùng hay không.

Hai job đã chuyển sang completed trên CVAT? Có / Không

Dán phần **TÓM TẮT** in ra từ `src/check_submission.py`:

```text
----- TÓM TẮT (dán vào báo cáo mục 5) -----
- File person: LeDucThanh_persons.zip
  Số ảnh: 12 · số skeleton `person`: 19 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000043719=1, 000000122199=2, 000000150192=1, 000000184224=1, 000000193879=3, 000000220045=2, 000000240340=1, 000000292999=1, 000000314154=1, 000000365099=1, 000000431988=2, 000000542160=3
  Cờ v: v=2 244 (76%) · v=1 19 (6%) · v=0 60 (19%)
  num_keypoints trung bình: 13.8
- File face: LeDucThanh_faces.zip
  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_178208=1, face_204787=1, face_257657=1, face_294580=1, face_356144=1, face_41666=1, face_416730=1, face_85624=1
  Cờ v: v=2 95 (91%) · v=1 1 (1%) · v=0 8 (8%)
  num_keypoints trung bình: 12.0
- Ghi chú: 68 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 6
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)
```

Các `[CẢNH BÁO]` còn giữ nguyên và lý do:

...

## 6. Ảnh chụp màn hình

1. Label `person` trong label constructor (đủ 17 điểm có tên):

   ![Label person](images/1_label_person.png)

2. Một người quay lưng đã gán, cờ đã đặt:

   ![Người quay lưng](images/2_nguoi_quay_lung.png)

3. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt:

   ![Khuôn mặt phóng to](images/3_mat_phong_to.png)

4. Một đoạn JSON xuất của một người:

   ![JSON export](images/4_json_export.png)

Nguồn ảnh: COCO val2017 / Wikimedia Commons.

## 7. Tự đánh giá

1. Lỗi bạn mắc nhiều nhất hôm nay, và cách bạn sẽ tránh ở dự án thật:

   không có

2. Một quy tắc bạn đề xuất thêm vào guideline (kèm ảnh ví dụ nếu có):

   không có

3. Nhãn của bạn đi vào model ở đâu? Chọn một lỗi bạn đã sửa và nói nó sẽ làm model học sai thế nào (heatmap, trọng số trong loss, hay bước lật ảnh):

   cờ v sai thì trọng số trong loss sai

## 8. Khó khăn và lỗi kỹ thuật

| Thời điểm | Lỗi | Cách xử lý | Kết quả |
|---|---|---|---|
| Chạy `setup` (CP0) | Chạy `python lab.py setup` ở thư mục cha `E:\Vin AI thuc chien`, báo `can't open file ... lab.py` | `cd` vào thư mục repo rồi chạy lại | `setup` thành công, tạo task `persons-LeDucThanh` (13) và `faces-LeDucThanh` (14) |
| Chụp ảnh 4 (CP4) | File JSON xuất nằm trên một dòng, khó chụp | Định dạng lại (chỉ xuống dòng, không sửa nội dung, không sửa file trong zip) để đọc mảng `keypoints` | Chụp được đoạn JSON của một người |

## Bonus (nếu làm)

Không làm bonus.

## 9. Tài liệu tham khảo và công cụ AI đã dùng

- Tài liệu: `docs/GUIDELINE.md`, `docs/CVAT_CHEATSHEET.md`, `docs/COCO_KEYPOINTS.md`, `CHECKPOINTS.md`, `RUBRIC.md`, `SUBMISSION.md` của repo.
- Công cụ AI: Claude Code (Claude, Anthropic) trong ứng dụng Claude desktop. Dùng để: tra cứu quy định của lab; giải thích khái niệm (cờ `v`, heatmap, trọng số trong loss, bước lật ảnh, ngưỡng 60 px, định dạng COCO Keypoints 1.0); hướng dẫn thao tác CVAT và các lệnh `lab.py`; đọc lỗi khi chạy `setup`; kiểm file xuất bằng script (đếm skeleton theo ảnh, kiểm 51/39 số, `v` và `num_keypoints`); tạo bản JSON xuống dòng để chụp ảnh 4; điền các mục số liệu 0, 1, 2, 5, 8, 9 từ dữ liệu thật.
- Không dùng AI hay model để gán điểm. Mục 3, 4, 7 do tôi tự viết.
