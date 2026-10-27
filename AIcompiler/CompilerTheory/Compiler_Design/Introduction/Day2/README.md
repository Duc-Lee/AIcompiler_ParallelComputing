# Analysis and Synthesis Phases (Hai Giai đoạn Phân tích và Tổng hợp)

## 1. Tổng quan kiến trúc Compiler

Một trình biên dịch (Compiler) tiêu chuẩn gồm **6 pha tuần tự** (phases). Về mặt kiến trúc tổng thể, 6 pha này được chia thành **2 giai đoạn lớn**:
1. **Analysis Phase (Giai đoạn Phân tích) – hay Front-end**
2. **Synthesis Phase (Giai đoạn Tổng hợp) – hay Back-end**

Cầu nối giữa hai giai đoạn này là **Intermediate Representation (IR - Mã biểu diễn trung gian)**.

---

## 2. Sơ đồ phân chia kiến trúc Front-end & Back-end

```
                 [ Mã nguồn bậc cao (C, Java, Python...) ]
                                     │
   ══════════════════════════════════╪══════════════════════════════════
   FRONT-END (Analysis Phase)        │  (Language-Dependent, Machine-Independent)
   ──────────────────────────────────┼──────────────────────────────────
                                     ▼
                          1. Lexical Analysis (Scanner)
                                     │
                                     ▼
                          2. Syntax Analysis (Parser)
                                     │
                                     ▼
                          3. Semantic Analysis
                                     │
                                     ▼
                     4. Intermediate Code Generation (ICG)
   ══════════════════════════════════╪══════════════════════════════════
                                     │
                                     ▼  [ Intermediate Representation (IR) ]
                                     │
   ══════════════════════════════════╪══════════════════════════════════
   BACK-END (Synthesis Phase)        │  (Machine-Dependent, Language-Independent)
   ──────────────────────────────────┼──────────────────────────────────
                                     ▼
                          5. Code Optimization
                                     │
                                     ▼
                          6. Code Generation
   ══════════════════════════════════╪══════════════════════════════════
                                     │
                                     ▼
                [ Mã hợp ngữ / Mã máy đích (x86, ARM, RISC-V...) ]
```

---

## 3. Giai đoạn Phân tích: Analysis Phase (Front-end)

### 3.1. Đặc trưng cốt lõi
* **Language-Dependent (Phụ thuộc ngôn ngữ nguồn):** Front-end phải hiểu cú pháp, ngữ pháp (grammar rules), từ khóa và kiểu dữ liệu riêng của ngôn ngữ nguồn (ví dụ: cú pháp C khác Java, Python).
* **Machine-Independent (Độc lập phần cứng máy tính):** Giai đoạn này không quan tâm chương trình sẽ chạy trên vi xử lý nào (Intel x86, ARM, RISC-V hay vi điều khiển 8051/8086). Nhiệm vụ duy nhất là phân tích tính hợp lệ của mã nguồn và chuyển sang dạng biểu diễn trung gian chuẩn.

### 3.2. Bốn pha thuộc Front-end
1. **Lexical Analysis (Phân tích từ vựng):** Quét luồng ký tự mã nguồn, nhóm thành các token hợp lệ và loại bỏ khoảng trắng, chú thích.
2. **Syntax Analysis (Phân tích cú pháp):** Kiểm tra cấu trúc câu theo văn phạm của ngôn ngữ, xây dựng cây cú pháp (Parse Tree / AST).
3. **Semantic Analysis (Phân tích ngữ nghĩa):** Kiểm tra tính hợp lệ về kiểu dữ liệu (Type checking), phạm vi biến (Scope checking) và ngữ nghĩa logic.
4. **Intermediate Code Generation - ICG (Sinh mã trung gian):** Chuyển đổi cây cú pháp thành mã trung gian trừu tượng (như Three-Address Code, SSA form), không phụ thuộc vào tập lệnh của bất kỳ CPU cụ thể nào.

---

## 4. Giai đoạn Tổng hợp: Synthesis Phase (Back-end)

### 4.1. Đặc trưng cốt lõi
* **Machine-Dependent (Phụ thuộc phần cứng máy tính):** Back-end chịu trách nhiệm trực tiếp với kiến trúc CPU đích (Target Architecture). Nó phải hiểu rõ:
  * Tập lệnh máy (Instruction Set Architecture - ISA: x86, ARM, MIPS...).
  * Số lượng và vai trò của các thanh ghi vật lý (Registers).
  * Mô hình định địa chỉ và kiến trúc bộ nhớ.
* **Language-Independent (Độc lập ngôn ngữ nguồn):** Back-end nhận đầu vào là mã trung gian (IR). Tại thời điểm này, chương trình ban đầu được viết bằng C, Java hay Python không còn quan trọng, vì IR đã được chuẩn hóa.

### 4.2. Hai pha thuộc Back-end
1. **Code Optimization (Tối ưu hóa mã):** Cải tiến mã lệnh để tăng tốc độ thực thi, giảm dung lượng bộ nhớ hoặc tiết kiệm năng lượng tiêu thụ (bao gồm cả tối ưu độc lập máy và tối ưu phụ thuộc máy).
2. **Code Generation (Sinh mã đích):** Ánh xạ mã trung gian thành chuỗi lệnh hợp ngữ (Assembly) hoặc mã máy trực tiếp cho vi xử lý đích, thực hiện phân bổ thanh ghi (Register Allocation) và định địa chỉ bộ nhớ.

---

## 5. Bảng so sánh Front-end vs Back-end

| Tiêu chí | Front-end (Analysis Phase) | Back-end (Synthesis Phase) |
| :--- | :--- | :--- |
| **Tên gọi khác** | Giai đoạn Phân tích (Analysis) | Giai đoạn Tổng hợp (Synthesis) |
| **Phụ thuộc Ngôn ngữ** | **Có (Language-Dependent)** | **Không (Language-Independent)** |
| **Phụ thuộc Phần cứng** | **Không (Machine-Independent)** | **Có (Machine-Dependent)** |
| **Đầu vào (Input)** | Mã nguồn bậc cao (C, Java, Python...) | Mã trung gian (Intermediate Representation - IR) |
| **Đầu ra (Output)** | Mã trung gian (IR) | Hợp ngữ / Mã máy đích (x86, ARM...) |
| **Các pha bao gồm** | 1. Lexical Analysis<br>2. Syntax Analysis<br>3. Semantic Analysis<br>4. Intermediate Code Gen | 5. Code Optimization<br>6. Code Generation |
| **Đối tượng hướng tới** | Lập trình viên & Quy tắc ngôn ngữ | Bộ vi xử lý & Kiến trúc phần cứng |

---

## 6. Ý nghĩa kiến trúc trong kỹ nghệ Compiler hiện đại

Việc tách rời hoàn toàn giữa **Front-end** và **Back-end** thông qua **IR** mang lại lợi ích công nghệ then chốt:

* **Tránh bùng nổ tổ hợp ($M \times N \rightarrow M + N$):**
  * Giả sử cần hỗ trợ $M$ ngôn ngữ lập trình chạy trên $N$ kiến trúc CPU khác nhau:
    * Nếu thiết kế nguyên khối (monolithic): Cần viết $M \times N$ trình biên dịch riêng biệt.
    * Với kiến trúc phân tách: Chỉ cần viết $M$ Front-ends và $N$ Back-ends kết nối qua một chuẩn IR chung. Tổng số module chỉ còn là $M + N$.
* Đây chính là triết lý thiết kế nền tảng của các hệ thống Compiler hiện đại như **LLVM** (Clang, Rust, Swift dùng chung LLVM Back-end) và **GCC**.