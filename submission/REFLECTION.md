# Reflection — Lab 19

**Tên:** Vũ Hải Nam
**Cohort:** 3
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Precision@10 theo loại query (golden set 50 queries): `exact` — BM25 96.7% = Hybrid 96.7% > Vector 88.7%; `paraphrase` — BM25 33.3% > Hybrid 32.0% > Vector 24.0%; `mixed` — Hybrid 100.0% > Vector 98.5% > BM25 97.0%.

**BM25 thắng `exact`** vì query chứa nguyên văn từ khoá — keyword matching là tín hiệu mạnh nhất. **Vector nhỉnh hơn `paraphrase`** vì không còn từ khoá trùng, chỉ embedding còn bắt được ngữ nghĩa (dù cả hai đều thấp vì `bge-small-en` tối ưu tiếng Anh, chưa mạnh cho paraphrase tiếng Việt). **Hybrid (RRF) thắng rõ nhất `mixed`** — loại query thực tế nhất, có cả từ khoá lẫn ý diễn đạt — vì RRF cộng dồn tín hiệu từ cả hai retriever thay vì phụ thuộc một loại.

**Không dùng hybrid khi:** (1) query luôn exact-match/mã sản phẩm/ID — BM25 thuần đã tối ưu và nhanh hơn nhiều (P50 ~2ms so với ~110ms); (2) latency-critical với corpus nhỏ, độ lợi Precision@10 của hybrid (~1-5pp) không đáng chi phí embedding mỗi query.

---

## Điều ngạc nhiên nhất khi làm lab này

_(Optional, 1–2 câu)_

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
