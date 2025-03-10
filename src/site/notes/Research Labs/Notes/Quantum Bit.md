---
{"up":["[[Quantum Computing MOC]]"],"related":null,"created":"2023-12-31","tags":["quantum_computing"],"dg-publish":true,"permalink":"/research-labs/notes/quantum-bit/","dgPassFrontmatter":true}
---

## Giới thiệu về Quantum Bits
qubit được định nghĩa là một đối tượng dùng để truyền tải thông tin trên nền tảng lý thuyết thông tin lượng tử và tính toán trên máy tính lượng tử

Thuật ngữ được đề xuất bởi Benjamin Schumacher trong research paper =="Quantum Coding"== năm 1995

Trong nghiên cứu lý thuyết, qubit thường được mô tả như 1 hạt có spin 1/2 *(Spin là một đại lượng vật lý, có bản chất của momen động lượng và là một khái niệm thuần túy lượng tử, không có sự tương ứng trong cơ học cổ điển)*

## Biểu diễn toán học của qubit
Qubit là một hệ lượng tử có hai mức được biểu diễn trong không gian Hilber 2 chiều. 

Trong không gian này, một cặp trạng thái lượng tử trực giao và chuẩn hóa được chọn để mô tả một hệ vật lý
$$
|0\rangle = [_{0}^{1}\textrm{}] , |1\rangle = [_{0}^{1}\textrm{}]
$$

Dễ dàng nhận thấy rằng các trạng thái $|0\rangle$ và $|1\rangle$ của qubit tương ứng với các giá trị nhị phân của 0 và 1 của bit. Tuy nhiên, điểm khác biệt quan trọng chính là bit cổ điển chỉ có thể biểu diễn tại một thời điểm duy nhất một trạng thái 0 hoặc 1.

Trong khi đó, với nguyên lý chồng chập, qubit có thể tạo thành một tổ hợp tuyến tính (chồng chất) của các vecto cơ sở. Điều này có nghĩa là một qubit đơn có thể được mô tả bằng sự tổ hợp tuyến tính của $|0\rangle$ và $|1\rangle$:
$$
|\psi\rangle = \alpha|0\rangle + \beta|1\rangle
$$
trong đó, $\alpha$ và $\beta$ là các số phức được gọi là biên độ xác suất[1]. 

Theo Born rule[2], trong cơ học lượng tử, xác suất để tìm thấy qubit ở trạng thái $|0\rangle$ là $|\alpha|^2$; và xác suất để tìm thấy qubit ở trạng thái $|1\rangle$ là $|\beta|^2$. Vì tổng xác suất bằng 1, nên người ta đưa ra ràng buộc:
$$
|\alpha|^2 + |\beta|^2 = 1
$$
Biểu thức tổng quát phía trên còn trình bày một ý nghĩa quan trọng: nó cho biết qubit là một sự *chồng chập trạng thái* kết hợp giữa $|0\rangle$ và $|1\rangle$ thay vì một hỗn hợp không kết hợp.

## Biểu diễn qubit bằng quả cầu Bloch
Quả cầu Bloch là một quả cầu có bán kính đơn vị. Nó được sử dụng để biểu diễn các qubit một cách trực quan. Vị trí của một qubit được xác định rõ ràng thông qua các thông số $\theta$ và $\psi$.

![|400](https://i.imgur.com/nP1pyRa.png)


$$
|\psi\rangle = \alpha|0\rangle + \beta|1\rangle=\cos(\frac{\theta}{2})|0\rangle +  e^{i\varphi}\sin(\frac{\theta}{2})|1\rangle 
$$
Với $0\leqslant\varphi <2\pi$ và $0\leqslant\theta<\frac{\pi}{2}$

Khi biểu diễn trên một quả cầu như vậy, một bit cổ điển chỉ có thể ở **Bắc cực** hoặc **Nam cực**, tại các vị trí $|0\rangle$ và $|1\rangle$ tương ứng. Phần còn lại của quả cầu Bloch không thể tiếp cận được đối với một bit cổ điển, nhưng một qubit có thể biểu diễn bởi bất kỳ điểm nào trên bề mặt. 

Các mũi tên cho thấy hướng mà vector trạng thái đang trỏ và mỗi phép biến đổi có thể được coi như một phép quay về một trong các trục.

Ví dụ, trạng thái qubit $(|0\rangle+|1\rangle)/\sqrt{2}$ sẽ nằm trên xích đạo của quả cầu ở trục x dương.

Bề mặt của quả cầu Bloch là một không gian 2 chiều, thể hiện không gian trạng thái quan sát được của các trạng thái qubit.
### Visualize quantum bit bằng quả cầu Bloch

![|400](https://i.imgur.com/c25vZ5V.png)


```python
import numpy as np  
import matplotlib.pyplot as plt  
from qutip import *  
# Generate a random quantum state vector  
num_qubits = 1  # Number of qubits  
state = rand_ket(2 ** num_qubits)  
  
# Visualize the state using a Bloch sphere representation  
bloch = Bloch()  
bloch.add_states(state)  
bloch.show()  
  
# Show the plots  
plt.show()
```

---
[1] Probability amplitude là một số phức được sử dụng để mô tả các hành vi của hệ thống. Bình phương modul của đại lượng này biểu thị mật độ xác suất
[2] Born rule là một định đề trong cơ học lượng tử cho biết xác xuất mà một phép đo lường *(measurement)* trong hệ lượng tử sẽ mang lại một kết quả nhất định

