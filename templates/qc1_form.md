# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): 2A202603259       Người kiểm (học viên):  2A202603247
Ngày: 20/11/2026                        Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest):  A01-A06
Số ảnh kiểm: 6
Số nhãn đã kiểm (shape + tag): 64 mục (43 shape + 21 tag).
Lưu ý: con số này đếm annotation đang có; chưa bao gồm nhãn kỳ vọng có thể bị bỏ sót.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 ô tag kỳ vọng (6 ảnh × 4 tag); đã kiểm 6 camera | 3 tag bị thiếu ở A02; camera sai/thiếu: 0 | nhẹ |
| QC1-02 đủ L1, R1 | bỏ sót | 6 cặp ảnh | 0 xác nhận; 1 nghi vấn R1 ở A06 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 14 polyline lane | 0 xác nhận; giá trị thuộc tính hợp lệ | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 14 polyline lane | 0 xác nhận; chưa đo độ lệch pixel bằng GT | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 14 polyline lane | 0 xác nhận; cần kiểm thêm các đoạn bị che | chính |
| QC1-06 style, color, kind | sai thuộc tính | 14 polyline lane | 0 xác nhận qua kiểm tra sơ bộ | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 13 shape (11 drivable, 1 crosswalk, 1 road_curb) | 0 xác nhận; 2 vùng drivable cần xác minh | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 8 box đèn | 0 xác nhận qua kiểm tra sơ bộ | nặng/chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 8 box biển | 0 xác nhận; chưa đối chiếu từng biển với GT | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 8 box biển | 0 xác nhận; chưa thể xác nhận đủ mọi biển nếu thiếu GT | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 ảnh fisheye | Không áp dụng cho mẫu A01–A06 | không áp dụng |
| QC1-12 file | lỗi file | 1 annotations.xml; chưa kiểm hai file zip bàn giao | chưa xác minh export/lint/manifest | chưa kết luận |

*Theo thang QC1, thiếu tag `timeofday`, `weather`, `source` là lỗi nhẹ; chỉ camera sai hoặc thiếu mới là lỗi nặng.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-01 | A02_b3c26aff-63a0d7d6 | tag `timeofday` | nhẹ | Thiếu Tag  |
| 2 | QC1-01 | A02_b3c26aff-63a0d7d6 | tag `weather` | nhẹ | Thiếu Tag  |
| 3 | QC1-01 | A02_b3c26aff-63a0d7d6 | tag `source` | nhẹ | Thiếu Tag |
| 4 | QC1-07 | A01_bc5fadac-fa6dd225 | polygon `drivable`, polygon thứ 2 gán `direct` | chính  | Vùng polygon phía phải có vẻ nằm ngoài làn đang đi; kiểm tra có phải làn cùng chiều bên cạnh và cần đổi `area_type` thành `alternative` không. |
| 5 | QC1-07 | A03_b1c66a42-6f7d68ca | polygon `drivable`, polygon `direct` | chính  | Polygon kết thúc tại y=690; kiểm tra phần đường phía dưới có bị bỏ sót không, hoặc có thuộc vùng thân xe/không gán hay không. |
| 6 | QC1-02 | A06_b8c66e31-37045eec | lane; không có id shape  | nặng | Xác nhận R1 có nhìn thấy được trong ảnh không; không vẽ thêm nếu thực sự không có vạch. |


## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A01 | Polygon drivable thứ 2 gán `direct` có thuộc làn đang đi hay làn cùng chiều bên cạnh (`alternative`)? | Thuộc làn cùng chiều lên là alternative |
| A03 | Phần ảnh dưới car có mặt đường cần gán `drivable`, hay thuộc vùng không gán? | Vẫn cần gán đến sát car vì thuộc mặt đường đã gán  `drivable`|
| A06 | Có thấy được vạch R1 không? Nếu không thấy, QC1-02 không được tính là lỗi. | Không thấy vạch R1 |
| A03 | `weather=clear` có đúng không, hay bầu trời nhiều mây nên chọn `overcast`? | Bầu trời có thể vừa chọn clear hoặc overcast đều được |

## Quyết định

Lỗi nặng: 0 
Lỗi chính: 2 ở A01 và A03
Tỉ lệ lỗi chính: 2 / 64 × 100 = 3,125% ≈ 3,13%
Lỗi nhẹ: 3 tag bị thiếu ở A02
Ca chờ lead: 0

Quyết định (Release / Hold / Rework): Release
Lý do: Không còn lỗi nặng. Tỉ lệ lỗi chính là 2 / 64 = 3,13%, không vượt ngưỡng 5%. Ba lỗi nhẹ ở các tag không bắt buộc không làm thay đổi điều kiện quyết định. Các ca mơ hồ đã được xác nhận.