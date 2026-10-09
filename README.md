<!-- ═══════════════════════════ HERO ═══════════════════════════ -->
<a href="https://github.com/Alessandro-BS">
  <img src="./assets/hero.svg" width="100%" alt="Aless Bustamante — Full Stack Developer"/>
</a>

<p align="center">
  <a href="https://github.com/Alessandro-BS">
    <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=2800&pause=900&color=8B7CF6&center=true&vCenter=true&width=720&lines=LMS+multi-instituto+en+producci%C3%B3n+(PHP+8.3);App+Android+nativa+con+Kotlin+%2B+Compose;Agentes+de+IA+por+WhatsApp+con+MCP;Clean+Architecture%2C+TDD+y+Git+Flow" alt="Typing SVG"/>
  </a>
</p>

<p align="center">
  <a href="#-proyectos-destacados"><img src="https://img.shields.io/badge/Proyectos-404db0?style=for-the-badge&logo=rocket&logoColor=white" alt="Proyectos"/></a>
  <a href="#-stack-tecnológico"><img src="https://img.shields.io/badge/Stack-6a5acd?style=for-the-badge&logo=stackshare&logoColor=white" alt="Stack"/></a>
  <a href="#-actividad-en-github"><img src="https://img.shields.io/badge/Actividad-ffcd42?style=for-the-badge&logo=github&logoColor=black" alt="Actividad"/></a>
  <br/>
  <img src="https://komarev.com/ghpvc/?username=Alessandro-BS&label=Visitas&color=404db0&style=flat-square" alt="profile views"/>
  <img src="https://img.shields.io/github/followers/Alessandro-BS?label=Seguidores&style=flat-square&color=6a5acd" alt="followers"/>
  <img src="https://img.shields.io/badge/Lima-Per%C3%BA-ffcd42?style=flat-square&logo=googlemaps&logoColor=black" alt="Lima, Perú"/>
</p>

<br/>

## 👋 Sobre mí

<img align="right" width="260" src="https://github.com/Aurorp1g/Aurorp1g/raw/main/cartoon.webp" alt="gato programando"/>

Estudiante de **Ingeniería de Software (7.º ciclo)** y desarrollador **Full Stack**. Me gusta construir software que la gente usa de verdad: hoy mantengo el **aula virtual de un consorcio de cuatro institutos** que está en producción, desarrollo una **app Android nativa** para coordinar horarios en grupo y diseño **agentes de IA** que atienden por WhatsApp.

Trabajo con **Clean Architecture**, pruebas automatizadas y Git Flow con staging, porque prefiero que los cambios lleguen a producción sin sorpresas. Ahora mismo estoy profundizando en **ciberseguridad**, **cloud** y **agentes de IA**.

```yaml
rol:          Full Stack Developer
enfoque:      [Clean Architecture, APIs REST, Automatización con IA]
en_producción: [Educa LMS — 3 institutos en vivo, el 4.º en camino]
aprendiendo:  [Ciberseguridad, Cloud, Agentes de IA]
lema:         "Código seguro, eficiente y mantenible."
```

<br clear="right"/>

---

## 🚀 Proyectos destacados

### 🎓 Educa LMS &nbsp;<sub><img src="https://img.shields.io/badge/repositorio-privado-555?style=flat-square&logo=github" alt="privado"/> <img src="https://img.shields.io/badge/estado-en%20producci%C3%B3n-3ddc97?style=flat-square" alt="en producción"/></sub>

<img src="./assets/educa-lms.svg" width="100%" alt="Educa LMS — una base de código, cuatro institutos"/>

Aula virtual propia de un consorcio educativo peruano (**EDUCA · IPSE · ICEPP · CESUP**). Cada instituto tiene su servidor, su base de datos y su marca, pero el código **se escribe una sola vez**: una herramienta generadora toma una versión etiquetada de `main` y produce la variante de cada marca (nombre, colores, logo, series de facturación). Cubre todo el ciclo del alumno: venta, matrícula, cobranza con comprobantes electrónicos, clases, exámenes y certificados.

