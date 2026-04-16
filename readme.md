import cv2
import requests
import time

PI_IP = "http://10.27.78.191:5000"

cap = cv2.VideoCapture(0)

if not cap.isOpened():
    print("Camera not working")
    exit()

while True:
    ret, frame = cap.read()

    if not ret:
        print("Frame not captured")
        continue

    # Simulate detection
    detected = True

    if detected:
        print("Detection triggered")
        try:
            requests.get(f"{PI_IP}/trigger")
            time.sleep(2)   # prevent spamming
            requests.get(f"{PI_IP}/off")
        except Exception as e:
            print("Error:", e)

    time.sleep(1)
