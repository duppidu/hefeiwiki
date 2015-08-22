## Verbesserungen

### Dynamische Erkennung  
Um den Ungenauigkeiten bei der Positionierung un dem eventuellen verwackeln der Kameraposition entgegenzuwirken währe eine dynamische Erkennung eine gute Lösung.  
Man müsste auf dem Bild eine Farbe erkennen und dann auf diese Farbe die Position der gesamten Lampensäule errechnen. Am besten würde sich für diese Anwendung wohl die Grüne Lampe eignen. Diese müsste dann Leuchtend und nicht Leuchtend erkannt werden. Nach dem erkennen der Farbe müsste die grösse der Fläche ermittelt werden und dann nochmals 2 gleichgrosse Flächen auf diese gelegt werden um so die Position der anderen beiden Lampen zu ermitteln. Danach kann die jetzige Bilderkennung gestartet werden.