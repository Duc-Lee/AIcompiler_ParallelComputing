# Language Processing System (Hệ thống Xử lý Ngôn ngữ)

## 1. Tổng quan về Language Processing System (LPS)

Để một chương trình viết bằng ngôn ngữ bậc cao có thể thực thi được trên phần cứng, cần có một chuỗi các công cụ phối hợp với nhau. Chuỗi công cụ này được gọi là **Language Processing System (LPS)**.

### 1.1. Bản chất vấn đề
* **Programmer (Lập trình viên):** Viết chương trình bằng **ngôn ngữ bậc cao (High-Level Language - HLL)** như C/C++, Java, Python... Ngôn ngữ này gần gũi với tư duy con người, có tính trừu tượng cao nhưng vi xử lý không thể hiểu trực tiếp.
* **Processor (Bộ vi xử lý / CPU):** Chỉ có thể hiểu và thực thi **ngôn ngữ máy / mã nhị phân (Low-Level Language / Binary Code)** gồm các chuỗi bit `0` và `1`.
* **Nhiệm vụ của LPS:** Đóng vai trò như một "hộp đen" nhận đầu vào là mã nguồn (Source Code) và chuyển đổi thành mã thực thi (Executable Code / Machine Code) mà CPU có thể chạy được.

---

## 2. Kiến trúc tổng quan của LPS

Hệ thống xử lý ngôn ngữ gồm 4 giai đoạn nối tiếp nhau:

```
[ High-Level Language (Source Code) ]
                 │
                 ▼
       ┌───────────────────┐
       │   Preprocessor    │  (Bộ tiền xử lý)
       └───────────────────┘
                 │
                 ▼  [ Pure High-Level Language ]
       ┌───────────────────┐
       │     Compiler      │  (Trình biên dịch)
       └───────────────────┘
                 │
                 ▼  [ Target Assembly Language ]
       ┌───────────────────┐
       │     Assembler     │  (Trình hợp dịch)
       └───────────────────┘
                 │
                 ▼  [ Relocatable Object Code ]
       ┌───────────────────┐
       │  Linker / Loader  │  (Bộ liên kết & Bộ nạp)
       └───────────────────┘
                 │
                 ▼
   [ Absolute Machine Code / Executable ]
```

---

## 3. Chi tiết các thành phần trong LPS

### 3.1. Preprocessor (Bộ tiền xử lý)
Thực hiện các thao tác xử lý sơ bộ mã nguồn trước khi biên dịch thực sự:
* **Macro Expansion (Mở rộng Macro):** Thay thế các định danh macro bằng giá trị hoặc biểu thức thực tế (ví dụ: `#define PI 3.14`).
* **File Inclusion (Chèn tệp):** Đọc nội dung của các file tiêu đề (header files) hoặc module ngoài vào tệp nguồn hiện tại (ví dụ: `#include <stdio.h>`).
* **Loại bỏ chú thích (Stripping comments) & Xử lý biên dịch có điều kiện:** Xóa bỏ comment, xử lý các chỉ thị tiền xử lý (`#ifdef`, `#endif`).
* **Đầu ra:** **Pure High-Level Language** (Mã nguồn thuần bậc cao – toàn bộ macro và thư viện phụ thuộc đã được nhúng đầy đủ).

---

### 3.2. Compiler (Trình biên dịch)
Dịch mã nguồn thuần bậc cao thành **Target Assembly Language** (Hợp ngữ đích).
* Assembly là ngôn ngữ sử dụng các mã gợi nhớ (**mnemonics**) thay vì chuỗi bit nhị phân trực tiếp (ví dụ: `MOV`, `ADD`, `MUL`), thao tác trực tiếp với các thanh ghi (registers) và bộ nhớ.
* Trình biên dịch là trọng tâm chính của môn học này, gồm 6 pha phân tích và tổng hợp (sẽ học chi tiết ở các bài sau).

#### Ví dụ minh họa quá trình sinh mã của Compiler

Xét câu lệnh gán trong ngôn ngữ bậc cao:
```c
x = a + b * c;
```

Để chuyển câu lệnh này sang hợp ngữ (Target Assembly Language), Compiler phải xử lý hai vấn đề cốt lõi:
1. **Độ ưu tiên toán tử (Operator Precedence):** Phép nhân (`*`) có độ ưu tiên cao hơn phép cộng (`+`), do đó biểu thức con `b * c` phải được tính trước.
2. **Quản lý và tái sử dụng thanh ghi (Register Allocation & Reuse):** CPU không tính toán trực tiếp giữa hai ô nhớ RAM mà phải đưa vào thanh ghi. Sau khi một thanh ghi hoàn thành nhiệm vụ, Compiler sẽ tái sử dụng ngay để tiết kiệm tài nguyên.

---

##### Quá trình sinh mã diễn ra qua 4 bước:

* **Bước 1 – Nạp dữ liệu vào thanh ghi:**
  * Giả sử giá trị biến `b` được đưa vào thanh ghi `R0`.
  * Giá trị biến `c` được đưa vào thanh ghi `R1`.

* **Bước 2 – Thực hiện phép nhân (`b * c`):**
  ```assembly
  MUL R0, R1      ; R0 = R0 * R1
  ```
  * Lấy giá trị trong `R0` nhân với `R1`, kết quả của `(b * c)` được lưu lại vào `R0`.
  * Sau lệnh này, giá trị của `c` trong `R1` không còn cần thiết nữa $\rightarrow$ thanh ghi `R1` trở thành thanh ghi tự do (free).

