# 🚀 Sistema de Correos Masivos HIGH-PERFORMANCE V0.0.3

Sistema de envío de correos masivos de alto rendimiento con procesamiento paralelo, rate limiting inteligente y optimización extrema. Desarrollado por **Isaac Esteban Haro Torres**.

---

## 📝 Descripción

Sistema profesional de correo masivo diseñado para enviar miles de emails de forma eficiente, inteligente y cumplimiento-friendly.

### ¿Qué hace este proyecto?

- **Procesamiento paralelo**: Envíos simultáneos con múltiples threads
- **Rate limiting dinámico**: Se adapta a los límites del servidor SMTP
- **Cola de mensajes**: Sistema de cola para grandes campañas
- **Resume capability**: Continúa campañas interrumpidas
- **Smart retry**: Reintentos inteligentes con backoff exponencial
- **Balanceo de carga**: Distribuye carga entre múltiples cuentas SMTP

---

## ✨ Características Principales

| Característica | Descripción |
|----------------|-------------|
| ⚡ **Multi-threading** | Hasta 10 conexiones simultáneas |
| 🎯 **Rate limiting** | Configurable (emails/segundo) |
| 🔄 **Sistema de cola** | Persistencia para campañas grandes |
| 💾 **Checkpoint resume** | Continúa donde se quedó |
| 📊 **Dashboard CLI** | Monitoreo en tiempo real |
| 🔀 **Múltiples cuentas** | Balancea entre varias cuentas SMTP |
| ⏱️ **Backoff exponencial** | Manejo inteligente de errores 429 |

---

## 🛠️ Stack Tecnológico

- **Lenguaje**: Python 3.10+
- **Concurrencia**: threading, concurrent.futures
- **Colas**: queue.Queue, SQLite
- **Email**: smtplib, aiosmtplib (async)
- **Datos**: Pandas
- **CLI**: Rich (interfaz enriquecida)
- **Logging**: Python logging

---

## 🚀 Instalación y Uso

### Instalación

```bash
pip install pandas rich sqlalchemy aiosmtplib
```

### Uso básico de alto rendimiento

```python
from correohigh import CorreoMasivoHP

# Inicializar con múltiples cuentas
enviador = CorreoMasivoHP(
    cuentas_smtp=[
        {'user': 'cuenta1@email.com', 'pass': 'xxx', 'daily_limit': 500},
        {'user': 'cuenta2@email.com', 'pass': 'xxx', 'daily_limit': 500},
    ],
    max_workers=5,           # Hilos simultáneos
    rate_limit=10,           # 10 emails/segundo
    checkpoint=True          # Guardar progreso
)

# Ejecutar campaña
resultado = enviador.enviar_campana(
    plantilla="promocion.html",
    contactos="10000_leads.csv",
    asunto="Tu promoción exclusiva"
)

# Ver estadísticas
enviador.mostrar_dashboard()
```

### Configuración avanzada

```python
# Rate limiting inteligente
config = {
    'rate_limit': {
        'inicial': 5,           # Emails/segundo inicial
        'maximo': 20,           # Máximo configurable
        'incremento': 1,        # Aumento si no hay errores
        'decremento': 0.5,      # Reducción si hay errores
    },
    'retry': {
        'max_intentos': 3,
        'backoff_base': 2,      # 2^n segundos
    },
    'checkpoint': {
        'intervalo': 50,        # Guardar cada 50 emails
        'archivo': 'campana.db'
    }
}
```

---

## 📊 Dashboard en Tiempo Real

```
╔═══════════════════════════════════════════════════════════╗
║           🚀 CORREO MASIVO HP - DASHBOARD                ║
╠═══════════════════════════════════════════════════════════╣
║                                                           ║
║  📤 Enviados:     ████████████░░░░░░░░  1,250 / 10,000  ║
║                                                           ║
║  ⏱️  Velocidad:   8.5 emails/segundo                      ║
║  ⏳ Tiempo rest.: 17 minutos                              ║
║                                                           ║
║  ✅ Exitosos:    1,230 (98.4%)                            ║
║  ❌ Fallidos:       20 (1.6%)                             ║
║                                                           ║
║  🔄 En cola:        8,750                                 ║
║  💤 Hilos activos:   5/10                                ║
║                                                           ║
║  Cuenta activa: cuenta1@email.com (enviados: 487/500)  ║
╚═══════════════════════════════════════════════════════════╝
```

---

## 📁 Estructura del Proyecto

```
Correos_Masivos_v0.0.3/
├── TinkuDev_Correos_Masivos_Colegios_v0_0_3.ipynb
├── correohigh/                    # Módulo principal
│   ├── __init__.py
│   ├── sender.py                  # Envío paralelo
│   ├── queue.py                   # Sistema de cola
│   ├── rate_limiter.py           # Rate limiting
│   └── checkpoint.py              # Persistencia
├── cuentas_smtp.json              # Configuración multi-cuenta
├── Campanas/                      # Campañas guardadas
└── README.md
```

---

## 🎯 Casos de Uso Avanzados

1. **Grandes campañas**: 10,000+ emails sin problemas
2. **Agencias de marketing**: Múltiples clientes, múltiples cuentas
3. **Product launches**: Lanzamientos masivos exitosos
4. **Notificaciones masivas**: Sistemas de alerta a usuarios

---

## ⚡ Optimizaciones de Rendimiento

| Técnica | Descripción |
|---------|-------------|
| Connection pooling | Reutiliza conexiones SMTP |
| Batch processing | Agrupa envíos en batches |
| Async DNS | Resolución DNS no bloqueante |
| Compresión | Comprime cuerpos de email |
| Template caching | Cachea templates compilados |

---

## ⚠️ Mejores Prácticas

- **Respeta límites**: No excedas 500 emails/día por cuenta Gmail
- **Warming**: Comienza lento y aumenta gradualmente
- **Contenido**: Evita spam triggers en el asunto/cuerpo
- **Unsubscribe**: Siempre incluye enlace de cancelación

---

## 🔧 Comparación de Versiones

| Característica | v0.0.1 | v0.0.2 | v0.0.3 |
|----------------|--------|--------|--------|
| Envío básico | ✅ | ✅ | ✅ |
| HTML responsivo | ❌ | ✅ | ✅ |
| Tracking | ❌ | ✅ | ✅ |
| Multi-threading | ❌ | ❌ | ✅ |
| Rate limiting | ❌ | ✅ | ✅ |
| Multi-cuenta SMTP | ❌ | ❌ | ✅ |
| Resume capability | ❌ | ❌ | ✅ |

---

## 🤝 Contribuciones

¿Agregaste nuevas técnicas de optimización?
¡Abre un Pull Request!

---

## 👨‍💻 Desarrollado por Isaac Esteban Haro Torres

**Ingeniero en Sistemas · Full Stack · Automatización · Data**

- 📧 Email: zackharo1@gmail.com
- 📱 WhatsApp: 098805517
- 💻 GitHub: https://github.com/ieharo1
- 🌐 Portafolio: https://ieharo1.github.io/portafolio-isaac.haro/

---

© 2026 Isaac Esteban Haro Torres - Todos los derechos reservados.
