Este proyecto integra un sistema automatizado de control ambiental programado en Arduino que monitorea en tiempo real la temperatura y la humedad mediante sensores analógicos en los pines A0 y A1, desplegando los datos en un monitor serial y en una pantalla LCD 16x2. A través de su lógica de control, el código reacciona a los valores medidos girando un servomotor a 90° en el pin 7 para abrir una compuerta al superar los 30 °C, encendiendo un motor extractor en el pin 8 junto a una alarma en el pin 13 si la temperatura excede los 40 °C, y activando la bomba de riego en el pin 12 cuando la humedad supera el 30 %, todo respaldado por una pausa de 500 ms que garantiza la estabilidad de las lecturas.

<img width="667" height="707" alt="image" src="https://github.com/user-attachments/assets/0de99457-378b-4fb6-bdf7-6730ec5876ac" />

<img width="715" height="432" alt="image" src="https://github.com/user-attachments/assets/5c691b0e-bf86-482c-af00-6f8ff0188979" />