<p>
  <img src="https://img.shields.io/badge/PHP_8.3-777BB4?style=for-the-badge&logo=php&logoColor=white"/>
  <img src="https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white"/>
  <img src="https://img.shields.io/badge/OpenLiteSpeed-0E76A8?style=for-the-badge&logo=litespeed&logoColor=white"/>
  <img src="https://img.shields.io/badge/PHPUnit_12-3C9CD7?style=for-the-badge&logo=php&logoColor=white"/>
  <img src="https://img.shields.io/badge/Playwright-2EAD33?style=for-the-badge&logo=playwright&logoColor=white"/>
  <img src="https://img.shields.io/badge/PWA-5A0FC8?style=for-the-badge&logo=pwa&logoColor=white"/>
</p>

<details>
<summary><b>🏗️ Arquitectura — ver cómo está construido</b></summary>
<br/>

```mermaid
flowchart LR
    R["👥 6 roles<br/>Administrador · Estudiante · Docente<br/>Cobranza · Certificación · Venta"]:::r
    R -->|sesión + rol + CSRF| P[Página PHP]
    P --> S["src/ · Servicios por módulo<br/>con TDD"]
    S --> DB[(MariaDB<br/>migraciones versionadas)]
    API["API · 35 endpoints<br/>auth por token"] --> S
    CRON["19 cron jobs<br/>cola · respaldos · conciliación"] --> DB
    S --> EXT["🧾 Facturación electrónica<br/>💬 WhatsApp · 🔔 Push"]
    classDef r fill:#404db0,color:#fff,stroke:#6a5acd
```

- **Dos capas que conviven:** las páginas por rol validan sesión, rol y CSRF; la lógica de negocio nueva vive en `src/` por módulos (Académico, Cobros, Certificados, Ventas, Soporte) con **TDD**.
- **Esquema solo por migraciones** fechadas — nunca un `CREATE TABLE` escondido en una página.
- **Cola de envíos concurrente segura** entre marcas del mismo servidor (`SELECT … FOR UPDATE SKIP LOCKED` + candado por sitio).
- **Seguridad:** secretos solo en `.env` por servidor, nada de credenciales en el repositorio, y el staging tiene la facturación neutralizada para no emitir comprobantes reales.

</details>

<details>
<summary><b>🌿 Flujo de trabajo — Git Flow con staging y pases ensayados</b></summary>
<br/>

```mermaid
gitGraph
    commit id: "base" tag: "v2026.09.2"
    branch develop
    checkout develop
    commit id: "integración"
    branch feature
    checkout feature
    commit id: "flujo-certificados"
    commit id: "pruebas"
    checkout develop
    merge feature id: "PR revisado"
    branch release
    checkout release
    commit id: "QA en staging"
    checkout main
    merge release id: "pase" tag: "v2026.09.12"
    checkout develop
    merge main id: "sync"
```

| Rama | Para qué | Entorno |
|---|---|---|
| `feature/*` | Un cambio; vuelve por Pull Request | Local / staging |
| `develop` | Integración de lo terminado | **Staging** |
| `release/*` | Congelado para QA final | Staging |
| `main` | Lo que corre en producción, con etiqueta `vAAAA.MM.N` | **Producción** |
| `hotfix/*` | Error urgente: sale de `main`, vuelve a `main` y `develop` | — |

Cada pase a producción es un **script ensayado sobre una copia desechable**, ejecutado a mano y con su vuelta atrás preparada.

</details>

<br/>

### 📱 HueckoApp &nbsp;<sub><a href="https://github.com/Alessandro-BS/HueckoApp-Android"><img src="https://img.shields.io/badge/ver_repositorio-6750A4?style=flat-square&logo=github&logoColor=white" alt="Repositorio"/></a> <img src="https://img.shields.io/badge/versi%C3%B3n-1.0.0-d0bcff?style=flat-square" alt="v1.0.0"/></sub>

