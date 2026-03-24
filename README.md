# Actividad-Managing-IP-Addresses
Guía esencial sobre los conocimientos básicos de IP

# 🧩 1. ¿Qué es una dirección IP?

| Concepto | Definición simple | Nivel técnico breve | Ejemplo |
|----------|------------------|--------------------|---------|
| IP | Es la dirección de un dispositivo en internet | Identificador único que permite que dispositivos se comuniquen en una red | 192.168.1.1 |
| IPv4 | (Internet Protocol v4) Versión antigua de IP | Usa números de 32 bits, formato decimal separado por puntos | 8.8.8.8 |
| IPv6 | (Internet Protocol v6) Versión nueva de IP | Usa 128 bits, permite muchísimas más direcciones | 2001:0db8:85a3::8a2e |

---

# ⚙️ 2. Tipos de IP

## 🔹 Diferencias clave

- **IP pública vs privada**
  - Pública: visible en internet  
  - Privada: usada dentro de redes internas (casa, oficina)

- **IP estática vs dinámica**
  - Estática: no cambia  
  - Dinámica: cambia automáticamente  

---

## 📊 Tabla

| Tipo | ¿Qué es? | ¿Cuándo se usa? | Ejemplo real |
|------|---------|----------------|--------------|
| Pública | IP visible en internet | Servidores, páginas web | IP de un servidor en la nube |
| Privada | IP dentro de red local | Casas, empresas | 192.168.0.5 |
| Estática | IP fija | Hosting, APIs, servidores | Backend en producción |
| Dinámica | IP que cambia | Usuarios normales | IP de tu casa con WiFi |

---

# 💻 3. Conexión con desarrollo

## 🔹 ¿Qué IP usa tu backend?

- **Local:**
  - `localhost → 127.0.0.1` (IPv4)  
  - `localhost → ::1` (IPv6)  
  *(solo funciona en tu computador)*

- **Producción:**
  - IP pública o dominio  
  - Ejemplo: `api.midominio.com`

---

## 🔹 ¿Por qué no puedes acceder a localhost desde otro PC?

Porque `127.0.0.1` siempre apunta al mismo computador.  
Cada máquina tiene su propio **localhost**.

---

## 🔹 ¿Qué pasa con `npm run dev`?

- Levanta un servidor local  
- Escucha normalmente en:
  - `127.0.0.1`
  - `localhost`
- Solo accesible desde tu máquina (a menos que lo expongas)

---

## 🔹 ¿Qué IP usa una base de datos en la nube?

- Usa una IP pública o privada  

**Ejemplos:**
- AWS RDS  
- MongoDB Atlas (cluster accesible vía internet)

---

# 🌍 4. Caso práctico (debugging)

## 🧩 Escenario

> “Tu frontend funciona, pero no logra conectarse al backend.”

---

## ❓ ¿Puede ser problema de IP?

Sí, muy probablemente.

Porque la conexión depende de:
- Que la IP sea correcta  
- Que el puerto esté abierto  
- Que ambos estén en la misma red o accesibles  

👉 Si la IP está mal:
- El frontend “no sabe a dónde ir”  
- La petición nunca llega al backend  

**Ejemplo típico:**

```
http://localhost:3000
```

Pero el backend está en otro computador → ❌ error de conexión

---

## 🔍 ¿Qué revisar primero?

1. IP correcta del backend  
2. Puerto (ej: `:3000`, `:8080`)  
3. Si el servidor está corriendo  
4. Configuración CORS  
5. Firewall o red  

**Herramientas útiles:**

```
ipconfig
netstat -an
netstat -an | find "3000"
ping 192.168.x.x
netsh advfirewall firewall show rule name=all
```

---

## ⚠️ Errores típicos

- Usar `localhost` en frontend (no funciona en producción)  
- IP mal escrita  
- Puerto incorrecto  
- Backend no levantado  
- Bloqueo por firewall  

---

# 🧪 5. DHCP y DNS

## 🔹 ¿Qué hace DHCP?

Asigna automáticamente una IP a tu dispositivo cuando te conectas a una red.

---

## 🔹 ¿Qué hace DNS?

Traduce nombres como `google.com` a una IP real.

---

## 🔹 Flujo cuando escribes `google.com`

1. Escribes `google.com`  
2. El navegador consulta al DNS  
3. DNS responde con una IP (ej: 142.x.x.x)  
4. Tu computador se conecta a esa IP  
5. Se carga la página  

---

# 🔄 6. Analogía

- IP = dirección de casa  
- DNS = agenda de contactos (nombre → dirección)  
- DHCP = persona que asigna casas automáticamente  

---

# 🧠 BONUS

## 🔹 ¿Qué es NAT?
NAT es una función del router que permite que varios dispositivos con IP privada compartan una sola IP pública para acceder a internet, traduciendo las direcciones entre la red interna y externa.

- Traduce IP privadas a una IP pública  
- Permite que muchos dispositivos compartan una sola IP de internet  

👉 Ejemplo: tu casa (todos usan el mismo WiFi)

---

## 🔹 IP en Docker
En Docker, cada contenedor tiene su propia IP privada dentro de una red interna virtual. Los contenedores se comunican entre sí usando esas IPs, y para acceder desde fuera se exponen puertos, por ejemplo localhost:3000, que redirige al contenedor.

- Cada contenedor tiene su propia IP interna  
- Se comunican dentro de una red virtual  
- Se exponen con puertos (ej: `localhost:3000`)

---

## 🔹 IP en AWS (EC2)
En AWS EC2, cada instancia tiene una IP privada (para comunicación interna) y una IP pública (para acceso desde internet). La IP pública puede cambiar al reiniciar, a menos que uses una Elastic IP, que es fija.

- Tiene:
  - IP privada (interna)  
  - IP pública (internet)  

- La IP pública puede cambiar (a menos que uses Elastic IP)
