# Fagor Comparator

Calculadora de comparación de máquinas de lavado Fagor (WRC/WRA y CCO) frente a modelos de la competencia. Calcula coste operativo, ahorro, TCO (coste total de propiedad) y ROI, y genera un informe descargable en PDF.

Sitio en producción: _((https://inakigoikofagor.github.io/fagor-comparator-v3/fagor_calculadora.html) — GitHub Pages, Cloudflare Pages, etc.)_

## Archivos del proyecto

Todo vive en la raíz del repositorio — **no en subcarpetas** — porque `fagor_calculadora.html` pide los CSV con ruta relativa (`./nombre.csv`).

| Archivo | Contenido |
|---|---|
| `fagor_calculadora.html` | La aplicación completa (HTML + CSS + JS en un solo archivo) |
| `1_Modelos_Fagor.csv` | Modelos Fagor (WRC/WRA/CCO): tanques por etapa, producción, consumo |
| `2_Tarifas_y_Precios.csv` | Precios PVP por modelo y por tarifa (00, E0, K0, P1, 30, 72) |
| `3_Paises_Tarifa.csv` | País → tarifa asignada → moneda local (columna `Moneda (ISO)`) |
| `4_Parametros_Calculo.csv` | Parámetros técnicos por defecto (temperaturas, dosificación) |
| `5_Modelos_Competencia.csv` | Modelos de competencia precargados (Meiko, Winterhalter...) |

**Importante:** los nombres de archivo distinguen mayúsculas/minúsculas en GitHub Pages y en la mayoría de hostings estáticos. Deben coincidir exactamente con la tabla de arriba.

## Cómo actualizar los datos (precios, modelos, países)

1. Descarga el CSV correspondiente, edítalo (Excel, Google Sheets...) manteniendo:
   - Separador `;` (punto y coma)
   - Codificación UTF-8 con BOM (estándar de Excel en español)
   - Mismos nombres de columna y mismo orden
2. Sube el CSV editado al repositorio, sustituyendo al anterior, **con el mismo nombre exacto**.
3. Espera 1-2 minutos y recarga la calculadora con Ctrl+Shift+R (para evitar caché).

## Cómo desplegar (GitHub Pages)

1. Sube estos 6 archivos a la raíz del repo (rama `main`).
2. Settings → Pages → Source: **"Deploy from a branch"** → Branch `main` → carpeta **`/ (root)`**.
3. La URL será `https://TU-USUARIO.github.io/NOMBRE-DEL-REPO/fagor_calculadora.html`.

## Lógica de moneda (resumen)

- **PVP / precio neto de tarifa**: en euros para casi todos los países, salvo Polonia (PLN), Reino Unido (GBP) y República Checa (CZK), que tienen tarifa propia — ver `TARIFA_CURRENCY` en el HTML.
- **Costes operativos, ahorro, coste/cesta**: en la moneda local del país seleccionado (columna `Moneda (ISO)` de `3_Paises_Tarifa.csv`).
- Los tipos de cambio se cargan de una API en vivo con una tabla de referencia fija integrada como respaldo (no depende de red para funcionar).

## Notas técnicas

- Aplicación 100% estática (sin backend propio). Autenticación de usuarios vía Supabase (externo).
- Sin build ni dependencias — es un único archivo HTML autocontenido.