<a href="https://github.com/Alessandro-BS/HueckoApp-Android">
  <img src="./assets/huecko.svg" width="100%" alt="HueckoApp — coordinación de horarios grupales"/>
</a>

Coordinar un plan por chat es un caos. **HueckoApp** cruza los horarios de todo el grupo, pinta un **mapa de calor** con la disponibilidad y deja que el grupo **vote** propuestas hasta llegar al quórum. El horario se puede cargar a mano o **desde una foto** usando Gemini, con un modo offline de respaldo si no hay red.

<p>
  <img src="https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white"/>
  <img src="https://img.shields.io/badge/Jetpack_Compose-4285F4?style=for-the-badge&logo=jetpackcompose&logoColor=white"/>
  <img src="https://img.shields.io/badge/Material_3-6750A4?style=for-the-badge&logo=materialdesign&logoColor=white"/>
  <img src="https://img.shields.io/badge/Gemini_%C2%B7_Firebase_AI-FFCA28?style=for-the-badge&logo=firebase&logoColor=black"/>
  <img src="https://img.shields.io/badge/MVVM-3DDC84?style=for-the-badge&logo=android&logoColor=white"/>
</p>

<details>
<summary><b>🧩 Arquitectura MVVM por capas</b></summary>
<br/>

```mermaid
flowchart LR
    UI["🖼️ UI · Compose<br/>Dashboard · Grupos · Horario · OCR · Votación"]
    VM["🧠 ViewModels<br/>StateFlow"]
    UC["⚙️ Dominio<br/>AvailabilityMatcher · modelos"]
    REPO["📦 Repositorios<br/>interfaces en domain, impl en data"]
    AI["✨ GeminiService<br/>OCR + fallback offline"]
    UI --> VM --> UC
    VM --> REPO
    REPO --> AI
    classDef k fill:#6750A4,color:#fff,stroke:#d0bcff
    class UI,VM,UC,REPO,AI k
```

</details>

<details>
<summary><b>🔍 El algoritmo del “hueco” — por qué no uso el promedio</b></summary>
<br/>

El cruce de agendas es una **función pura** (sin repositorios ni corrutinas), así se prueba con una lista de bloques y nada más. Junta las horas consecutivas en las que el grupo supera su umbral y **describe cada franja por su hora menos disponible**: decir “de 10 a 13 está libre el 80 %” cuando a las 12 solo lo está el 40 % sería prometer un hueco que se rompe a la mitad.

```kotlin
val anterior = ventanas.lastOrNull()
if (anterior != null && anterior.endHour == hour) {
    // Prolonga la franja y se queda con el PEOR dato de sus horas
    ventanas[ventanas.lastIndex] = anterior.copy(
        endHour = hour + 1,
        availabilityPercentage = minOf(anterior.availabilityPercentage, porcentaje),
        freeMembers = minOf(anterior.freeMembers, libres),
    )
}
```

</details>

<br/>

### 🤖 Camila — Agente de WhatsApp con IA &nbsp;<sub><img src="https://img.shields.io/badge/estado-en%20desarrollo-ffcd42?style=flat-square" alt="en desarrollo"/></sub>

Agente conversacional para un instituto que informa la oferta de cursos y gestiona matrículas por WhatsApp. Diseñé el flujo de mensajes, las secuencias de remarketing y las reglas comerciales; los cursos y precios se consultan **en tiempo real** desde Google Sheets mediante una herramienta **MCP** (`consultar_curso`) expuesta con Apps Script.

<p>
  <img src="https://img.shields.io/badge/BotcakeAI-6C5CE7?style=for-the-badge&logoColor=white"/>
  <img src="https://img.shields.io/badge/WhatsApp_API-25D366?style=for-the-badge&logo=whatsapp&logoColor=white"/>
  <img src="https://img.shields.io/badge/MCP-000000?style=for-the-badge&logo=anthropic&logoColor=white"/>
  <img src="https://img.shields.io/badge/Google_Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white"/>
  <img src="https://img.shields.io/badge/Apps_Script-4285F4?style=for-the-badge&logo=google&logoColor=white"/>
