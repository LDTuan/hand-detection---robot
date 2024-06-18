# Ứng dụng xử lý ảnh nhận dạng cử chỉ bàn tay điều khiển robot chuyển động
Code chương trình cho nhận diện bàn tay
•	
Code chương trình cho Arduino
•	
•	
Trong đề tài, được chia làm 3 nhiệm vụ chính:

•	Nhận diện cử chỉ bàn tay 

•	Xây dựng phần cứng cho robot (cơ cấu chấp hành)

•	Truyền nhận tính hiệu điều khiển từ laptop qua robot

![image](https://github.com/LDTuan/hand-detection-robot/assets/138774749/bf13507d-f318-4f2f-b1cc-b1af5e4a732c)

1.	Nhận diện cử chỉ bàn tay

•	Sử dụng mô hình Machine Learning được tạo sẵn bởi MediaPipe
              Đầu vào : Video ( được lấy trực tiếp từ webcam của laptop)
              Đầu ra: Đánh dấu được 21 điểm trên bàn tay
              Đưa ra được số ngón tay khi dơ 1,2,… ngón lên

•	Các bước xây dựng chương trình phát hiện và đánh điểm trên bàn tay. 
-	Bước 1 : Lấy dữ liệu từ camera 
-	Bước 2 : Chuyển đổi không gian màu để phù hợp với định dạng của mediapipe.
-	Bước 3 : Tạo biến và đối tượng để sử dụng các tính năng của mediapipe.
-	Bước 4 : Đánh các điểm trên bàn tay sử dụng giải pháp MediaPipe Hand Landmarks.
-	Bước 5 : So sánh tọa độ các điểm đã được đánh dấu để xác đinh số ngón tay.
  
2.	Xây dựng phần cứng cho robot (cơ cấu chấp hành).
•	Linh kiện sử dụng 
-	Arduino Uno
-	Module điều khiển động cơ L298N
-	Module thu phát tín hiệu RF NRF24L01
-	Động cơ
-	Pin 18650
-	Khung xe, pin, công tắc, led,….
  
 ![image](https://github.com/LDTuan/hand-detection-robot/assets/138774749/d6fce4ab-7061-44c1-9ed9-707aece9c072)
3.	Truyền nhận tính hiệu điều khiển từ laptop qua robot.
•	Ta sẽ nhận dữ liệu từ laptop thông qua cổng com bằng thư viện Serial trên python và gửi dữ liệu tới robot bằng sóng RF
•	Linh kiện sử dụng 
-	Arduino Nano
-	Module thu phát tín hiệu RF NRF24L01
-	Led, điện trở
  
 ![image](https://github.com/LDTuan/hand-detection-robot/assets/138774749/834ce647-3370-475f-949b-2b726693d3e8)


