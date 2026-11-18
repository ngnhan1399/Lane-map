# Lane-map — dữ liệu phân luồng giao thông cho Lane

Kho này đăng tệp overlay phân luồng giao thông đường bộ Việt Nam, cập nhật mỗi sáng.
Muse trích từ thông báo chính thức và báo lớn, kiểm bằng chứng nguyên văn, gắn đoạn đường vào dữ liệu OpenStreetMap, xếp mức áp dụng, rồi đăng ở đây. Kho chỉ chứa tệp tĩnh — không có máy chủ nào chạy trong kho này.

## Tệp Lane / VPS đọc

`active.json` ở nhánh `main` — địa chỉ cố định:

```
https://raw.githubusercontent.com/ngnhan1399/Lane-map/main/active.json
```

- `active.json` chỉ chứa các bản ghi đang hiệu lực hôm nay, mức `HARD` và `SOFT`.
- Trong tuần chạy bóng đầu tiên, `active.json` trên `main` giữ `"records": []`; bản thật nằm ở nhánh `shadow`.

## Cấu trúc

| Đường dẫn | Nội dung |
|---|---|
| `active.json` | Tập bản ghi đang hiệu lực (khuôn version 1) |
| `days/YYYY-MM-DD.json` | Ảnh chụp `active.json` từng ngày, để quay về |
| `inbox/YYYY-MM-DD.json` | Bản ghi thô Muse trích trong ngày |
| `matched/YYYY-MM-DD.json` | Kết quả kiểm bằng chứng + gắn bản đồ, kèm lý do loại |
| `logs/YYYY-MM-DD.md` | Nhật ký ngày |

## Khuôn bản ghi (tóm tắt)

Mỗi bản ghi gồm: `id`, `city`, `type` (`ONEWAY | ROAD_CLOSED | TURN_BAN | VEHICLE_BAN | NEW_ROAD_OPEN | ROAD_REOPENED`), `level` (`HARD | SOFT`), `vehicles`, `start`, `end`, `daily_hours`, `street`, `from_cross`, `to_cross`, `geometry` (đường gấp khúc `[lat, lon]` từ `from_cross` sang `to_cross`, điểm cách nhau ≤ 30 m), `banned` (`forward | backward | both | null`), `turn` (chỉ với `TURN_BAN`), `osm_knows`, `first_seen`, `last_seen`, `source`.

## Ghi công và giấy phép

- Hình học đường: © OpenStreetMap contributors, giấy phép ODbL.
- Quy định giao thông: theo nguồn ghi trong từng bản ghi (thông báo của cơ quan quản lý và báo chí Việt Nam).
- Không dùng Google Maps hay ứng dụng bản đồ nào làm nguồn. Không ghi gì lên OpenStreetMap công cộng.