* **Bước 3 – Tái sử dụng `R1` và thực hiện phép cộng (`a + (b * c)`):**
  * Do `R1` đã rảnh, Compiler nạp giá trị của biến `a` vào `R1` (thay vì phải tốn thêm thanh ghi `R2`).
  * Thực hiện phép cộng:
  ```assembly
  ADD R0, R1      ; R0 = R0 + R1
  ```
  * Cộng giá trị `a` (trong `R1`) với kết quả `b * c` (đang có sẵn trong `R0`), kết quả toàn bộ biểu thức nằm tại `R0`.

* **Bước 4 – Ghi kết quả về bộ nhớ (Store):**
  ```assembly
  MOV [x], R0     ; Lưu giá trị từ R0 vào địa chỉ ô nhớ của biến x
  ```
  * Di chuyển kết quả cuối cùng từ thanh ghi `R0` vào ô nhớ của biến `x` trong RAM.

---

##### Tổng hợp chuỗi lệnh Assembly & Bảng theo dõi trạng thái (Trace Table)

**Chuỗi lệnh Assembly hoàn chỉnh:**
```assembly
MUL R0, R1      ; Bước 1: Tính b * c       -> Lưu kết quả vào R0
ADD R0, R1      ; Bước 2: Tính a + (b * c)  -> Lưu kết quả vào R0 (với R1 đã nạp a)
MOV [x], R0     ; Bước 3: Ghi R0 vào ô nhớ x
```

**Bảng theo dõi biến đổi của Thanh ghi và Bộ nhớ:**

| Thao tác / Lệnh Assembly | Giải thích chi tiết | Thanh ghi `R0` | Thanh ghi `R1` | Bộ nhớ `[x]` |
| :--- | :--- | :---: | :---: | :---: |
| *(Trạng thái nạp ban đầu)* | Nạp biến `b` vào `R0`, biến `c` vào `R1` | `b` | `c` | Chưa đổi |
| `MUL R0, R1` | Nhân: $R0 = R0 \times R1$ (tính $b \times c$) | $b \times c$ | *Rảnh* | Chưa đổi |
| *(Nạp bổ sung)* | Tái sử dụng `R1` vừa rảnh để nạp biến `a` | $b \times c$ | `a` | Chưa đổi |
| `ADD R0, R1` | Cộng: $R0 = R0 + R1$ (tính $a + (b \times c)$) | $a + (b \times c)$ | `a` | Chưa đổi |
| `MOV [x], R0` | Ghi kết quả từ `R0` vào ô nhớ của `x` | $a + (b \times c)$ | `a` | $a + (b \times c)$ |

---

### 3.3. Assembler (Trình hợp dịch)
* **Chức năng:** Chuyển đổi mã hợp ngữ (Assembly Language) thành mã máy nhị phân.
* **Đặc điểm đầu ra:** Sinh ra **Relocatable Object Code** (Mã đối tượng tái định vị, thường có đuôi `.o` hoặc `.obj`).
  * Đây là mã nhị phân gồm các bit `0` và `1`, nhưng các địa chỉ ô nhớ chưa phải là địa chỉ cố định (absolute address), mà vẫn ở dạng địa chỉ tương đối (relocatable) vì chương trình có thể chưa được đặt ở vị trí bộ nhớ cụ thể.

---

### 3.4. Linker & Loader (Bộ liên kết & Bộ nạp)

Hai công cụ này thường phối hợp chặt chẽ để hoàn tất việc đưa chương trình vào thực thi:

#### Linker (Bộ liên kết):
* Một chương trình lớn thường được chia thành nhiều file mã nguồn (nhiều file `.obj`) và sử dụng các hàm từ thư viện chuẩn (library files như `libc.a`, `dll`).
* Linker gom các file object rời rạc lại, giải quyết các tham chiếu ngoại vi (external symbols/references) và liên kết các lời gọi hàm thư viện vào chương trình.
* Kết quả sinh ra file thực thi hoàn chỉnh (Executable binary, e.g., `.exe` trên Windows hoặc ELF trên Linux).

#### Loader (Bộ nạp):
* Chịu trách nhiệm nạp file thực thi từ đĩa cứng (Secondary Storage) vào **bộ nhớ chính (RAM)**.
* Thiết lập không gian địa chỉ: cấp phát vùng nhớ mã lệnh (Code segment), dữ liệu (Data/BSS segment), ngăn xếp (Stack), và bộ nhớ động (Heap).
* Khởi tạo các thanh ghi vi xử lý và chuyển quyền điều khiển cho CPU để bắt đầu chạy chương trình.
* **Đầu ra cuối cùng:** **Absolute Machine Code** (Mã máy tuyệt đối) nằm trên RAM, sẵn sàng thực thi trực tiếp.

---

## 4. Bảng tổng kết luồng xử lý

| Giai đoạn (Stage) | Đầu vào (Input) | Đầu ra (Output) | Vai trò chính |
| :--- | :--- | :--- | :--- |
| **Preprocessor** | Source Code (HLL) | Pure HLL | Mở rộng macro, chèn header files, làm sạch mã nguồn. |
| **Compiler** | Pure HLL | Target Assembly Language | Phân tích cú pháp/ngữ nghĩa, tối ưu và sinh mã hợp ngữ. |
| **Assembler** | Target Assembly Language | Relocatable Object Code (`.o`/`.obj`) | Dịch mã gợi nhớ sang mã máy nhị phân địa chỉ tương đối. |
| **Linker** | Relocatable Object Code + Libraries | Executable File (`.exe`/ELF) | Ghép nối các module, giải quyết địa chỉ tham chiếu chéo. |
| **Loader** | Executable File | Absolute Machine Code in RAM | Nạp mã vào RAM, thiết lập thanh ghi và phân bổ bộ nhớ. |

