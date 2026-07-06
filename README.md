# SOCIAL OPLESK
### 🏴‍☠️ HACKS 
<br/>

## ⚡️ Hack Github Actions 2⚡️

<br />
<br />


**Requisitos previos**
<br/>

```diff
- NOTA HACER LAS PRÁCTICAS MEDIANTE LA CONSOLA - TERMINAL  
- Debes tener cuenta en vercel y usar la terminal de wsl en caso de emplear windows, ideal sobre debian / ubuntu / fedora.
```
|Hacks | Details | 
|----------|---------|
| H-1      | deploy index.html |
| H-2      | minify index.html mejorado |
<br/> 

## 🏆 H-1 

```

📁hack_gh_1/
├── .github/workflows/deploy.yml
├── index.html

```

1. Crear un directorio el archivo deploy.yml en un repositorio

2. Dentro del flow.yml pegar el script

3. Debes crear aplicar los ajustes necesarios

<br/> 
<img width="635" height="180" alt="image" src="https://github.com/user-attachments/assets/3c7df5aa-bb92-4b9c-9d41-bc13397efa6f" />

```
- Ve a Settings → Pages
```

<br/>
<img width="887" height="571" alt="image" src="https://github.com/user-attachments/assets/4d6eb894-efe9-45d3-a2e2-3e79137979c5" />

```
- Da click en Pages
```

<br/>
<img width="902" height="572" alt="image" src="https://github.com/user-attachments/assets/10f29fb4-a736-461e-9eec-10e497810caf" />

```
- En "Build and deployment" → Source:cambia "Deploy from a branch" por "Github Actions"
- Guarda. En 1-2 min tendrás la URL: https://TU_USUARIO.github.io/mi-sitio/
- Recuerda siempre sobre la Branch: main y carpeta / (root)
```

<br/>
⚡ Script html para el index.html

```
<!DOCTYPE html>
<html lang="">
<head>
  <meta charset="UTF-8" />
  <title>Hello, world!</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <meta name="description" content="" />
  <link rel="icon" href="favicon.png">
</head>
<body>
  <h1>Hello, world!</h1>
</body>
</html>
```

<br/>
🟢 Script github/actions del hack-1 a resolver 🟢

```
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  deploy:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Checkout
        uses: actions/checkout@v7

      - name: Setup Pages
        uses: actions/configure-pages@v5

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```


<br />
<br />



## 🏆 H-2

```

📁hack_gh_2/
├── .github/workflows/flow.yml

```

1. Crear un directorio el archivo flow.yml en un repositorio

2. Dentro del flow.yml pegar el script

3. Debes crear aplicar los ajustes necesarios 
     
```
❌ Mal(para versiones lo ideal es no aplicar el valor directamente)
      with:
          node-version: '20'

✅ Bien 
    with:
     ${{ env.NODE_VERSION }}

---

❌ Mal(evitar instalaciones globales, consumen mayor tiempo computo del runner)
   - name: install minifier-terser
     run: npm install html-minifier-terser -g

✅ Bien 
  - name: install minifier-terser
    run: npm install html-minifier-terser

---
✅ Bien(ideal para guardar el resultado final, de esta forma verificar la salida)
      - name: save output .dist/index.html
        uses: actions/upload-artifact@v4
        with:
          name: dist
          path: dist/
          retention-days: 10 

```

<br/>
⚡ Script html para el index.html

```
<!DOCTYPE html>
<html lang="">
<head>
  <meta charset="UTF-8" />
  <title>Hello, world!</title>
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <meta name="description" content="" />
  <link rel="icon" href="favicon.png">
</head>
<body>
  <h1>Hello, world!</h1>
</body>
</html>
```

<br/>
🟢 Script github/actions del hack-2 a resolver 🟢

```
name: deploy

on:
  push:
    branches:❓

  workflow_dispatch:

env:
  NODE_VERSION: '24'

jobs:
  deploy-to-vercel:
    runs-on: ubuntu-latest

    steps:
      - name: download project
        uses: actions/checkout@v5

      - name: install nodejs
        uses: actions/setup-node@v5
        with:
          node-version: ❓

      - name: install minifier-terser
        run: ❓

      - name: minify index.html
        run: |
          mkdir -p dist
          ./node_modules/.bin/html-minifier-terser --collapse-whitespace --remove-comments --minify-js true -o dist/index.html index.html

      - name: verificar minify
        run: |
          if [ ! -f ./dist/index.html ]; then
              echo "no found index.html with minify"
              exit 1
          fi

          echo "weight without minify index.html $(wc -c < index.html) bytes"
          echo "weight with minify ./dist/index.html $(wc -c < ./dist/index.html) bytes"

      - name: save output .dist/index.html
        uses: actions/upload-artifact@v4
        with:
          name: dist
          path: dist/
          retention-days: 10

      - name: deploy to vercel
        uses: amondnet/vercel-action@v42
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-args: --prod
          vercel-org-id: ${{ secrets.VERCEL_USER_ID}}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID}}
          working-directory: ./dist
```



---
<h3 align="center">SOCIAL OPLESK</h3>

