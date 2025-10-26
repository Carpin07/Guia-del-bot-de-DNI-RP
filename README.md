# 📄 Sistema de DNI Automatizado - Documentación Completa

> Bot de Discord para gestionar Documentos Nacionales de Identidad virtuales con firma digital y base de datos persistente.

---

## 📑 Tabla de Contenidos

1. [Instalación](#-instalación)
2. [Configuración Inicial](#-configuración-inicial)
3. [Comandos para Usuarios](#-comandos-para-usuarios)
4. [Comandos para Administradores](#-comandos-para-administradores)
5. [Sistema de Solicitudes Automáticas](#-sistema-de-solicitudes-automáticas)
6. [Personalización de DNIs](#-personalización-de-dnis)
7. [Preguntas Frecuentes](#-preguntas-frecuentes)
8. [Solución de Problemas](#-solución-de-problemas)

---

## 🚀 Instalación

### Requisitos Previos

- Python 3.8 o superior
- Una cuenta de Discord Developer
- Permisos de administrador en tu servidor

### Paso 1: Instalar Python

1. Descarga Python desde [python.org](https://www.python.org/downloads/)
2. Durante la instalación, marca "Add Python to PATH"
3. Verifica la instalación:
   ```bash
   python --version
   ```

### Paso 2: Instalar Dependencias

Abre PowerShell o Terminal y ejecuta:

```bash
# Instalar librerías necesarias
pip install discord.py
pip install Pillow
pip install qrcode[pil]
```

### Paso 3: Crear Bot en Discord

1. Ve a [Discord Developer Portal](https://discord.com/developers/applications)
2. Click en "New Application"
3. Dale un nombre a tu bot
4. Ve a la sección "Bot"
5. Click en "Add Bot"
6. **Copia el TOKEN** (lo necesitarás después)
7. Activa estos **Privileged Gateway Intents**:
   - ✅ Presence Intent
   - ✅ Server Members Intent
   - ✅ Message Content Intent

### Paso 4: Invitar el Bot

1. Ve a "OAuth2" → "URL Generator"
2. Marca estos **Scopes**:
   - ✅ bot
   - ✅ applications.commands
3. Marca estos **Bot Permissions**:
   - ✅ Send Messages
   - ✅ Embed Links
   - ✅ Attach Files
   - ✅ Read Message History
   - ✅ Add Reactions
   - ✅ Use Slash Commands
4. Copia la URL generada y ábrela en tu navegador
5. Selecciona tu servidor y autoriza

### Paso 5: Configurar el Bot

1. Descarga todos los archivos del bot
2. Crea una carpeta llamada `fonts` dentro de la carpeta del bot
3. Descarga la fuente **Inter** desde [Google Fonts](https://fonts.google.com/specimen/Inter)
4. Extrae `Inter-Regular.ttf` y colócalo en la carpeta `fonts`
5. Abre `index.py` y edita estas líneas:

```python
ADMIN_ROLE_ID = 1234567890  # <-- ID de tu rol de administrador
BOT_TOKEN = "TU_TOKEN_AQUI"  # <-- Token del bot
```

**¿Cómo obtener el ID del rol?**
1. En Discord, activa el Modo Desarrollador (Ajustes → Avanzado → Modo Desarrollador)
2. Click derecho en el rol → Copiar ID

### Paso 6: Ejecutar el Bot

```bash
# En la carpeta del bot
python index.py
```

Si ves esto, ¡funciona! ✅
```
✅ Bot conectado como [Nombre del Bot]
📊 DNIs en base de datos: 0
⏳ DNIs pendientes: 0
```

---

## ⚙️ Configuración Inicial

### 1. Configurar Canales del Sistema

Ejecuta en Discord:

```
/config_canales
```

**Parámetros:**
- `canal_solicitudes` - Canal donde los usuarios enviarán solicitudes automáticas
- `canal_firmados` - Canal donde se publicarán DNIs aprobados

**Ejemplo:**
```
/config_canales canal_solicitudes:#solicitudes-dni canal_firmados:#dnis-oficiales
```

### 2. Verificar Configuración

```
/config_canales
```

Sin parámetros, muestra la configuración actual.

---

## 👥 Comandos para Usuarios

### Ver Ayuda

```
/ayuda_dni
```

Muestra una guía completa del sistema con todos los comandos disponibles.

### Ver Estadísticas

```
/stats_dni
```

Muestra:
- Total de DNIs creados
- DNIs firmados y pendientes
- Distribución por países
- Información general del sistema

---

## 👑 Comandos para Administradores

### Crear DNI Manual

```
/crear_dni
```

**Parámetros opcionales:**
- `pais` - Selecciona el país (España, México, Argentina)
- `tema` - Selecciona el diseño (Clásico, Moderno, Oscuro)

**Proceso:**
1. Selecciona país y tema
2. Se abre un formulario
3. Completa:
   - Edad
   - Fecha de Nacimiento (dd/mm/yyyy)
   - Usuario de Roblox
4. Revisa el preview
5. Confirma o cancela
6. Si confirmas, se publica para firma

**Ejemplo:**
```
/crear_dni pais:España tema:Moderno
```

### Firmar DNI

Cuando se genera un DNI pendiente, aparecen dos botones:

- **✅ Firmar y Aprobar** - Aprueba el DNI
- **❌ Rechazar** - Rechaza la solicitud

Al firmar:
- Se publica en el canal de DNIs firmados (si está configurado)
- Se envía por DM al ciudadano
- Se guarda en la base de datos permanente

---

## 🤖 Sistema de Solicitudes Automáticas

### ¿Cómo funciona?

Los usuarios pueden enviar solicitudes escribiendo un mensaje en el canal configurado con un formato específico. El bot lo detecta automáticamente y crea el DNI.

### Formato de Solicitud

En el canal de solicitudes, escribe:

```
DNI nuevo
Edad: 25
Fecha de Nacimiento: 15/03/1999
Usuario de Roblox: Player123
País: españa
Tema: clasico
```

### Campos Requeridos

✅ **Obligatorios:**
- `Edad` - Número entre 0 y 150
- `Fecha de Nacimiento` - Formato dd/mm/yyyy
- `Usuario de Roblox` - Tu nombre de usuario en Roblox

📋 **Opcionales:**
- `País` - españa, mexico, argentina (por defecto: españa)
- `Tema` - clasico, moderno, oscuro (por defecto: clasico)

### Ejemplo Completo

```
DNI nuevo
Edad: 18
Fecha de Nacimiento: 05/08/2006
Usuario de Roblox: JuanGamer123
País: mexico
Tema: oscuro
```

### ¿Qué pasa después?

1. El bot detecta tu mensaje ✅
2. Genera el DNI automáticamente 📄
3. Lo publica para que los admins lo firmen 🖊️
4. Añade ✅ a tu mensaje original ✔️
5. Un admin firma el DNI 👑
6. Recibes tu DNI firmado por DM 📨

### Ventajas del Sistema Automático

- ⚡ **Rápido** - No necesitas usar comandos
- 📝 **Simple** - Solo copias y pegas el formato
- 🔄 **Automático** - El bot hace todo el trabajo
- 💾 **Persistente** - Al reiniciar, procesa mensajes pendientes

---

## 🎨 Personalización de DNIs

### Países Disponibles

| País | Código | Bandera | Nacionalidad |
|------|--------|---------|--------------|
| España | `españa` | 🇪🇸 | Español/a |
| México | `mexico` | 🇲🇽 | Mexicano/a |
| Argentina | `argentina` | 🇦🇷 | Argentino/a |

### Temas Disponibles

| Tema | Descripción | Colores |
|------|-------------|---------|
| `clasico` | Diseño tradicional | Azul y blanco |
| `moderno` | Diseño minimalista | Gris claro |
| `oscuro` | Diseño dark mode | Negro y gris |

### Información en el DNI

Cada DNI incluye:

- 👤 **Nombre completo** (nombre de Discord)
- 🎂 **Edad**
- 📅 **Fecha de nacimiento**
- 💬 **Tag de Discord**
- 🆔 **ID único** (formato: ESP-000001)
- 🎮 **Usuario de Roblox**
- 🌍 **País y nacionalidad**
- 📆 **Fecha de ciudadanía**
- ✓ **Estado** (Activo)
- 📱 **Código QR** con información verificable
- 🔐 **Sello oficial** (verde si firmado, rojo si pendiente)
- ✍️ **Firma del administrador**

---

## ❓ Preguntas Frecuentes

### ¿Puedo crear mi propio DNI?

No, solo los administradores pueden crear DNIs. Pero puedes solicitar uno usando el sistema automático en el canal de solicitudes.

### ¿Los DNIs se pierden si el bot se reinicia?

No, todos los DNIs se guardan en `dnis_database.json` y persisten entre reinicios.

### ¿Puedo cambiar mi DNI después de creado?

No actualmente. Contacta a un administrador para crear uno nuevo.

### ¿Por qué no recibí mi DNI por DM?

Asegúrate de tener los mensajes privados activados desde miembros del servidor.

### ¿Puedo tener DNIs de varios países?

Sí, puedes solicitar un DNI por cada país disponible.

### ¿Los códigos QR son funcionales?

Sí, contienen información del DNI que puede ser escaneada.

### ¿Cómo sé si mi solicitud fue procesada?

El bot añadirá una reacción ✅ a tu mensaje de solicitud.

### ¿Cuánto tarda en firmarse un DNI?

Depende de cuándo un administrador esté disponible para firmar.

---

## 🔧 Solución de Problemas

### El bot no responde a comandos

**Solución:**
1. Verifica que el bot esté online (luz verde)
2. Comprueba que tienes permisos
3. Intenta `/ayuda_dni` para probar

### Error: "Falta discord.py"

**Solución:**
```bash
pip install discord.py
```

### Error: "No se encontró la fuente"

**Solución:**
1. Descarga Inter-Regular.ttf
2. Colócala en la carpeta `fonts/`
3. Reinicia el bot

### El bot no detecta solicitudes automáticas

**Solución:**
1. Verifica que el canal esté configurado con `/config_canales`
2. Asegúrate de que el mensaje empiece con "DNI nuevo"
3. Verifica que el formato sea exacto (con dos puntos después de cada campo)

### Error: "Solo los administradores pueden firmar DNIs"

**Solución:**
1. Verifica que tengas el rol configurado en `ADMIN_ROLE_ID`
2. Pide a un administrador del servidor que te asigne el rol

### El DNI no se envía por DM

**Solución:**
1. Activa "Permitir mensajes directos de miembros del servidor" en Privacidad
2. Si no funciona, el DNI se publica en el canal configurado

### Error al generar imagen

**Solución:**
```bash
pip install --upgrade Pillow
```

### El bot se desconecta constantemente

**Solución:**
- Verifica tu conexión a internet
- Comprueba que el token sea correcto
- Revisa si hay errores en la consola

---

## 📞 Soporte

Si tienes problemas:

1. Revisa esta documentación
2. Verifica la sección de solución de problemas
3. Consulta los logs en la consola
4. Contacta al desarrollador del bot en tu servidor

---

## 📝 Notas Importantes

- ⚠️ **Nunca compartas tu token del bot** - Es como tu contraseña
- 🔄 **Haz backups** del archivo `dnis_database.json` regularmente
- 📊 **Monitorea el uso** con `/stats_dni`
- 🔐 **Solo admins de confianza** deben tener el rol configurado
- 💾 **El archivo de base de datos** crece con cada DNI

---

## 🎉 ¡Disfruta del Sistema de DNI!

Este bot fue diseñado para hacer la gestión de documentos virtuales fácil y automática. Si tienes sugerencias o encuentras bugs, contacta a tu administrador.

**Versión:** 2.0  
**Última actualización:** 2025  
**Desarrollado para:** Servidores de roleplay y comunidades
