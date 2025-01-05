# WEB-CopiaDNI

https://copiadni.es/ 

https://copiadni.com/

CopiaDNi es una aplicación web para el procesamiento de documentos de identidad con un enfoque centrado en la privacidad, desarrollada con Node.js y alojada en una maquina virtual Ubuntu minimal con CloudPanel.io. Esta aplicación permite a los usuarios procesar imágenes de documentos de identidad de manera segura, convirtiéndolas a blanco y negro y añadiendo marcas de agua personalizables. Todo el procesamiento ocurre localmente en el navegador del usuario, garantizando la máxima privacidad y seguridad.

*Leer en: [Inglés](README.md), [Español](README_ES.md)*

## Infraestructura y Stack Tecnológico

La web está construida con JavaScript. La aplicación utiliza JavaScript tanto para la interfaz de usuario (frontend) como para el servidor (backend), lo cual es posible gracias a Node.js. Este enfoque unificado de desarrollo, utilizando un único lenguaje de programación en toda la aplicación, simplifica significativamente el desarrollo y mantenimiento. **En el frontend**, React sirve como el framework principal para construir la interfaz de usuario, proporcionando una experiencia fluida y responsive. Esto se complementa con Tailwind CSS, que proporciona estilos y diseños listos para usar. **En el backend**, Node.js actúa como el puente que permite que JavaScript se ejecute en el lado del servidor. Node.js nos permite utilizar JavaScript en toda la aplicación. Express.js, construido sobre Node.js, simplifica tareas comunes del servidor como servir archivos a los navegadores. **La aplicación** está alojada en una máquina virtual (instancia cloud) que ejecuta Ubuntu Minimal como sistema operativo. La aplicación Node.js se ejecuta y gestiona mediante PM2, un gestor de procesos que asegura su funcionamiento continuo y proporciona capacidades de reinicio automático. CloudPanel.io se utiliza como panel de control web para facilitar la administración del servidor.

### ¿Por qué Node.js?

Uso Node.js como base para esta aplicación web por la siguientes razones:

- **Ecosistema JavaScript**: Node.js permite utilizar JavaScript tanto en el cliente como en el servidor, proporcionando un lenguaje unificado en toda la pila de aplicaciones. Esto facilita el desarrollo y mantenimiento.
- **Rendimiento**: El modelo de E/S no bloqueante y dirigido por eventos de Node.js lo hace particularmente eficiente para servir aplicaciones web, especialmente aquellas que manejan conexiones concurrentes.
- **Ecosistema Rico de Paquetes**: El acceso a npm (Node Package Manager) proporciona una amplia biblioteca de paquetes y herramientas de código abierto que aceleran el desarrollo.
- **Desarrollo Moderno**: Integración con herramientas y prácticas de desarrollo actuales, incluyendo React para desarrollo frontend y Express.js para servicios backend.

El stack tecnológico completo incluye:

### Desarrollo Frontend
- **React 18**: Biblioteca de JavaScript para construir interfaces de usuario
- **Vite**: Herramienta de construcción frontend moderna que ofrece una experiencia de desarrollo más rápida
- **Tailwind CSS**: Framework CSS basado en utilidades para desarrollo rápido de interfaces

### Backend y Servidor
- **Node.js**: Entorno de ejecución para ejecutar JavaScript del lado del servidor
- **Express.js**: Framework de aplicaciones web para servir archivos estáticos
- **PM2**: Gestor de procesos para aplicaciones Node.js en producción

## Características Principales

La aplicación proporciona una forma sencilla y segura de procesar documentos de identidad:

- Procesamiento de imágenes completamente en el navegador sin almacenamiento en servidor
- Conversión de imágenes a blanco y negro
- Sistema de marca de agua personalizable con texto, colores y opacidad ajustables
- Aplicación de una sola página con interfaces modales intuitivas
- Arquitectura centrada en la privacidad
- Diseño responsivo para todos los dispositivos

## Estructura del Proyecto

```
.
├── src/
│   ├── components/
│   │   ├── image/
│   │   │   ├── CameraCapture.jsx
│   │   │   ├── ImagePreview.jsx
│   │   │   └── ImageUploader.jsx
│   │   ├── layout/
│   │   │   ├── Header.jsx
│   │   │   └── Body.jsx
│   │   └── ui/
│   │       ├── ActionButtons.jsx
│   │       ├── WatermarkControls.jsx
│   │       ├── InstructionsModal.jsx
│   │       └── LegalNotice.jsx
│   ├── utils/
│   │   └── imageProcessing.js
│   ├── assets/
│   │   └── react.svg
│   ├── App.jsx
│   ├── App.css
│   ├── main.jsx
│   └── index.css
├── public/
│   ├── vite.svg
│   └── ejemplo-procesado.jpg
├── server.js
├── vite.config.js
├── tailwind.config.js
├── postcss.config.js
├── eslint.config.js
├── package.json
└── package-lock.json
```

