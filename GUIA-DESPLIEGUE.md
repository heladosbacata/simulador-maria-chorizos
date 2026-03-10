# Guía: GitHub, servidor local y Vercel

Sigue estos pasos en orden.

---

## Parte 1: Subir el proyecto a GitHub

### 1.1 Inicializar Git (si no lo has hecho)

En la terminal, dentro de la carpeta del proyecto:

```bash
cd /Users/mac/Desktop/simulador-franquicias
git init
```

### 1.2 Añadir archivos y primer commit

```bash
git add .
git status
git commit -m "Initial commit: simulador María Chorizos"
```

### 1.3 Crear el repositorio en GitHub

1. Entra en [github.com](https://github.com) e inicia sesión.
2. Clic en **"+"** (arriba derecha) → **"New repository"**.
3. **Repository name:** por ejemplo `simulador-maria-chorizos`.
4. Descripción opcional: "Simulador de rentabilidad - María Chorizos".
5. Elige **Public**.
6. **No** marques "Add a README" (ya tienes archivos locales).
7. Clic en **"Create repository"**.

### 1.4 Conectar tu carpeta local con GitHub y subir

En la terminal (sustituye `TU_USUARIO` y `simulador-maria-chorizos` por tu usuario y nombre del repo):

```bash
git remote add origin https://github.com/TU_USUARIO/simulador-maria-chorizos.git
git branch -M main
git push -u origin main
```

Si GitHub te pide autenticación:
- **Usuario:** tu usuario de GitHub.
- **Contraseña:** usa un **Personal Access Token** (no la contraseña de la cuenta). Crear uno: GitHub → Settings → Developer settings → Personal access tokens → Generate new token (con permiso `repo`).

---

## Parte 2: Servidor local para desarrollar

Sirve la carpeta por HTTP para probar como en un sitio real (rutas, CORS, etc.).

### Opción A: Python (viene en macOS)

```bash
cd /Users/mac/Desktop/simulador-franquicias
python3 -m http.server 8000
```

Abre en el navegador: **http://localhost:8000**  
Para parar: `Ctrl + C`.

### Opción B: npx serve (Node.js)

```bash
cd /Users/mac/Desktop/simulador-franquicias
npx serve -l 3000
```

Abre: **http://localhost:3000**  
Para parar: `Ctrl + C`.

### Opción C: Abrir el HTML directamente

Doble clic en `index.html` o arrástralo al navegador. Funciona, pero sin “servidor” (algunas APIs o recursos pueden comportarse distinto).

---

## Parte 3: Desplegar en Vercel

### 3.1 Cuenta e instalación (opcional)

1. Entra en [vercel.com](https://vercel.com) y regístrate (puedes usar **"Continue with GitHub"**).
2. (Opcional) Instalar CLI para desplegar desde la terminal:
   ```bash
   npm i -g vercel
   ```

### 3.2 Conectar el repo de GitHub (recomendado)

1. En Vercel: **Add New…** → **Project**.
2. **Import Git Repository** → conecta GitHub si no lo has hecho.
3. Elige el repo `simulador-maria-chorizos` (o el nombre que hayas usado).
4. **Configure Project:**
   - **Framework Preset:** Other (o no cambiar nada).
   - **Root Directory:** `.` (dejar por defecto).
   - **Build Command:** vacío (no hay build).
   - **Output Directory:** vacío o `.` (Vercel sirve los archivos estáticos).
5. Clic en **Deploy**.

En unos segundos tendrás una URL tipo:  
`https://simulador-maria-chorizos-xxx.vercel.app`.

### 3.3 Despliegue desde la terminal (alternativa)

Con la CLI instalada, dentro del proyecto:

```bash
cd /Users/mac/Desktop/simulador-franquicias
vercel
```

Sigue las preguntas (login si hace falta, nombre del proyecto, etc.). Al final te dará la URL del despliegue.

---

## Flujo de trabajo diario

1. **Desarrollar en local:** edita archivos y prueba con `python3 -m http.server 8000` o `npx serve -l 3000`.
2. **Subir cambios a GitHub:**
   ```bash
   git add .
   git commit -m "Descripción del cambio"
   git push
   ```
3. **Vercel:** si el proyecto está conectado a GitHub, cada `git push` a `main` generará un nuevo despliegue automático.

---

## Resumen rápido

| Acción              | Comando / Dónde                          |
|---------------------|------------------------------------------|
| Servidor local      | `python3 -m http.server 8000` o `npx serve -l 3000` |
| Primer push a GitHub| `git init` → `git add .` → `git commit` → `git remote add origin ...` → `git push` |
| Deploy Vercel       | Conectar repo en vercel.com o usar `vercel` en la terminal |

Si quieres, en el siguiente paso podemos ejecutar juntos `git init`, `git add`, `git commit` y dejarlo listo para que tú añadas el `remote` y hagas el primer `git push` desde tu máquina.
