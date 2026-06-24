# QuinceDresses — Panel de Ventas

Dashboard estático de ventas para las tiendas QuinceDresses (NJ, VA, CT, NY).  
Funciona 100% en el navegador: no hay backend, no hay servidor, los datos de clientes nunca salen del dispositivo.

---

## Ver el dashboard

### Localmente (para revisar antes de publicar)

```bash
cd /ruta/a/la/carpeta
python3 -m http.server 8000
# Abre http://localhost:8000 en el navegador
```

> **Por qué hace falta un servidor local?**  
> Los navegadores bloquean la lectura de archivos locales por seguridad (`file://`).  
> Con `python3 -m http.server` se resuelve en segundos.

### En GitHub Pages (público)

1. Sube todos los archivos a un repo de GitHub (el `index.html` y los 4 CSV deben quedar en la **raíz** del repo).
2. Ve a **Settings → Pages → Branch: `main` → Folder: `/ (root)`** → Save.
3. En ~1 minuto la URL `https://TU_USUARIO.github.io/NOMBRE_REPO/` estará activa.

---

## Actualizar los datos (nuevos pedidos)

Los gráficos leen directamente los 4 CSV. Para actualizarlos:

1. Abre el Google Sheet de la tienda correspondiente.
2. **Archivo → Descargar → CSV (.csv)**.
3. Renombra el archivo descargado con el nombre exacto:
   - `Master QuinceCouture - NJ.csv`
   - `Master QuinceCouture - VA.csv`
   - `Master QuinceCouture - CT.csv`
   - `Master QuinceCouture - NY.csv`
4. Reemplaza el archivo viejo en la carpeta/repo.
5. Sube los cambios a GitHub (`git add . && git commit -m "actualiza datos" && git push`).  
   GitHub Pages se actualiza automáticamente en ~1 minuto.

---

## Estructura de archivos

```
/
├── index.html                       ← el dashboard (no tocar)
├── Master QuinceCouture - NJ.csv
├── Master QuinceCouture - VA.csv
├── Master QuinceCouture - CT.csv
├── Master QuinceCouture - NY.csv
└── README.md
```

---

## Columnas esperadas en los CSV

El dashboard lee estas columnas (case-sensitive tal como las exporta Google Sheets):

| Columna          | Descripción                         |
|------------------|-------------------------------------|
| `Code`           | Número/código del pedido            |
| `CLIENTE`        | Nombre del cliente                  |
| `FECHA DE ORDEN` | Fecha en que se tomó el pedido      |
| `EVENTO`         | Fecha del evento / quinceañera      |
| `COMPANIA`       | Marca del vestido                   |
| `ESTILO`         | Código de estilo                    |
| `COLOR`          | Color del vestido                   |
| `SIZE`           | Talla                               |
| `STATUS`         | Estado del pedido                   |

> Si alguna columna cambia de nombre en el Sheet, actualiza también el nombre en `index.html` (busca el string en el `<script>`).

---

## Privacidad

Los CSV **nunca se suben a ningún servicio externo**.  
PapaParse los descarga desde el mismo servidor que sirve el `index.html` y los procesa en el navegador del usuario.  
Quien acceda a GitHub Pages podrá ver los datos — si los CSV contienen información sensible, mantén el repositorio **privado** y usa GitHub Pages solo con plan de pago que soporte repos privados, o comparte el link solo internamente.
