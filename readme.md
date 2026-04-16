from flask import Flask
import RPi.GPIO as GPIO

app = Flask(__name__)

GPIO.setmode(GPIO.BCM)
GPIO.setup(17, GPIO.OUT)

@app.route('/trigger')
def trigger():
    GPIO.output(17, True)
    return "ON"

@app.route('/off')
def off():
    GPIO.output(17, False)
    return "OFF"

app.run(host='0.0.0.0', port=5000)












import cv2
import requests

PI_IP = "http://10.27.78.191:5000"

cap = cv2.VideoCapture(0)

while True:
    ret, frame = cap.read()

    # Temporary detection
    detected = True

    if detected:
        try:
            requests.get(f"{PI_IP}/trigger")
        except:
            pass

    cv2.imshow("Camera", frame)

    if cv2.waitKey(1) == 27:
        break

cap.release()
cv2.destroyAllWindows()
