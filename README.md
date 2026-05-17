# 🎭 Funko Tracker

Una aplicación web moderna para gestionar entregas y ventas de figuras Funko, con sincronización automática en Google Drive.

## ✨ Características

### Gestión de Entradas
- **4 tipos de transacciones**: Venta presencial, Mercado Libre, Paquetería, Gastos
- **Estados duales**: Control independiente de pago y entrega
- **Seguimiento de anticipo**: Calcula automáticamente el monto pendiente por cobrar
- **Notas y metadata**: Campos adicionales para observaciones
- **Fotos**: Sube y visualiza imágenes de figuras (redimensionadas automáticamente)

### Vistas y Filtros
- **📦 Entregas**: Tabla agrupada por fecha con filtros por canal (HEB, Walmart, FedEx, ML, etc.)
- **⏳ Pendientes**: Tarjetas de entregas sin fecha asignada
- **🔮 Preventas**: Gestión de preventa de figuras
- **📊 Estadísticas**: Análisis financiero por período (semana, mes, todo)
- **⬆️ Importar**: Carga de datos desde Excel con preview

### Sincronización
- Almacenamiento en **Google Drive** (appDataFolder)
- Guardado automático cada 1.2 segundos
- Indicador de estado (Listo, Guardando, Error)
- Validación de sesión expirada

### Estadísticas
- Total de ingresos y gastos
- Ganancia neta
- Monto por cobrar vs cobrado
- Desglose por canal de entrega
- Filtros por período temporal

## 🚀 Inicio Rápido

### Requisitos
- Navegador moderno (Chrome, Firefox, Safari, Edge)
- Cuenta de Google
- Conexión a Internet

### Uso
1. Abre `index.html` en tu navegador
2. Haz clic en **"Iniciar sesión con Google"**
3. Autoriza el acceso a Google Drive (solo appDataFolder)
4. ¡Comienza a registrar tus ventas!

## 📋 Tipos de Entradas

| Tipo | Campos | Uso |
|------|--------|-----|
| **💚 Venta Presencial** | Monto, anticipo, comprador, canal | Ventas directas o punto de venta |
| **🟡 Mercado Libre** | Solo descripción y notas | Registrar envíos ML sin monto |
| **📦 Paquetería** | Monto, anticipo, transportista | Envíos por courier |
| **🔴 Gasto** | Monto (negativo) | Registro de gastos de operación |

## 📊 Estados

### Estado de Pago
- **🟡 Pendiente**: Aún no se ha cobrado
- **✅ Pagado**: Monto cobrado (con fecha de pago)

### Estado de Entrega
- **📫 Listo**: Disponible para entregar
- **📭 Sin fecha**: Coordinar fecha con cliente
- **🔮 Preventa**: Figura no disponible aún
- **📦 Sin asignar**: No clasificado

## 🔧 Estructura del Proyecto

```
funko-tracker/
├── index.html          # App completa (HTML + CSS + JS)
├── README.md          # Este archivo
└── [datos en Drive]   # funko-tracker-data.json (Google Drive)
```

## 🛠️ Tecnologías

- **Frontend**: HTML5, CSS3 (Grid, Flexbox, Variables CSS), JavaScript vanilla
- **API**: Google Drive API v3, OAuth 2.0
- **Importación**: SheetJS (XLSX)
- **Almacenamiento**: Google Drive (appDataFolder)
- **Estilos**: Dark mode con colores temáticos por canal

## 🎨 Temas de Color

```css
:root {
  --green: #22c55e      /* Ventas/Pagado */
  --red: #ef4444        /* Gastos/Error */
  --yellow: #f59e0b     /* ML/Pendiente */
  --cyan: #06b6d4       /* Paquetería */
  --accent: #a855f7     /* Preventa/Acciones */
  --orange: #f97316     /* Estafeta/Otros */
}
```

## 📥 Importar desde Excel

### Formato requerido
Columnas obligatorias en el Excel:
- `fecha` - Fecha de transacción (YYYY-MM-DD)
- `fechaPago` - Fecha de pago (opcional)
- `tipo` - venta, ml, pkg, gasto
- `desc` - Descripción/nombre figura
- `buyer` - Comprador
- `canal` - HEB, WALMART, FEDEX, CORREOS, etc.
- `monto` - Cantidad (negativa para gastos)
- `anticipo` - Anticipo recibido
- `estatusPago` - pendiente, pagado
- `estatusEntrega` - listo, sin-fecha, preventa, ninguno
- `notas` - Observaciones

### Proceso
1. Ve a la pestaña **⬆️ Importar**
2. Selecciona o arrastra tu archivo Excel
3. Revisa el preview
4. Haz clic en **⬆️ Importar a Drive**

## 🔐 Seguridad

- **Autenticación**: OAuth 2.0 con Google (no almacenamos credenciales)
- **Almacenamiento**: Google Drive (appDataFolder - privado)
- **Token**: Guardado en localStorage (solo para esta sesión)
- **Sesión**: Se valida automáticamente; si expira, se requiere re-autenticación
- **Datos**: Solo acceso de lectura/escritura al archivo de tu aplicación

## ⚡ Rendimiento

- Guardado automático con throttle de 1.2s
- Imágenes redimensionadas a máximo 600px de ancho
- Compresión JPEG 75% para fotos
- Búsqueda en tiempo real sin lag

## 🐛 Resolución de Problemas

### "Sesión expirada"
→ Recarga la página e inicia sesión nuevamente

### Las imágenes no se guardan
→ Verifica el tamaño (se redimensionan automáticamente a 600px)

### Los datos no se sincronizan
→ Verifica tu conexión a Internet y el indicador de sincronización

### El Excel no importa
→ Asegúrate de que tiene todas las columnas requeridas

## 📈 Mejoras Futuras

- [ ] Exportar a Excel/PDF
- [ ] Sincronización en tiempo real con múltiples dispositivos
- [ ] Gráficos avanzados (Chart.js)
- [ ] Categorización customizable de canales
- [ ] Backup automático
- [ ] Modo offline (Service Workers)
- [ ] App móvil nativa
- [ ] Integración con otros CRMs

## 📝 Notas de Uso

- **Todos los montos están en tu moneda local** (configurable según necesidad)
- **Las fotos se comprimen** para no saturar tu Drive
- **Los datos se guardan en tiempo real** - no hay botón "Guardar"
- **Puedes editar cualquier entrada** - los cambios se sincronizan inmediatamente
- **El estadístico se calcula en tiempo real** basado en fechas de pago

## 📞 Soporte

Para reportar bugs o sugerir mejoras, contacta al desarrollador.

---

**Última actualización**: Mayo 2026  
**Versión**: 1.0  
**Licencia**: Privada
