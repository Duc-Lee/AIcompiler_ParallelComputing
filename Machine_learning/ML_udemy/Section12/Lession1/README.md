## Lession 1: Numpy in Python

- Sang phần mới là phần về Phân tích dữ liệu bằng Python (Data analysis with Python)
  - Mô đun này sẽ tập trung vào các thư viện cốt lõi:
    - **Numpy, Pandas**: Dùng để xử lí, thao tác và phân tích dữ liệu
    - **Matplotlib, Seaborn**: Dùng để trực quan hóa dữ liệu (Data visualization)
- Trong số đó, Numpy đóng vai trò nền tảng tối quan trọng. Kể cả sau này khi làm việc với các mô đun Deep-Learning (Học sâu), bạn vẫn sẽ dùng Numpy theo nhiều cách khác nhau. Numpy cho phép chúng ta tạo mảng, thao tác với ma trận và thực thi các phép toán số học cực kì nhanh chóng.

### 1. Định nghĩa và cách cài đặt Numpy

- Numpy là thư viện cơ bản phục vụ tính toán khoa học trong Python. Nó cung cấp mảng đa chiều, ma trận cùng hệ thống các hàm toán học tối ưu để thao tác trực tiếp trên các cấu trúc dữ liệu này thông qua các phép toán vector hoá (vectorized operations).
- Khi khởi tạo một môi trường ảo (virtual environment) mới, Numpy không được tích hợp sẵn. Có 2 cách cài đặt:
  - **Cách 1: Qua file requirements.txt**
    - Thêm numpy vào file `requirements.txt`, sau đó mở terminal chạy lệnh:
```bash
pip install -r requirements.txt
```
  - **Cách 2: Chạy trực tiếp trong terminal**
```bash
pip install numpy
```
- Để sử dụng thư viện numpy, đặt bí danh (alias) là `np`:
```python
import numpy as np
```
- Việc khởi tạo đặt bí danh alias là `np` giúp không cần gõ lại toàn bộ nguyên vẹn chữ numpy.

### 2. Khởi tạo mảng và tìm hiểu về chiều

#### a. Mảng 1 chiều (1D - Array)
- Sử dụng hàm `np.array()` và truyền một danh sách (list) hoặc tuple.

```python
import numpy as np

# Tạo mảng 1 chiều
arr = np.array([1, 2, 3, 4, 5])

print(arr)
# Output: [1 2 3 4 5]

# Kiểm tra dữ liệu của đối tượng
print(type(arr))
# Output: <class 'numpy.ndarray'>

# Kiểm tra kích thước và hình dạng
print(arr.shape)
# Output: (5,)
```
> Lưu ý quan trọng về mảng 1D: Kết quả shape hiển thị `(5,)` với một khoảng trống sau dấu phẩy nghĩa là mảng này chỉ có đúng 1 chiều gồm 5 phần tử. Đây không phải là 1 hàng 5 cột; mảng 1 chiều thuần túy không phân định hàng hay cột.