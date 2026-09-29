# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B2 | ATTRIBUTE | 1 |
| center | B2 | MISSING | 9 |
| center | B2 | SPURIOUS | 12 |
| center | C0 | SPURIOUS | 1 |
| edge | B2 | ATTRIBUTE | 1 |
| edge | B2 | BOX_GEOMETRY | 1 |
| edge | B2 | MISSING | 2 |
| edge | B2 | SPURIOUS | 1 |
| edge | B2 | WRONG_CLASS | 1 |
| mid | B2 | ATTRIBUTE | 1 |
| mid | B2 | BOX_GEOMETRY | 1 |
| mid | B2 | MISSING | 5 |
| mid | B2 | SPURIOUS | 14 |
| unknown | B2 | ATTRIBUTE | 1 |
| unknown | B2 | WRONG_CLASS | 1 |

## Top defects
- SPURIOUS: 28 (ví dụ frame adasind_019560.jpg)
- MISSING: 16 (ví dụ frame adasind_060000.jpg)
- ATTRIBUTE: 4 (ví dụ frame adasind_086220.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- **Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy:**
  - *Lỗi nổi bật nhất là `SPURIOUS` (28 ca) do Model sinh ra*: Nguyên nhân chính là **`E4_model_domain`** (domain gap của mô hình AI). Mô hình phát hiện vật thể gặp khó khăn trước đặc thù quang học của camera mắt cá fisheye (vùng cong méo và dải bóng râm phức tạp ở vùng `mid` và `center`), dẫn đến việc mô hình nhận diện nhầm các mảng kết cấu mặt đường/bóng cây thành vật thể giả (`M_only`).
  - *Về phía người gán nhãn (`E1_annotator_error`)*: Gặp lỗi thiếu thuộc tính `truncated` ở vùng rìa thấu kính (như ca `L11` ở frame `adasind_086220.jpg`) do thói quen gán nhãn camera thường chưa chú ý ranh giới cắt quang học của lens fisheye.
- **Cách sửa và ai nhận việc (`owner`):**
  - **`ai_team`**: Bổ sung tập dữ liệu ảnh fisheye vào tập train để fine-tune mô hình; điều chỉnh ngưỡng confidence score tại vùng `mid` và `center` nhằm giảm thiểu 28 ca false positives.
  - **`annotator`**: Thực hiện rework bổ sung thuộc tính `truncated=1` cho các box chạm biên quang học và rà soát kỹ các vật thể bị che khuất (`occluded`) ở vùng `center`.
- **Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule):**
  - Ảnh minh chứng: [submission/screenshots/qa_evidence_L11_truncated.png](submission/screenshots/qa_evidence_L11_truncated.png) ghi nhận rõ xe ba bánh `L11` chạm mép viền ảnh `xbr=1080px` nhưng `truncated=0`.
  - Dòng findings: Dòng `r2_qa`, frame `adasind_086220.jpg`, vật thể `L11`, vi phạm quy tắc `R05` trong tài liệu [docs/02-rules-vi.md](docs/02-rules-vi.md).
