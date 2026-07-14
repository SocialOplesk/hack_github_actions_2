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
- Debes tener cuenta en github y usar la terminal de wsl en caso de emplear windows, ideal sobre debian / ubuntu / fedora.
```
|Hacks | Details | 
|----------|---------|
| H-1      | deploy index.html |

<br/> 

## 🏆 H-1 

```

📁hack_gh_1/
├── .github/workflows/deploy.yml
├── index.html

```

1. Crear un directorio el archivo deploy.yml en un repositorio

2. Dentro del deploy.yml pegar el script 

3. Debes crear aplicar los ajustes necesarios en settings del repositorio y no de la cuenta
  
4. Tomar el script del html y copiarlo en index.html
   
5. Haces varios cambios acompañado de push, para verificar el deploy ordenado desde Github Actions funciona  
   
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

---
# Evita race conditions: si haces dos pushes seguidos, no se ejecutan dos deploys en paralelo pisándose. 

concurrency:
  group: "pages"
  cancel-in-progress: false

---
 # Sube al storage de Actions

- uses: actions/upload-pages-artifact@v3
        with:
          path: '.'

```

<br/>

```
- contents: read → puede leer el código del repo (checkout)
- pages:    write → puede publicar en GitHub Pages
- id-token: write → autenticación sin secretos
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
🟢 Script github/actions del hack-1 🟢

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
      - name: Clonar reporitorio / Descargar repositorio
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
├── .github/workflows/deploy.yml
├── index.html

```
1. Crear un directorio el archivo deploy.yml en un repositorio

2. Dentro del deploy.yml pegar el script 

3. Debes crear aplicar los ajustes necesarios en settings del repositorio para activar github pages
  
4. Tomar el script del html y copiarlo en index.html

5. El comando "test -f index.html" verifica que el archivo existe la flag "-f" quiere decir file <br/>
   test -f archivo devuelve código de salida 0 si el archivo existe y es un archivo regular, 1 si no. <br/>
   Si falla (||), imprime error con el prefijo ::error:: (sintaxis que GitHub Actions reconoce para resaltarlo en rojo)

  <img width="683" height="140" alt="image" src="https://github.com/user-attachments/assets/cb2abef2-ea0f-4a54-a3a6-ada84177e002" />
  

<br/>

---

<img width="613" height="150" alt="image" src="https://github.com/user-attachments/assets/6631f4de-f25b-47e5-8e8a-b06f595ec9db" />

```
- Debe mostrar 2 jobs en el dashboard de actions de github actions
- Se divide en 2 jobs para asi dividir las tareas una de CI y otra de CD 
- Esto indica que una tarea pasa a otra mediante el step del artefacto: "Subir artefacto para Pages"

- name: Subir artefacto para Pages
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'

---
# La palabra clave needs

Indica que un trabajo actual no puede empezar hasta que el trabajo del que depende haya terminado con éxito.
integration: Es simplemente el nombre de otra tarea(job) previa (por ejemplo, una fase de pruebas de integración).

-  deploy:
    needs: integration
    runs-on: ubuntu-latest
```

---
<br/>

🟢 Script github/actions del hack-2 🟢

```
name: ❓

on:
  push:
    branches: [❓]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  integration:
    runs-on: ❓
    steps:
      - name: Clonar reporitorio / Descargar repositorio
        uses: actions/❓

      - name: Validar estructura del sitio
        run: |
          test -f index.html || (echo "::error::No existe index.html en la raíz" && exit ❓)
          echo "index.html encontrado, validación básica OK"

      - name: Configurar Pages
        uses: actions/configure-pages@v5

      - name: Subir artefacto para Pages
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'

  deploy:
    needs: ❓
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy a GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```


---
<h3 align="center">SOCIAL OPLESK</h3>