## Descripción de la Arquitectura Principal

Este repositorio incluye un archivo core.js que demuestra la estructura fundamental y el flujo de la aplicación. Este archivo sirve como documentación técnica que ilustra cómo interactúan los diferentes componentes dentro del sistema.

La descripción arquitectónica en core.js refleja la implementación real distribuida entre los componentes del proyecto, mostrando cómo la aplicación gestiona el procesamiento de imágenes, las interacciones de la interfaz de usuario y las medidas de seguridad. Proporciona información sobre la gestión del estado, la jerarquía de componentes y el proceso de procesamiento sin exponer detalles sensibles de la implementación.

La representación arquitectónica demuestra varios aspectos clave del sistema:

```mermaid
graph TD
    subgraph FlujoAplicacion
        UI[Interfaz de Usuario] --> IC[Captura/Subida de Imagen]
        IC --> P[Procesamiento]
        P --> D[Descarga]
    end

    subgraph EstructuraComponentes
        A[App.jsx] --> L[Componentes de Layout]
        A --> I[Componentes de Imagen]
        A --> C[Controles de UI]
        
        L --> H[Encabezado]
        L --> B[Cuerpo]
        
        I --> UP[Subida de Imagen]
        I --> CP[Captura de Cámara]
        I --> PR[Previsualización]
        
        C --> W[Controles de Marca de Agua]
        C --> AC[Botones de Acción]
    end

    style FlujoAplicacion fill:#f9f,stroke:#333,stroke-width:2px
    style EstructuraComponentes fill:#bbf,stroke:#333,stroke-width:2px
```

## Arquitectura de Desarrollo

```mermaid
flowchart TB
    subgraph "Entorno de Desarrollo"
        LC[Código Local] --> GT[Git]
        GT --> GH[Repositorio GitHub]
    end

    subgraph "Despliegue Automatizado"
        GH --> DP[Servicio Dploy]
        DP -->|Obtiene Código| SV[Servidor Ubuntu Minimal]
        DP -->|Instala Dependencias| NM[npm install]
        DP -->|Construye| BD[npm run build]
    end

    subgraph "Entorno de Producción CloudPanel.io"
        subgraph "Gestión del Servidor"
            CP[CloudPanel.io] -->|Gestiona| SV
            SV -->|Ejecuta| PM[PM2]
            PM -->|Administra| NS[Servidor Node.js]
        end

        subgraph "Aplicación de Una Página"
            NS -->|Sirve| SA[Archivos Estáticos]
            SA -->|Carga| RA[Aplicación React]
            RA -->|Procesa| IMG[Procesamiento de Imagen]
            IMG -->|Descarga| DL[Imagen Procesada]
        end
    end
```

## Funcionamiento

La aplicación sigue un flujo de trabajo seguro con procesamiento del lado del cliente:

1. **Subida de Documentos**: Los usuarios pueden subir imágenes de documentos a través de su navegador
2. **Procesamiento Local**: Las imágenes se procesan enteramente en el navegador del cliente:
   - Conversión a blanco y negro
   - Aplicación de marca de agua personalizada
   - Sin transmisión de datos a servidores externos
3. **Descarga**: Las imágenes procesadas están disponibles inmediatamente para su descarga
4. **Privacidad**: No se almacenan ni transmiten imágenes o datos

## Privacidad y Seguridad

La aplicación prioriza la privacidad y seguridad del usuario mediante:

- Procesamiento de todas las imágenes en el lado del cliente
- Sin almacenamiento de documentos en el servidor
- Cifrado SSL/TLS para todas las conexiones
- Actualizaciones y mantenimiento regular de seguridad

## Licencia

Este proyecto está licenciado bajo la Licencia GNU AGPLv3. Esto significa:

- Puedes ver y hacer fork de este repositorio
- Debes mantener la misma licencia para cualquier modificación
- Debes revelar el código fuente de cualquier modificación
- El uso comercial requiere permiso explícito

Ver el archivo [LICENSE](LICENSE) para más detalles.
