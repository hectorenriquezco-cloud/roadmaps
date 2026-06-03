# POC — Roadmap Contracargos en GitHub Pages

HTML mínimo y responsive para validar el deployment a GitHub Pages antes de construir la versión completa con sync a Jira.

## Qué incluye

- Single-file `index.html` (autocontenido, sin dependencias externas)
- 11 items de ejemplo distribuidos en 3 streams × 4 trimestres
- **Responsive:** desktop muestra swimlanes + timeline; mobile colapsa a tarjetas verticales
- Banner POC visible para evitar confusión con la versión real

## Para validar localmente

```bash
open index.html
```

Para probar la vista móvil: DevTools → toggle device toolbar → iPhone/Galaxy.

## Para deployar a GitHub Pages (pasos manuales — sin `gh` CLI)

### 1. Crear el repo en GitHub

1. Ir a https://github.com/new
2. **Name:** `roadmaps` (o el que prefieras — el URL final será `https://<usuario>.github.io/<nombre-repo>/`)
3. **Visibility:** Public (GH Pages free requiere público)
4. **Initialize:** déjalo vacío (no agregues README ni .gitignore)
5. Click "Create repository"

### ✅ Estado actual (2026-06-02)

- Repo: https://github.com/hectorenriquezco-cloud/roadmaps
- **URL público:** https://hectorenriquezco-cloud.github.io/roadmaps/

### 2. Push del POC al repo

Desde esta carpeta:

```bash
cd /Users/hectorenriquez/Documents/github/chargebacks_anb/roadmap_poc

git init
git add index.html README.md
git commit -m "POC: roadmap responsive en GitHub Pages"

# Reemplaza <usuario> y <repo> con los tuyos:
git remote add origin https://github.com/hectorenriquezco-cloud/roadmaps
git branch -M main
git push -u origin main
```

Si te pide autenticación, usa un **personal access token** (Settings → Developer settings → Personal access tokens → Tokens classic, con scope `repo`).

### 3. Habilitar GitHub Pages

1. En el repo → **Settings** → **Pages** (sidebar izquierdo)
2. **Source:** Deploy from a branch
3. **Branch:** `main`, **Folder:** `/ (root)`
4. Click **Save**
5. Esperar 30-60 segundos
6. GitHub te da el URL: `https://<usuario>.github.io/<repo>/`

### 4. Validar

- Abrir el URL en tu navegador (desktop)
- Abrir el mismo URL en tu celular para validar mobile
- Si se ve igual que el `open index.html` local → ✅ POC exitoso

## Cuando POC esté validado

Pasos siguientes para la versión real:
1. Crear `config.yaml` con todos los streams + items del roadmap completo (`../roadmap/index.html` actual)
2. Crear `refresh.py` que pulla Jira con un token API
3. Modificar `index.html` para hacer `fetch('data.json')` en lugar de tener data hardcodeada
4. Setup GitHub Action en `.github/workflows/refresh.yml` con cron horario
5. Guardar `JIRA_API_TOKEN` + `JIRA_EMAIL` como Secrets del repo

Ver contexto completo: [`../docs/context_roadmap_vivo_jira.md`](../docs/context_roadmap_vivo_jira.md)
