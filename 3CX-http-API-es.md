# 3CX HTTP API
Documentación de la interfaz

**17 de febrero de 2022**  
*Andreas Olenitzack*

---

## Contenido

1. [Showallcalls](#1-showallcalls)
2. [Makecall](#2-makecall)
3. [Ready](#3-ready)
4. [Notready](#4-notready)
5. [Logout](#5-logout)
6. [Login](#6-login)
7. [dnregs](#7-dnregs)
8. [ondn](#8-ondn)
9. [getcallerid](#9-getcallerid)
10. [Drop](#10-drop)
11. [Answer](#11-answer)
12. [Record](#12-record)
13. [Transfer](#13-transfer)
14. [Park](#14-park)
15. [Unpark](#15-unpark)
16. [Atttrans](#16-atttrans)
17. [Setstatus](#17-setstatus)
18. [Showstatus](#18-showstatus)
19. [Divert](#19-divert)
20. [Stop](#20-stop)

---

### 1. Showallcalls

- **Llamada**:  
  ```
  http://IP:puerto/showallcalls
  ```
- **Valor devuelto**: Llamadas abiertas en formato HTML  
- **Función**: Devuelve todas las llamadas actualmente abiertas  
- **Ejemplo de respuesta**:  
  ```
  ID=98741:CCID=1:S=Connected:DN=xxxx:EP=+49xxxx:REC=Stop
  ```

### 2. Makecall

- **Llamada**:  
  ```
  http://IP:puerto/makecall/<extensión>/<destino>/<tipo-de-teléfono>
  ```
- **Valor devuelto**: ID de la llamada  
- **Función**: Crea una llamada usando los valores indicados  
- **Tipos de teléfono**:  
  1. Soft (Softphone 3CX)  
  2. Desktop (Teléfono físico)  
  3. Mobile (en preparación)  
- **Ejemplos**:  
  ```
  http://IP:puerto/makecall/10/11/Soft
  http://IP:puerto/makecall/10/11/Desktop
  ```

### 3. Ready

- **Llamada**:  
  ```
  http://IP:puerto/ready/<extensión>
  ```
- **Valor devuelto**: `true` / `is not an agent of the queues`  
- **Función**: Pone al agente en estado **Disponible** y lo registra en sus colas

### 4. Notready

- **Llamada**:  
  ```
  http://IP:puerto/notready/<extensión>
  ```
- **Valor devuelto**: `true` / `is not an agent of the queues`  
- **Función**: Pone al agente en estado **No disponible** (Custom 1) y lo desregistra de sus colas

### 5. Logout

- **Llamada**:  
  ```
  http://IP:puerto/logout/<extensión>
  ```
- **Valor devuelto**: `true` / `false`  
- **Función**: Desloguea al usuario de la cola y lo marca como **Ausente**

### 6. Login

- **Llamada**:  
  ```
  http://IP:puerto/login/<extensión>/<acción>
  ```
- **Acciones**:  
  - `login_all`  
  - `logout_all`  
- **Función**: Registra o desregistra al usuario en todas las colas

### 7. dnregs

- **Llamada**:  
  ```
  http://IP:puerto/dnregs/<extensión>
  ```
- **Valor devuelto**: Datos de registro de la extensión

### 8. ondn

- **Llamada**:  
  ```
  http://IP:puerto/ondn/<extensión>
  ```
- **Valor devuelto**: Datos de la conexión activa de la extensión

### 9. getcallerid

- **Llamada**:  
  ```
  http://IP:puerto/getcallerid/<extensión>
  ```
- **Valor devuelto**:  
  - `idle`  
  - Información de la llamada entrante  
- **Función**: Muestra el estado de la extensión; en llamadas entrantes indica de qué cola proviene la llamada

### 10. Drop

- **Llamada**:  
  ```
  http://IP:puerto/drop/<extensión>
  ```
- **Valor devuelto**: `true` / `false`  
- **Función**: Finaliza la llamada activa

### 11. Answer

- **Llamada**:  
  ```
  http://IP:puerto/answer/<extensión>
  ```
- **Valor devuelto**: `true` / `false`  
- **Función**: Atiende la llamada en el Softphone

### 12. Record

- **Llamada**:  
  ```
  http://IP:puerto/record/<extensión>/<acción>
  ```
- **Valor devuelto**: `true` / `false`  
- **Acciones**:  
  - `0` = start  
  - `1` = stop  
  - `2` = break  
  - `3` = resume  
- **Función**: Graba la llamada actual

### 13. Transfer

- **Llamada**:  
  ```
  http://IP:puerto/transfer/<extensión>/<destino>
  ```
- **Valor devuelto**: `true` / `false`  
- **Función**: Transfiere la llamada a la nueva destinación

### 14. Park

- **Llamada**:  
  ```
  http://IP:puerto/park/<extensión>/
  ```
- **Valor devuelto**: `true` / `false`  
- **Función**: Aparca la llamada activa en la posición de aparcamiento 0

### 15. Unpark

- **Llamada**:  
  ```
  http://IP:puerto/unpark/<extensión>/
  ```
- **Valor devuelto**: `true` / `false`  
- **Función**: Recupera la llamada aparcada de la posición 0

### 16. Atttrans

- **Llamada**:  
  ```
  http://IP:puerto/atttrans/<extensión>/
  ```
- **Valor devuelto**: `true` / `false`  
- **Función**: Conecta las llamadas activas para una transferencia asistida

### 17. Setstatus

- **Llamada**:  
  ```
  http://IP:puerto/setstatus/<extensión>/<acción>
  ```
- **Valor devuelto**: Estado actual de la extensión  
- **Acciones**:  
  - `"avail"` = Available  
  - `"away"` = Away  
  - `"oof"`   = Out of Office  
  - `"custom1"` = Custom 1  
  - `"custom2"` = Custom 2  
- **Función**: Establece el estado de la extensión

### 18. Showstatus

- **Llamada**:  
  ```
  http://IP:puerto/showstatus/<extensión>
  ```
- **Valor devuelto**: Estado actual de la extensión  
- **Función**: Muestra el estado de la extensión

### 19. Divert

- **Llamada**:  
  ```
  http://IP:puerto/divert/<extensión>/<destino>
  ```
- **Función**: Desvía la llamada a la destinación indicada

### 20. Stop

- **Llamada**:  
  ```
  http://IP:puerto/stop
  ```
- **Función**: Detiene el servicio de la API
