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

## Parte 3: Desplegar en Vercel (y que se actualice en cada push)

### 3.1 Conectar el repo de GitHub

1. Entra en [vercel.com](https://vercel.com) e inicia sesión con **GitHub**.
2. **Add New…** → **Project**.
3. **Import Git Repository** → selecciona `heladosbacata/simulador-maria-chorizos` (o tu repo).
4. **Configure Project:**
   - **Framework Preset:** Other.
   - **Root Directory:** `.`
   - **Build Command:** vacío.
   - **Output Directory:** `.` (o vacío).
5. **Deploy**.

### 3.2 Deploy automático en cada commit + push

Cuando el proyecto está **conectado a GitHub**, Vercel hace un **deploy nuevo cada vez que haces push** a la rama que tengas configurada (normalmente `main`).

- Cada `git push origin main` → Vercel detecta el cambio y vuelve a desplegar.
- No hace falta hacer nada en Vercel: solo commit + push desde tu máquina.
- Puedes ver el estado de cada deploy en el dashboard del proyecto en Vercel.

Si no se actualiza al hacer push, revisa en Vercel: **Project → Settings → Git** que el repositorio conectado sea el correcto y que la rama de producción sea `main`.

### 3.3 Despliegue desde la terminal (opcional)

Si prefieres desplegar sin GitHub:

```bash
npm i -g vercel
cd /Users/mac/Desktop/simulador-franquicias
vercel
```

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
