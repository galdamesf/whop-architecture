# whop-architecture

Repositorio de documentación técnica y arquitectónica del proyecto **WHOP** — una plataforma SaaS para la venta y distribución de productos digitales.

Este repositorio centraliza todos los diagramas de arquitectura y flujos de procesos clave del sistema, mantenidos de forma versionada para facilitar la comprensión, revisión y evolución del proyecto por parte del equipo.

---

## Estructura del repositorio

```
whop-architecture/
│
├── arquitectura/
│   ├── diagrama-contexto.drawio
│   ├── diagrama-contexto.png
│   ├── diagrama-contenedores.drawio
│   └── diagrama-contenedores.png
│
├── componentes/
│   ├── diagrama-componentes-backend.drawio
│   ├── diagrama-componentes-backend.png
│   ├── diagrama-componentes-frontend.drawio
│   └── diagrama-componentes-frontend.png
│
├── flujos/
│   ├── Diagrama-Flujo-Registro.drawio
│   ├── Diagrama-Flujo-Registro.png
│   ├── Diagrama-Flujo-Producto.drawio
│   ├── Diagrama-Flujo-Producto.png
│   ├── Diagrama-Flujo-Compra.drawio
│   └── Diagrama-Flujo-Compra.png
│
└── README.md
```

---

## Diagramas de Arquitectura

### Diagrama de Contexto

Define los límites del sistema y sus relaciones con actores externos. Muestra la Plataforma SaaS WHOP en el centro, con sus 3 actores humanos (Comprador, Creador/Seller y Administrador) y 4 sistemas externos (Stripe, Discord/Telegram, Servicio de Email y CDN de archivos). Establece los flujos principales de comunicación hacia adentro y afuera de la plataforma.

### Diagrama de Contenedores

Muestra la arquitectura interna de la plataforma a nivel de contenedores. Detalla cómo se divide el sistema en sus bloques principales: el frontend desarrollado en Next.js 15, el backend en Node.js con NestJS, la base de datos PostgreSQL 16, el sistema de caché con Redis, el procesamiento de jobs asincrónicos con BullMQ y el almacenamiento de archivos con AWS S3. Define cómo se comunican estos contenedores entre sí y con los sistemas externos.

---

## Diagramas de Componentes

### Diagrama de Componentes — Backend

Documenta los 11 módulos que conforman el sistema backend: Auth, Marketplace, Products, Payments, Fulfillment, Tickets, Affiliates, Admin, Seller Dashboard, Stores y Notifications. Cada módulo está desglosado en su Controller, Services y Repository, con sus endpoints REST correspondientes. Los servicios externos (Stripe, Discord, Telegram, Email) están marcados como stubs pendientes de integración real.

### Diagrama de Componentes — Frontend

Documenta las 7 features que conforman el sistema frontend sobre Next.js 15 App Router: Auth, Marketplace, Account (Buyer), Store, Products, Notifications y Seller Dashboard. Cada feature está desglosada en sus componentes React, custom hooks, servicios y tipos TypeScript. Incluye la capa compartida global con componentes UI, utilidades, tipos globales y el cliente API base.

---

## Diagramas de Flujo

### Flujo 1 — Registro de Usuario, Verificación de Email y Creación de Tienda

Documenta el proceso mediante el cual un nuevo usuario crea su cuenta en la plataforma, verifica su identidad por email y configura su tienda como Seller. Cubre la validación de datos, la generación del token de verificación, la activación del panel de Seller y la creación de la tienda con validación de slug único.

**Actores:** Usuario / Seller, Sistema WHOP, EmailService (stub)

### Flujo 2 — Creación de Producto y Publicación en Marketplace

Documenta el proceso mediante el cual un Seller crea, configura y publica un producto en la plataforma. Cubre la selección del tipo de producto, la configuración del modelo de precio (único, suscripción o free trial), la configuración de archivos o integraciones, las reglas de acceso y el proceso de revisión y aprobación por parte del Administrador.

**Actores:** Seller, Administrador, Sistema WHOP

### Flujo 3 — Compra, Procesamiento de Pago y Entrega Automática de Acceso

Documenta el proceso completo mediante el cual un comprador adquiere un producto, procesa el pago a través de Stripe y recibe acceso automático al contenido. Cubre la autenticación del comprador, la creación de la orden, el procesamiento del pago con manejo de reintentos, la ejecución del FulfillmentService según el tipo de producto (archivo, licencia, Discord o Telegram) y el registro del acceso en product_access_logs.

**Actores:** Comprador, Sistema WHOP, Stripe (stub), EmailService (stub), Discord / Telegram (stub)

---

## Convenciones visuales

Todos los diagramas de flujo siguen la misma convención de colores:

| Color                    | Significado              |
| ------------------------ | ------------------------ |
| 🟢 Verde                 | Inicio / Fin del proceso |
| 🔵 Azul                  | Acción del Usuario       |
| 🟣 Morado                | Acción del Sistema       |
| 🟠 Naranja               | Decisión (SÍ / NO)       |
| 🔴 Rojo oscuro           | Error / Fin alternativo  |
| 🟣 Morado con borde rosa | Servicio Externo (stub)  |

---

## Herramienta utilizada

Todos los diagramas fueron creados con **[draw.io](https://app.diagrams.net)**. Los archivos `.drawio` pueden abrirse y editarse directamente en draw.io. Los archivos `.png` son exportaciones de alta calidad para visualización rápida.

---

## Versionado

Cada modificación a los diagramas debe registrarse con un commit descriptivo siguiendo la convención:

```
docs: descripción del cambio realizado
```

Ejemplos:

```
docs: actualiza diagrama de componentes backend con módulo Notifications
docs: corrige flujo de compra en manejo de reintentos
docs: agrega diagrama de contenedores v2
```

---

## Repositorios relacionados

- **whop-backend** — Código fuente del backend en Node.js / NestJS
- **whop-frontend** — Código fuente del frontend en Next.js 15