</p>

<details>
<summary><b>💬 Ver el flujo de una conversación</b></summary>
<br/>

```mermaid
flowchart LR
    A["💬 Cliente<br/>WhatsApp"] --> B["🤖 Camila<br/>Agente IA"]
    B --> C["🔌 MCP<br/>consultar_curso"]
    C --> D["📊 Google Sheets<br/>cursos y precios"]
    D --> B
    B --> E["📈 Secuencia de<br/>remarketing"]
    B --> F["📝 Matrícula<br/>registrada"]
```

</details>

---

## 🧰 Stack tecnológico

<table>
  <tr>
    <td align="center" width="140"><b>Lenguajes</b></td>
    <td><img src="https://skillicons.dev/icons?i=php,java,kotlin,ts,js,py,html,css&perline=8" alt="lenguajes"/></td>
  </tr>
  <tr>
    <td align="center"><b>Backend</b></td>
    <td><img src="https://skillicons.dev/icons?i=spring,nodejs,express,django,fastapi&perline=8" alt="backend"/></td>
  </tr>
  <tr>
    <td align="center"><b>Frontend y móvil</b></td>
    <td><img src="https://skillicons.dev/icons?i=angular,react,tailwind,bootstrap,vite,androidstudio&perline=8" alt="frontend"/></td>
  </tr>
  <tr>
    <td align="center"><b>Datos</b></td>
    <td><img src="https://skillicons.dev/icons?i=mysql,postgres,mongodb,supabase,firebase&perline=8" alt="datos"/></td>
  </tr>
  <tr>
    <td align="center"><b>DevOps y cloud</b></td>
    <td><img src="https://skillicons.dev/icons?i=git,github,githubactions,docker,linux,aws,azure,gcp&perline=8" alt="devops"/></td>
  </tr>
  <tr>
    <td align="center"><b>Herramientas</b></td>
    <td><img src="https://skillicons.dev/icons?i=postman,figma,maven,vscode,idea&perline=8" alt="herramientas"/></td>
  </tr>
</table>

<details>
<summary><b>📚 Ver el stack completo</b></summary>
<br/>

