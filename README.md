# 🔐 Auditoría de Seguridad WiFi: Captura de Handshake WPA2 con SSID Oculto y Ataque de Diccionario

![Banner del Proyecto](bannerp.png)


## 🎯 Objetivo del Proyecto

Demostrar la vulnerabilidad de las redes WiFi WPA2 ante ataques de diccionario, utilizando un entorno controlado (red propia) para:

- ✅ Capturar un handshake WPA2 en una red con SSID oculto.
- ✅ Evaluar la robustez de la contraseña frente a herramientas de pentesting.
- ✅ Analizar la efectividad del ocultamiento del SSID como medida de seguridad.
- ✅ Documentar el proceso completo para fines educativos y de concienciación.

## 📁 Fase 1: Configuración del Hardware y Preparación del Entorno
- Selección del adaptador WiFi (RTL88x2bu)
- Instalación de drivers en Linux
- Activación del modo monitor
- Verificación del funcionamiento

## 📁 Fase 2: Captura y Análisis del Handshake WPA2
- Escaneo de redes
- Captura del handshake
- Resolución del problema del SSID oculto
- Ataque de diccionario con aircrack-ng
- Análisis de resultados y conclusiones

- ---

## 📁 Fase 1: Configuración del Hardware y Preparación del Entorno

### 🛠️ Selección del Adaptador WiFi
- **Modelo:** USB AC1200 (LV-UAC15)
- **Chipset:** RTL88x2bu
- **Sistema:** Linux Mint (kernel 7.0.0-28)

### 🔧 Instalación de Drivers en Linux
- Instalación desde el PPA `kelebek333/kablosuz`.
- Verificación del adaptador con `lsusb`.

### 📡 Activación del Modo Monitor
- Comando: `sudo airmon-ng start wlx909164306c59`
- Verificación: `iwconfig` y `ip link show`

### ✅ Verificación del Funcionamiento
- Escaneo de redes: `sudo airodump-ng wlx909164306c59`
- Confirmación de captura de paquetes y redes visibles.

---

## 📁 Fase 2: Captura y Análisis del Handshake WPA2

### 🔍 Escaneo de Redes
- Identificación de la red objetivo: `FSociety_NoVoilesEICodigo`
- BSSID: `30:16:9D:81:12:17`
- Canal: 9

### 📡 Captura del Handshake
- Enfoque en la red: `sudo airodump-ng -c 9 --bssid 30:16:9D:81:12:17 -w captura_fsociety wlx909164306c59`
- Forzar reconexión: `sudo aireplay-ng -0 2 -a 30:16:9D:81:12:17 wlx909164306c59`
- Verificación: `sudo aircrack-ng captura_fsociety-01.cap`

### 🧩 Resolución del Problema del SSID Oculto
- **Problema:** `aircrack-ng` requería el ESSID, pero el archivo `.cap` no lo contenía.
- **Solución:** Captura del ESSID en vivo con `airodump-ng` y `aireplay-ng`.
- **ESSID obtenido:** `FSociety_NoVoilesEICodigo`

### 🔓 Ataque de Diccionario con Aircrack-ng
- Diccionario utilizado: `master.list`
- Comando: `sudo aircrack-ng -w /home/leon2001/Documentos/wordlist/WPA/master.list -e FSociety_NoVoilesEICodigo captura_fsociety-01.cap`
- **Resultado:** La contraseña no se encontró en el diccionario.

### 📊 Análisis de Resultados y Conclusiones
- La contraseña es robusta frente a ataques de diccionario comunes.
- El SSID oculto no impide la captura del handshake ni el descubrimiento del nombre de la red.
- La seguridad de una red WiFi depende de la fortaleza de la contraseña.

---

### 📄 Documentación

📎 [Descargar Configuracion de Adaptador Wifi (.pdf)](./Configuracion-adaptadorwifi.pdf)
*(Incluye análisis de riesgos, implicaciones legales y referencias normativas).*

📎 [Descargar Auditoria (.pdf)](./auditoria.pdf)  
*(Para visualizar la configuración en Cisco Packet Tracer).*

## 📌 Lecciones Aprendidas

- 🔒 El SSID oculto no es una medida de seguridad efectiva.
- 🧠 `aircrack-ng` siempre necesita el ESSID, incluso si se usa el BSSID.
- 📡 La captura en vivo es una técnica poderosa para obtener información que no está en una captura pasiva.
- 🔑 La fortaleza de la contraseña es el factor crítico en la seguridad de una red WiFi.

---

## 📬 Contacto

📧 [elarhuaa@gmail.com](mailto:elarhuaa@gmail.com)
