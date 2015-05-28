# Color Detection

In der Klasse ColorDetection werden alle 3 Farben der Lampensäule auf **NICHT LEUCHTEN** überprüft.
Jede Farbe wird nacheinander gleich oft überprüft.

#### Attribute

| Name| Datentyp| Bemerkung|
| t1 | Thread |  |
| mqtt | MqttCom | Broker |
| capture | VideoCapture | hohlt das Webcam Bild |
| webcam_image | Mat | konvertiert das Webcam Bild in eine Matrix |
| hsv_image | Mat | Webcam Bild in HSV Werte konvertiert |
| thresholded | Mat | Zwischengespeichertes Bild |
| thresholded2 | Mat | Zweiter Zwischenspeicher |
| hsv_min | Scalar | minimaler Farbwert in HSV auf dem unkonvertierten Webcam Bild |
| hsv_max | Scalar | maximaler Farbwert in HSV auf dem unkonvertierten Webcam Bild |
| hsv_min2 | Scalar |  |
| hsv_max2 | Scalar |  |
| l1 | Lamps |  |
| startXMin | int |  |
| startXMax | int |  |
| startYMin | int |  |
| startYMax | int |  |
| endXMin | int |  |
| endXMax | int |  |
| endYMin | int |  |
| endYMax | int |  |
| redDetected | boolean |  |
| orangeDetected | boolean |  |
| greenDetected | boolean |  |
| colorToTrack | String |  |
| trackCount | int |  |
| ANZCOUNTS | int |  |
| COUNTTOLLERANZ | int |  |
| countRed | int |  |
| countOrange | int |  |
| countGreen | int |  |






### trackColor()

#### Attribute

| Name| Datentyp| Bemerkung|
 