**Lenguajes** &nbsp;
![PHP](https://img.shields.io/badge/php-%23777BB4.svg?style=flat-square&logo=php&logoColor=white) ![Java](https://img.shields.io/badge/java-%23ED8B00.svg?style=flat-square&logo=openjdk&logoColor=white) ![Kotlin](https://img.shields.io/badge/kotlin-%237F52FF.svg?style=flat-square&logo=kotlin&logoColor=white) ![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=flat-square&logo=typescript&logoColor=white) ![JavaScript](https://img.shields.io/badge/javascript-%23323330.svg?style=flat-square&logo=javascript&logoColor=%23F7DF1E) ![Python](https://img.shields.io/badge/python-3670A0?style=flat-square&logo=python&logoColor=ffdd54) ![Scala](https://img.shields.io/badge/scala-%23DC322F.svg?style=flat-square&logo=scala&logoColor=white) ![HTML5](https://img.shields.io/badge/html5-%23E34F26.svg?style=flat-square&logo=html5&logoColor=white) ![CSS3](https://img.shields.io/badge/css3-%231572B6.svg?style=flat-square&logo=css3&logoColor=white) ![PowerShell](https://img.shields.io/badge/PowerShell-%235391FE.svg?style=flat-square&logo=powershell&logoColor=white) ![Markdown](https://img.shields.io/badge/markdown-%23000000.svg?style=flat-square&logo=markdown&logoColor=white)

**Frameworks y librerías** &nbsp;
![Spring](https://img.shields.io/badge/spring-%236DB33F.svg?style=flat-square&logo=spring&logoColor=white) ![Thymeleaf](https://img.shields.io/badge/Thymeleaf-%23005C0F.svg?style=flat-square&logo=Thymeleaf&logoColor=white) ![Angular](https://img.shields.io/badge/angular-%23DD0031.svg?style=flat-square&logo=angular&logoColor=white) ![RxJS](https://img.shields.io/badge/rxjs-%23B7178C.svg?style=flat-square&logo=reactivex&logoColor=white) ![React](https://img.shields.io/badge/react-%2320232a.svg?style=flat-square&logo=react&logoColor=%2361DAFB) ![React Native](https://img.shields.io/badge/react_native-%2320232a.svg?style=flat-square&logo=react&logoColor=%2361DAFB) ![Next JS](https://img.shields.io/badge/Next-black?style=flat-square&logo=next.js&logoColor=white) ![Vue.js](https://img.shields.io/badge/vue.js-%2335495e.svg?style=flat-square&logo=vuedotjs&logoColor=%234FC08D) ![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=flat-square&logo=node.js&logoColor=white) ![Express.js](https://img.shields.io/badge/express.js-%23404d59.svg?style=flat-square&logo=express&logoColor=%2361DAFB) ![Django](https://img.shields.io/badge/django-%23092E20.svg?style=flat-square&logo=django&logoColor=white) ![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=flat-square&logo=django&logoColor=white&color=ff1709&labelColor=gray) ![Ionic](https://img.shields.io/badge/Ionic-%233880FF.svg?style=flat-square&logo=Ionic&logoColor=white) ![Jetpack Compose](https://img.shields.io/badge/Jetpack_Compose-4285F4?style=flat-square&logo=jetpackcompose&logoColor=white) ![TailwindCSS](https://img.shields.io/badge/tailwindcss-%2338B2AC.svg?style=flat-square&logo=tailwind-css&logoColor=white) ![Bootstrap](https://img.shields.io/badge/bootstrap-%238511FA.svg?style=flat-square&logo=bootstrap&logoColor=white) ![Vite](https://img.shields.io/badge/vite-%23646CFF.svg?style=flat-square&logo=vite&logoColor=white) ![Chart.js](https://img.shields.io/badge/chart.js-F5788D.svg?style=flat-square&logo=chart.js&logoColor=white) ![JWT](https://img.shields.io/badge/JWT-black?style=flat-square&logo=JSON%20web%20tokens)

**Bases de datos** &nbsp;
![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=flat-square&logo=mariadb&logoColor=white) ![MySQL](https://img.shields.io/badge/mysql-4479A1.svg?style=flat-square&logo=mysql&logoColor=white) ![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=flat-square&logo=postgresql&logoColor=white) ![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=flat-square&logo=microsoft%20sql%20server&logoColor=white) ![Oracle](https://img.shields.io/badge/Oracle-F80000?style=flat-square&logo=oracle&logoColor=white) ![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=flat-square&logo=mongodb&logoColor=white)

**DevOps, cloud y servidores** &nbsp;
![Git](https://img.shields.io/badge/git-%23F05033.svg?style=flat-square&logo=git&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=flat-square&logo=githubactions&logoColor=white) ![GitLab CI](https://img.shields.io/badge/gitlab%20CI-%23181717.svg?style=flat-square&logo=gitlab&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=flat-square&logo=docker&logoColor=white) ![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=flat-square&logo=amazon-aws&logoColor=white) ![Azure](https://img.shields.io/badge/azure-%230072C6.svg?style=flat-square&logo=microsoftazure&logoColor=white) ![Google Cloud](https://img.shields.io/badge/GoogleCloud-%234285F4.svg?style=flat-square&logo=google-cloud&logoColor=white) ![Cloudflare](https://img.shields.io/badge/Cloudflare-F38020?style=flat-square&logo=Cloudflare&logoColor=white) ![Netlify](https://img.shields.io/badge/netlify-%23000000.svg?style=flat-square&logo=netlify&logoColor=%2300C7B7) ![Vercel](https://img.shields.io/badge/vercel-%23000000.svg?style=flat-square&logo=vercel&logoColor=white) ![OpenLiteSpeed](https://img.shields.io/badge/OpenLiteSpeed-0E76A8?style=flat-square&logo=litespeed&logoColor=white) ![Apache Tomcat](https://img.shields.io/badge/apache%20tomcat-%23F8DC75.svg?style=flat-square&logo=apache-tomcat&logoColor=black) ![Gunicorn](https://img.shields.io/badge/gunicorn-%23298729.svg?style=flat-square&logo=gunicorn&logoColor=white) ![NPM](https://img.shields.io/badge/NPM-%23CB3837.svg?style=flat-square&logo=npm&logoColor=white) ![Maven](https://img.shields.io/badge/Maven-C71A36?style=flat-square&logo=apachemaven&logoColor=white)

**Calidad, datos y gestión** &nbsp;
![PHPUnit](https://img.shields.io/badge/PHPUnit-3C9CD7?style=flat-square&logo=php&logoColor=white) ![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white) ![JUnit](https://img.shields.io/badge/JUnit-25A162?style=flat-square&logo=junit5&logoColor=white) ![Postman](https://img.shields.io/badge/Postman-FF6C37?style=flat-square&logo=postman&logoColor=white) ![Swagger](https://img.shields.io/badge/Swagger-%2385EA2D.svg?style=flat-square&logo=swagger&logoColor=black) ![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=flat-square&logo=numpy&logoColor=white) ![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat-square&logo=pandas&logoColor=white) ![Power Bi](https://img.shields.io/badge/power_bi-F2C811?style=flat-square&logo=powerbi&logoColor=black) ![Jira](https://img.shields.io/badge/jira-%230A0FFF.svg?style=flat-square&logo=jira&logoColor=white) ![Figma](https://img.shields.io/badge/figma-%23F24E1E.svg?style=flat-square&logo=figma&logoColor=white) ![Canva](https://img.shields.io/badge/Canva-%2300C4CC.svg?style=flat-square&logo=Canva&logoColor=white) ![Cisco](https://img.shields.io/badge/cisco-%23049fd9.svg?style=flat-square&logo=cisco&logoColor=black)

</details>

---

## 📊 Actividad en GitHub

<p align="center">
  <img src="https://streak-stats.demolab.com/?user=Alessandro-BS&theme=tokyonight&hide_border=true&background=0d1117" height="170" alt="racha"/>
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=Alessandro-BS&theme=tokyonight" height="170" alt="repos por lenguaje"/>
</p>

<details>
<summary><b>📈 Ver más estadísticas</b></summary>
<br/>
<p align="center">
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=Alessandro-BS&theme=tokyonight" alt="resumen del perfil"/>
  <br/>
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=Alessandro-BS&theme=tokyonight" alt="lenguaje más usado"/>
  <img src="https://github-profile-summary-cards.vercel.app/api/cards/productive-time?username=Alessandro-BS&theme=tokyonight&utcOffset=-5" alt="horario productivo"/>
  <br/>
  <img src="https://github-trophies.vercel.app/?username=Alessandro-BS&theme=tokyonight&no-frame=true&no-bg=true&column=7&margin-w=10&margin-h=10" alt="trofeos"/>
</p>
</details>

<!-- La serpiente se genera con .github/workflows/snake.yml -->
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Alessandro-BS/Alessandro-BS/output/github-snake-dark.svg"/>
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/Alessandro-BS/Alessandro-BS/output/github-snake.svg"/>
  <img alt="serpiente comiéndose el gráfico de contribuciones" src="https://raw.githubusercontent.com/Alessandro-BS/Alessandro-BS/output/github-snake.svg"/>
</picture>

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:ffcd42,50:6a5acd,100:404db0&height=110&section=footer&text=Gracias%20por%20pasar%20%C2%B7%20Lima%2C%20Per%C3%BA&fontSize=20&fontColor=ffffff&fontAlignY=70" width="100%" alt="footer"/>
</p>
