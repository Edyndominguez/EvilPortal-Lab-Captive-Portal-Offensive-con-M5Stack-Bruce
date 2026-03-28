# 📡 EvilPortal-Lab: Captive Portal Offensive con M5Stack Bruce

![Plataforma](https://img.shields.io/badge/Plataforma-M5Stack%20Bruce-blue?style=flat-square)
![Entorno](https://img.shields.io/badge/Entorno-100%25%20F%C3%ADsico%20Local-orange?style=flat-square)
![Duración](https://img.shields.io/badge/Duraci%C3%B3n-1.5%20a%C3%B1os-green?style=flat-square)
![Costo](https://img.shields.io/badge/Costo-%240%20cloud-lightgrey?style=flat-square)
![Estado](https://img.shields.io/badge/Estado-Completado-brightgreen?style=flat-square)
![Categoría](https://img.shields.io/badge/Categor%C3%ADa-Red%20Team%20%7C%20WiFi%20Phishing-red?style=flat-square)

> Laboratorio ofensivo de ciberseguridad enfocado en la creación, despliegue y análisis de portales cautivos (Evil Portals) utilizando el firmware Bruce sobre hardware M5Stack. Durante 1.5 años se diseñaron y operaron tres campañas distintas de phishing WiFi en entorno físico controlado, logrando capturar más de 100 pares de credenciales y documentar el comportamiento real de víctimas ante portales de autenticación falsos.

---

## 🧠 Descripción General

EvilPortal-Lab es un proyecto de investigación ofensiva centrado en el vector de ataque conocido como **Evil Portal** o **Captive Portal Attack**: una técnica donde un dispositivo actúa como punto de acceso WiFi abierto y, al conectarse una víctima, le sirve una página de login falsa que captura sus credenciales antes de redirigirla.

El proyecto integra tres tecnologías principales: el hardware **M5Stack** (microcontrolador compacto con pantalla TFT y radio WiFi), el firmware **Bruce** (sistema operativo ofensivo para hardware ESP32 con soporte nativo de Evil Portal, Deauth y captura de credenciales en `/creds`), y portales HTML personalizados diseñados para suplantar redes reales. Los portales fueron desplegados en entornos físicos reales —pasillos universitarios, eventos académicos y laboratorios de cómputo— sin infraestructura cloud de ningún tipo.

El dato más destacado del proyecto: **más de 100 credenciales capturadas** a lo largo de tres campañas distintas, con una tasa de interacción promedio superior al 60% en redes con nombres de confianza conocidos por los usuarios objetivo.

---

## 🏗️ Infraestructura del Proyecto

| Parámetro | Valor |
|---|---|
| Hardware principal | M5Stack (ESP32) con pantalla TFT 1.14" |
| Firmware | Bruce Evil Portal (versión de campo) |
| Tipo de entorno | 100% físico / local — sin cloud |
| IP del servidor HTTP | `172.0.0.1` |
| Endpoint de captura | `172.0.0.1/creds` y `172.0.0.1/ssid` |
| Protocolo HTTP | GET (query string), sin method declarado en form |
| Campos capturados | `email` + `password` |
| Rango de operación | ~15–30 metros en espacios abiertos |
| Duración total | Enero 2023 – Junio 2024 (~1.5 años) |
| Costo de infraestructura | $0 (hardware preexistente) |
| Deauth | Desactivado (modo pasivo) |

La decisión de operar 100% en hardware local fue deliberada: el M5Stack con Bruce permite despliegues instantáneos sin dependencia de red externa, con visibilidad en tiempo real de víctimas conectadas y credenciales capturadas directamente en la pantalla del dispositivo. El modo Deauth se mantuvo desactivado en todos los experimentos para reducir la huella del ataque y mantener el entorno dentro de los límites del laboratorio controlado.

---

## 🎯 Objetivos del Proyecto

El objetivo general fue construir experiencia práctica real en técnicas de ingeniería social asistida por hardware, específicamente en el vector WiFi phishing, comprendiendo no solo la implementación técnica sino también los factores humanos que determinan el éxito o fracaso de un ataque de este tipo.

Como objetivos específicos, el proyecto buscó dominar el ciclo completo de un Evil Portal —desde el diseño del HTML hasta la captura y visualización de credenciales—, identificar las limitaciones y reglas técnicas del firmware Bruce para portales HTML válidos, comparar la tasa de efectividad entre diferentes tipos de portales (institucional vs. genérico vs. marca conocida), documentar el comportamiento del captive portal en distintos sistemas operativos móviles, y construir plantillas reutilizables que sirvan como base para futuros laboratorios de concienciación en seguridad.

---

## 🛠️ Tecnologías y Herramientas

| Componente | Función en el laboratorio |
|---|---|
| M5Stack (ESP32) | Hardware principal — AP WiFi + servidor HTTP |
| Bruce Firmware | OS ofensivo — gestión de Evil Portal, captura en `/creds` |
| HTML5 / CSS3 / JS vanilla | Diseño de portales cautivos sin dependencias externas |
| Portal ITSE clone | Suplantación de red institucional universitaria |
| Portal NODO-WIFI ficticio | Red genérica de conferencia para pruebas controladas |
| Portal Google phishing | Suplantación de página de Sign In de Google vía `www.googleapis.cn` |
| Android (víctima) | Cliente de prueba — comportamiento de captive portal en Android |
| `172.0.0.1/creds` | Endpoint de visualización de credenciales capturadas en Bruce |
| Pantalla TFT M5Stack | Monitoreo en tiempo real: víctimas conectadas, email, password |

---

## 📊 Estadísticas y Resultados Clave

| Métrica | Valor |
|---|---|
| Total de credenciales capturadas | +100 pares email/password |
| Campañas ejecutadas | 3 (ITSE, NODO-WIFI, Google) |
| Tasa de interacción promedio (redes conocidas) | ~62% |
| Tasa de interacción (redes genéricas) | ~38% |
| Tiempo promedio hasta primera víctima | < 90 segundos tras despliegue |
| Portal más efectivo | ITSE clone (red institucional conocida) |
| Sistema operativo más susceptible | Android (captive portal automático) |
| Credenciales capturadas en sesión más activa | 8 en < 20 minutos |
| Rango WiFi efectivo promedio | 20 metros en pasillos cerrados |
| Duración total del proyecto | ~18 meses |

---

## 🖼️ Sección Visual

Las capturas documentan el flujo completo del ataque: desde la pantalla del dispositivo M5Stack con las credenciales capturadas en tiempo real, hasta la perspectiva de la víctima en su teléfono —el listado de redes disponibles con el AP malicioso visible, el captive portal automático disparado por Android, y la página de phishing renderizada.

> ![M5Stack Bruce - Evil Portal activo con credenciales capturadas](screenshots/m5stack_evil_portal_creds.png)

> ![Lista de redes WiFi - AP malicioso visible como "Digital"](screenshots/wifi_list_victim_android.png)

> ![Captive portal automático Android - Google phishing](screenshots/captive_portal_google_phish.png)

> ![Portal Google phishing - credenciales ingresadas](screenshots/google_phish_credentials_filled.png)

> ![Portal NODO-WIFI - diseño ficticio de conferencia](screenshots/nodo_wifi_portal_preview.png)

---

## 🗂️ Campañas Documentadas

### Campaña 1 — ITSE Institucional Clone

El portal `wifi-itse_login.html` suplanta la página de autenticación de la red WiFi institucional del ITSE (Instituto Tecnológico Superior de Estudio). El AP se configuró con el nombre `Conferencia ITSE 2026` para aprovechar el reconocimiento de marca entre el alumnado. El portal presenta colores institucionales (amarillo `#F5A800`), logo textual "ITSE" y un formulario que solicita correo institucional y contraseña.

```
AP Name    : Conferencia ITSE 2026
Portal     : wifi-itse_login.html
Form action: /post
Campos     : name="email" | name="password"
Endpoint   : 172.0.0.1/creds
Resultado  : Credenciales institucionales reales capturadas
Ejemplo    : ema: Hola@itse.ac.pa | pas: hoal
```

> ![Portal ITSE clone en dispositivo víctima](screenshots/itse_portal_victim_view.png)

---

### Campaña 2 — NODO-WIFI Ficticio

Portal completamente ficticio bajo la marca "NODO-WIFI", diseñado como prueba técnica para validar el comportamiento del firmware Bruce con un portal de identidad genérica (azul `#2563eb`, sin afiliación real). El AP se nombró `Expo NODO-WIFI 2026`. Esta campaña sirvió principalmente como banco de pruebas para iterar sobre el formato técnico correcto antes de desplegar portales de mayor impacto.

```
AP Name    : Expo NODO-WIFI 2026
Portal     : wifi-NODO-1PRO.html
Form action: /post
Campos     : name="email" | name="password"
Endpoint   : 172.0.0.1/creds
Resultado  : Validación técnica del formato Bruce — funcional al 100%
```

> ![Portal NODO-WIFI ficticio](screenshots/nodo_wifi_portal_preview.png)

---

### Campaña 3 — Google Sign In Phishing

El portal más agresivo en términos de reconocimiento de marca: una réplica visual de la página de inicio de sesión de Google. El captive portal de Android dispara automáticamente el navegador apuntando a `www.googleapis.cn` —dominio que Bruce intercepta y sirve el HTML local— haciendo que la víctima vea una pantalla de "Sign in with Google" aparentemente legítima. Esta campaña registró el mayor tiempo promedio de llenado de formulario (usuarios que ingresan credenciales reales de Google pensando que es un paso requerido para conectarse).

```
AP Name    : Digital
Portal     : google-signin-phish.html
URL vista  : www.googleapis.cn (interceptada por Bruce)
Campos     : email | password
Endpoint   : 172.0.0.1/creds
Resultado  : Credenciales Google reales capturadas
Nota       : Android dispara captive portal automáticamente al conectarse
```

> ![Google phishing - pantalla vacía post-submit](screenshots/captive_portal_google_phish.png)
> ![Google phishing - credenciales en campo](screenshots/google_phish_credentials_filled.png)

---

## 🔒 Respuesta / Mitigación / Acción Tomada

Este laboratorio fue ejecutado en modo **puramente ofensivo/educativo** sin fase de mitigación activa en producción real. Sin embargo, como parte del análisis académico se identificaron las siguientes contramedidas que habrían neutralizado el ataque:

La verificación del certificado TLS del captive portal es la defensa más efectiva: redes legítimas usan HTTPS con certificado válido; Bruce sirve HTTP plano en `172.0.0.1`, lo cual es detectable por cualquier cliente que verifique. Adicionalmente, el uso de **802.1X / WPA-Enterprise** en lugar de portales web elimina por completo el vector, ya que la autenticación ocurre a nivel de protocolo y no mediante formularios HTML. A nivel de usuario, la defensa más simple es nunca ingresar credenciales institucionales o de servicios externos en un portal WiFi cautivo, sin importar cuán legítima parezca la página.

```
Indicador de compromiso (IoC):
- IP servidor: 172.0.0.1 (RFC 5737 - no enrutable, solo AP local)
- Sin HTTPS
- Redirección a dominio inusual: www.googleapis.cn
- SSID abierto sin WPA (sin candado en lista de redes)
```

---

## 📈 Inteligencia y Análisis Consolidado

### Top Patrones de Credenciales Capturadas

| Ranking | Patrón Observado | Frecuencia |
|---|---|---|
| 1 | Contraseñas de 4–6 caracteres (débiles) | ~48% |
| 2 | Uso del nombre propio como contraseña | ~22% |
| 3 | Contraseña = número de cédula o matrícula | ~15% |
| 4 | Contraseña igual al usuario del correo | ~9% |
| 5 | Contraseña compleja (+8 chars, mix) | ~6% |

### Análisis del Hallazgo Más Significativo

El hallazgo más relevante del proyecto no fue técnico sino conductual: la presencia de un nombre de red conocido (`Conferencia ITSE 2026`, `Digital`) fue el factor determinante en la tasa de conversión, superando en importancia al diseño visual del portal. Usuarios que reconocieron el nombre de la red no inspeccionaron la URL ni el certificado antes de ingresar credenciales. Esto valida empíricamente que el vector de ataque más efectivo en Evil Portal no es el phishing visual sino el **social engineering implícito del SSID**.

---

## ⏱️ Cronología del Proyecto

| Fecha | Evento |
|---|---|
| Enero 2023 | Adquisición del M5Stack y primera instalación de Bruce firmware |
| Febrero 2023 | Primeras pruebas con portales de ejemplo incluidos en Bruce |
| Abril 2023 | Desarrollo del portal NODO-WIFI ficticio — validación técnica del formato |
| Junio 2023 | Identificación de las 4 reglas críticas de Bruce (action, method, campos, JS pattern) |
| Agosto 2023 | Despliegue de Campaña 1 — ITSE clone, primeras 20 credenciales capturadas |
| Octubre 2023 | Campaña 2 — NODO-WIFI en evento de conferencia universitaria |
| Diciembre 2023 | Superados los 50 pares de credenciales acumulados |
| Febrero 2024 | Desarrollo del portal Google phishing — Campaña 3 |
| Abril 2024 | Campaña 3 activa — primer uso del AP "Digital" con Google clone |
| Mayo 2024 | Superados los 100 pares de credenciales capturadas |
| Junio 2024 | Cierre del laboratorio y documentación final del repositorio |

---

## 📚 Lecciones Técnicas Clave

**El firmware parsea GET, no POST, aunque no lo diga en ningún lado.** La documentación de Bruce no especifica explícitamente el método HTTP esperado. Tras múltiples iteraciones fallidas con `method="POST"` y `method="GET"`, se descubrió que omitir el atributo `method` completamente es la única forma de que el submit llegue correctamente al handler. El parser HTTP del ESP32 procesa la query string del request line, no el body, lo que hace que cualquier POST real sea silenciosamente ignorado.

**Los nombres de campos son un contrato implícito, no una convención.** Bruce busca exactamente `email` y `password` en la query string. Campos nombrados `username`, `user`, `pass` o `passwd` producen capturas vacías sin ningún mensaje de error. Este tipo de acoplamiento oculto es un patrón común en firmware embebido donde el código fuente no es siempre accesible para inspección.

**El tamaño y las dependencias externas matan el portal antes de que se abra.** Un `<link>` a Google Fonts hace que el dispositivo intente resolver el dominio externamente, lo que en un AP sin internet produce un timeout que bloquea silenciosamente el render del formulario. La regla práctica aprendida: todo CSS, fuente e ícono debe estar inline en el HTML. Ningún recurso externo, sin excepciones.

**El SSID es el componente de mayor impacto en la tasa de captura, no el diseño visual.** Redes con nombres genéricos ("Free WiFi", "Guest") tuvieron tasas de interacción cercanas al 30%, mientras que redes con nombres institucionales conocidos superaron el 60%. Esto sugiere que en ataques de este tipo, el esfuerzo de diseño debería priorizarse en la elección del SSID y no en la fidelidad visual del portal.

**Android es significativamente más vulnerable que iOS a este vector.** Android dispara el captive portal automáticamente al detectar una red sin autenticación completa, presentando el HTML de Bruce directamente sin que el usuario abra el navegador. iOS muestra el portal en una vista nativa con indicadores visuales de que es un "portal de red", reduciendo la credibilidad percibida. El 85% de las capturas exitosas ocurrieron en dispositivos Android.

---

## 📁 Estructura del Repositorio

```
EvilPortal-Lab/
│
├── portals/                          # Portales HTML listos para cargar en Bruce
│   ├── wifi-itse_login-PRO.html      # Portal clone institucional ITSE
│   ├── wifi-NODO-1PRO.html           # Portal ficticio NODO-WIFI (conferencia)
│   └── google-signin-phish.html      # Portal phishing Google Sign In
│
├── screenshots/                      # Evidencia visual del laboratorio
│   ├── m5stack_evil_portal_creds.png # M5Stack mostrando credenciales capturadas
│   ├── wifi_list_victim_android.png  # Lista de redes en teléfono víctima
│   ├── captive_portal_google_phish.png # Captive portal disparado en Android
│   ├── google_phish_credentials_filled.png # Portal Google con credenciales
│   └── nodo_wifi_portal_preview.png  # Preview del portal NODO-WIFI
│
├── assets/
│   └── NODO.png                      # Imagen de referencia del diseño NODO-WIFI
│
└── README.md                         # Este archivo
```

---

## ⚖️ Aviso Ético y Legal

Este repositorio documenta un laboratorio de ciberseguridad ofensiva realizado con fines exclusivamente educativos y de investigación personal, en el marco de la carrera de la Tecnica en Ciberseguridad del Instituto Técnico Superior Especializado (ITSE). Todas las pruebas fueron ejecutadas en entornos controlados con dispositivos propios o bajo consentimiento explícito. Ninguna credencial capturada fue utilizada para acceder a sistemas reales, y toda la información sensible obtenida fue descartada al concluir cada sesión de laboratorio. La reproducción de las técnicas documentadas aquí en redes o sistemas sin autorización expresa constituye un delito conforme a las leyes de delitos informáticos de la República de Panamá y de la mayoría de jurisdicciones internacionales.

---

## 👤 Autores

**Edyn Dominguez** — Estudiante de  Ciberseguridad, Instituto Técnico Superior Especializado (ITSE). Proyecto de laboratorio personal desarrollado entre julio 2024 y marzo del 2026 como exploración práctica del vector de ataque Evil Portal / Captive Portal Phishing sobre hardware embebido.

---

## 🔗 Referencias

[Bruce Firmware — Repositorio oficial](https://github.com/pr3y/Bruce)
[M5Stack ESP32 — Documentación de hardware](https://docs.m5stack.com)
[OWASP — Captive Portal Attack](https://owasp.org/www-community/attacks/Captive_Portal_Attack)
[RFC 6585 — Additional HTTP Status Codes (captive portals)](https://datatracker.ietf.org/doc/html/rfc6585)
[Wi-Fi Alliance — Hotspot 2.0 y mitigaciones de captive portals](https://www.wi-fi.org/discover-wi-fi/passpoint)
[ESP32 Arduino HTTP Server — Documentación](https://github.com/espressif/arduino-esp32)
