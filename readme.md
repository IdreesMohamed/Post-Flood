import cv2
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)
GPIO.setup(17, GPIO.OUT)

STREAM_URL = "http://10.27.78.56:8000"

cap = cv2.VideoCapture(STREAM_URL)

while True:
    ret, frame = cap.read()

    if not ret:
        print("Waiting for stream...")
        continue

    # Simple detection (always true for demo)
    detected = True

    if detected:
        print("Animal detected!")
        GPIO.output(17, True)
        time.sleep(2)
        GPIO.output(17, False)

    cv2.imshow("EcoSentinel - Pi", frame)

    if cv2.waitKey(1) == 27:
        break

cap.release()
cv2.destroyAllWindows()
