# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Dương Quốc Huy (duongquochuy)       Người kiểm (học viên): Đặng Trung Hiếu (dangtrunghieu)  
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `duongquochuy-front.zip`, revision 1 (sha256 khớp với `duongquochuy-manifest.json`)  
Số ảnh kiểm: 6 (A01, A02, A03, A04, A05, A06) (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 66 (42 shape + 24 tag)  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 1 (+2 chờ lead: A05, A06) | nặng |
| QC1-03 position | sai thuộc tính / thừa | 12 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 12 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 8 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 12 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 15 | 1 (xem thêm ca mơ hồ A01) | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 5 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 8 | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 6 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 | 0 | chính |
| QC1-12 file | lỗi file | 1 | 0 | nhẹ / nặng |

Cách đếm "số mục kiểm": QC1-01 là 6 tag camera; QC1-02 là 6 ảnh cần có L1 và R1; QC1-03, 04, 06 là 12 lane (A01: 4, A02: 3, A03: 2, A04: 3); QC1-05 là 8 vạch đứt; QC1-07 là 15 polygon drivable; QC1-08 là 5 hộp đèn (đều ở A06); QC1-09 là 8 hộp biển (A01: 2, A03: 2, A06: 4); QC1-10 là 6 ảnh; QC1-11 không có ảnh fisheye trong mẫu; QC1-12 là file `duongquochuy-front.zip`.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A03 | lane (thiếu) | nặng | Thiếu L1: vạch vàng liền dài ở bên trái làn mình (từ khoảng (230,700) lên (540,380)) chưa được vẽ. `lint` không bắt được vì ảnh vẫn có một polyline tên L1 |
| 2 | QC1-03 | A03 | lane#3@(699,466) | nặng | position = L1 nhưng đây là dãy vạch đứt bên phải làn mình (chỗ chữ SCHOOL), đúng là R1 |
| 3 | QC1-07 | A02 | drivable#6@(1173,720) | chính | Polygon `alternative` phủ phần lề rải nhựa và đất bên phải vạch trắng liền, không phải làn cùng chiều; vùng lái tràn lề |
| 4 | QC1-09 | A01 | traffic_sign#7@(551,407) | chính | group = prohibitory; đây là biển xanh chỉ dẫn, đúng là information |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Lô của Huy không có lane nào ở A05 (lint báo QC1-02 thiếu L1 và R1). Ảnh là đường hẹp, hai bên xe đỗ, mình không thấy vạch sơn. Có được miễn QC1-02 không? | |
| A06 | Lô của Huy không có lane nào ở A06 (lint báo QC1-02). Ảnh có đoạn vạch vàng ngắn ở xa phía sau xe đen. Có được miễn QC1-02 không, hay phải vẽ L1/R1? | |
| A03 | Polyline R1 của Huy nằm sát hàng xe đỗ bên phải. Đó có thể là vạch giới hạn chỗ đỗ xe chứ không phải vạch làn: nên bỏ, hay gán R2? | |
| A01 | Xe nằm sát một dãy đứt. Huy gán L1 và R1 là hai dãy đứt, R2 là vạch vàng. Cách gán này có đúng không? Ngoài ra có 4 polygon `alternative` nằm sát hai bên (có thể là lề hoặc làn khẩn cấp): có tính là thừa theo QC1-07 không? | |
| A04 | Huy gán `lane` L2 (dashed) và một polygon `crosswalk` nhỏ ở đường bên kia vạch vàng đôi (chiều ngược lại). Có thuộc phạm vi gán của A04 không? | |
| A03, A04 | `timeofday = day` nhưng ảnh chụp lúc chiều tối (trời xám, xe bật đèn). Có tính là sai tag không, và ở mức nào? | |

## Quyết định
Lỗi nặng: 2   Lỗi chính: 2 / 66 nhãn = 3,0 %   Lỗi nhẹ: 0   Ca chờ lead: 6  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Còn 2 lỗi nặng ở A03 (thiếu vạch vàng L1 và gán sai position của dãy đứt), nên theo luật phải Rework. Tỉ lệ lỗi chính 3,0 % chưa vượt 5 % nhưng không ảnh hưởng kết luận. Các ca mơ hồ ở trên không đổi kết luận, vì đã có lỗi nặng.

Ghi chú ngoài mẫu (không tính vào số liệu trên): `road_check lint` cho cả hai file của lô báo 22 lỗi nặng, trong đó cả 8 ảnh fisheye (B01–B08) đều có camera = front thay vì fisheye_front, fisheye_rear, fisheye_left, fisheye_right theo tên file.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
