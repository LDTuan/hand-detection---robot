import cv2 
import mediapipe as mp
import time
import serial

ser = serial.Serial("COM6", 9600)   ## Mở cổng kết với ardiono của bạn

mp_drawing = mp.solutions.drawing_utils
mp_hand = mp.solutions.hands
hands = mp_hand.Hands(
    model_complexity=0,
    min_detection_confidence=0.5,
    min_tracking_confidence=0.5
)

cap = cv2.VideoCapture(0)
while cap.isOpened():
    success, img = cap.read()
    if not success:
        break

    img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    result = hands.process(img)
    img = cv2.cvtColor(img, cv2.COLOR_RGB2BGR)
    count = 0
 #vebantay
    if result.multi_hand_landmarks:
        myHand=[]
        for idx, hand in enumerate(result.multi_hand_landmarks):
            mp_drawing.draw_landmarks(img, hand, mp_hand.HAND_CONNECTIONS)
            for id, lm in enumerate(hand.landmark):
                h, w, _ = img.shape
                myHand  .append([int(lm.x*w), int(lm.y*h)]) # x= 0 , y =1
            if myHand[8][1] < myHand[6][1]:
                count = count + 1
              #  ser.write(count)  ## Yêu cầu arduino bật PIN 1
            if myHand[12][1] < myHand[10][1]:
                count = count + 1

            if myHand[16][1] < myHand[14][1]:
                count = count + 1

            if myHand[20][1] < myHand[18][1]:
                count = count + 1

            if myHand[20][0] < myHand[12][0]:
                if myHand[4][0] > myHand[2][0] or myHand[4][1] < myHand[5][1]:
                    count = count + 1

            if myHand[20][0] > myHand[12][0]:
                if myHand[4][0] < myHand[2][0] or myHand[4][1] < myHand[5][1]:
                    count = count + 1

            if count == 1 :
                cv2.putText(img,str("1-Tien"),(50,70),cv2.FONT_HERSHEY_SIMPLEX, 2, (0, 0, 255), 2,cv2.LINE_AA )
            if count == 0 :
                cv2.putText(img,str("0-Dung"),(50,70),cv2.FONT_HERSHEY_SIMPLEX, 2, (0, 0, 255), 2,cv2.LINE_AA )
            if count == 2 :
                cv2.putText(img,str("2-Lui"),(50,70),cv2.FONT_HERSHEY_SIMPLEX, 2, (0, 0, 255), 2,cv2.LINE_AA )
            if count == 3 :
                cv2.putText(img,str("3-Quay Trai"),(50,70),cv2.FONT_HERSHEY_SIMPLEX, 2, (0, 0, 255), 2,cv2.LINE_AA )
            if count == 4 :
                cv2.putText(img,str("4-Quay Phai"),(50,70),cv2.FONT_HERSHEY_SIMPLEX, 2, (0, 0, 255), 2,cv2.LINE_AA )

    if ser.isOpen():
       ser.write(str(count).encode())

    #hien thi
    cv2.imshow("tay", img)
    key = cv2.waitKey(1)
    if key == 27:
        break

cap.release()