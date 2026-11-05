# Cruce RMH vs RPL

Página de una sola pieza (`index.html`) para comparar el stock en tienda del **RMH** (Stock Diario) contra el del **RPL** (`Rpl_KSD_…csv`), por tienda, modelo-color y talla.

Los archivos se leen en el navegador. No se suben a ningún servidor ni se guarda nada.

## Cómo se usa

1. Abre `index.html` en el navegador (o la página publicada, si este repositorio tiene GitHub Pages activo).
2. Arrastra el libro del RMH (`.xlsx`, hoja `stockrcp`) en la tarjeta RMH.
3. Arrastra el RPL (`.csv`, separado por `;`) en la tarjeta RPL.
4. Lee el Resumen y baja al detalle con las pestañas.

Hasta que cargues los dos archivos, la página muestra datos de ejemplo marcados como tales.

## Qué compara

| | RMH | RPL |
|---|---|---|
| Hoja o archivo | hoja `stockrcp` (si no existe, `Stock` o `Consulta`; también sirve un `.csv` con las mismas columnas) | `Rpl_KSD_….csv` |
| Tienda | `Storeid` | `IDSTORE` |
| SKU | `CodigoGp` | `ITEMCODE` |
| Cantidad | columna `Stock` (en la hoja `Stock` antigua hay también `total`, stock + fl) | `STK_TDA` (en tienda), o `STK_TOT` (con tránsito) |

- **Δ = RPL − RMH.** Positivo significa que el RPL tiene de más.
- **Desvío bruto** es la suma de |Δ| por SKU. Muestra las diferencias que el neto compensa entre sí.
- Las tiendas que están en un solo archivo quedan fuera del cruce, para no contarlas como diferencia. Se ven en la pestaña Cobertura.
- Solo entran estas marcas: Caterpillar, Converse, Fila, Hi-Tec, Merrell, Umbro, New Balance, Steve Madden, Madden Girl y Madden. La lista está en la constante `BRANDS_OK` de `index.html`. Todas las líneas entran; sin selección se comparan todas.
- Los nombres de tienda salen del RPL, porque la hoja `stockrcp` no los trae.
- «Excluir solo RMH» quita los SKU que RMH tiene en una tienda y el RPL no ve, y recalcula todos los totales.

## Pestañas

Resumen (con tablas por marca y por línea) · Por tienda · Por modelo-color · Tienda × modelo-color (con las tallas de cada fila) · Cobertura.

Cada tabla se puede ordenar y copiar para pegarla en Excel.

## Detalles técnicos

- HTML, CSS y JavaScript sin paso de compilación.
- Lee el `.xlsx` con [fflate](https://github.com/101arrowz/fflate) (cargada desde jsDelivr) y recorre solo la hoja necesaria, así que un libro de 100 MB carga en unos segundos.
- Tipografías IBM Plex desde Google Fonts, con tipografías del sistema como respaldo.
- Tema claro y oscuro según el sistema.
