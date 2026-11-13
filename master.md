# Tokens y Automatización: Una Brújula para los Negocios
**Conferencia Magistral | Ingeniería en Gestión Empresarial (TecNM)**

---

## 1. Prompt Master para el Agente de Inteligencia Artificial (Desarrollo Frontend)

> **PROMPT MASTER:**
> "Actúa como un Diseñador Web Senior y Desarrollador Frontend experto en experiencias web interactivas estilo *scrollytelling*. Construye un archivo HTML monolítico (Single-File con CSS y JavaScript incrustados) para la conferencia *'Tokens y Automatización: Una Brújula para los Negocios'*, adaptada al perfil del Ingeniero en Gestión Empresarial del TecNM.
> 
> **Requisitos Principales:**
> 1. **Estética TEDx:** Fondo oscuro profundo (`#0F0F0F`), texto en blanco cálido (`#F5F5F5`), acentos en rojo carmesí (`#EB0028`), y tipografía fluida adaptada a proyecciones grandes.
> 2. **Scroll-Snap Vertical:** Presentación deslizable por secciones de `100vh` con un indicador visual lateral de progreso.
> 3. **Modo Exposición / Modo Lectura:** Botón flotante para alternar entre tipografía normal y tipografía extra grande para proyección en auditorios.
> 4. **Contenido Completo:** Integre secciones detalladas sobre el perfil del IGE en México, adopción de automatización (CFDI, PyMEs, ERPs), IA agéntica, economía de tokens corporativos y el marco legal de los RWA (Valores Negociables Tokenizados) en México."

---

## 2. Guía de Diseño UI/UX e Identidad Visual

### Paleta de Colores Corporativa
* **Fondo Principal:** `#0F0F0F` (Negro carbón mate).
* **Superficies y Tarjetas:** `#1A1A1A` con bordes sutiles en `#2A2A2A`.
* **Texto Primario:** `#F5F5F5` (Blanco cálido de alta reflectancia).
* **Texto Secundario:** `#A0A0A0` (Gris neutro para subtítulos y notas).
* **Color de Acento TEDx:** `#EB0028` (Rojo intenso para puntos de inflexión y marcas de sección).

### Escalado Tipográfico Fluido (`clamp()`)
```css
:root {
  --font-title: clamp(2.2rem, 5vw, 4.2rem);
  --font-subtitle: clamp(1.1rem, 2.2vw, 1.8rem);
  --font-body: clamp(1rem, 1.6vw, 1.35rem);
}
body.presenter-mode {
  --font-title: clamp(3rem, 7vw, 5.5rem);
  --font-subtitle: clamp(1.5rem, 3vw, 2.5rem);
  --font-body: clamp(1.3rem, 2.2vw, 1.9rem);
}
```

---

## 3. Estructura Narrativa y Contenido Integral de la Ponencia

### Sección 0: Portada e Introducción (Hero Slide)
* **Encabezado:** *Tokens y Automatización*
* **Subtítulo:** *Una Brújula para los Negocios en la Era Digital*
* **Etiqueta:** `CONFERENCIA MAGISTRAL | INGENIERÍA EN GESTIÓN EMPRESARIAL (TecNM)`
* **Caja de Énfasis Inicial:**
  > "Un Ingeniero en Gestión Empresarial del TecNM no es un administrador tradicional; es un estratega con visión sistémica capacitado para crear, dirigir, innovar y transformar organizaciones en un entorno global altamente competitivo."
* **Evolución del Rol:**
  > *"De bombero operativo a estratega e innovador."*

---

### Sección 1: El Contexto en México — Adopción de la Automatización y Realidad PyME
* **Título:** *1. El Panorama Operativo en México: Entre el Corporativo y la PyME*
* **Contenido Narrativo:**
  - El ecosistema empresarial mexicano vive una transición mixta y polarizada.
  - **Grandes Corporativos:** Más del 43% de las empresas de más de 100 trabajadores en manufactura avanzada, automotriz y servicios financieros ya implementan automatización de procesos.
  - **El Catalizador Fiscal:** México cuenta con una ventaja estructural única: la obligatoriedad de la **facturación electrónica (CFDI) ante el SAT**, lo que forzó la digitalización contable.
  - **El Reto PyME:** Más del 75% reconoce la urgencia de automatizar, pero gran parte se halla en fase exploratoria, superando la era de la simple "máquina de escribir digital".
* **Software Clave que Domina el Mercado:**
  - *ERPs Corporativos y PyME:* SAP Business One, Odoo, Microsoft Dynamics 365.
  - *Automatización No-Code / Low-Code:* Zapier, Make y Microsoft Power Automate.

---

### Sección 2: La Evolución de la Automatización — Hacia la IA Agéntica
* **Título:** *2. De la Tarea Manual a la Toma de Decisiones con IA*
* **Contenido Narrativo:**
  - La automatización no elimina profesiones completas; automatiza tareas repetitivas y basadas en reglas fijas.
  - **Empresas Frontera (*Frontier Firms*):** La evolución desde macros simples hasta agentes inteligentes capaces de procesar documentos no estructurados (facturas con diseños diversos, contratos), interactuar en lenguaje natural con bases de datos corporativas y tomar decisiones basadas en contexto.
* **Áreas de Oportunidad Estratégica:**
  1. Optimización del tiempo cognitivo humano.
  2. Hiper-personalización de servicios y operaciones comerciales.
  3. Interconectividad total de sistemas heredados (*Legacy*).

---

### Sección 3: La Economía de los Tokens — El Nuevo Costo Operativo y Financiero
* **Título:** *3. Los Tokens: La Nueva Unidad de Consumo y Capital*
* **Contenido Narrativo:**
  - Para el IGE, los tokens representan la nueva unidad monetaria y operativa que cruza la tecnología y los negocios.
  - **Tokens de Inteligencia Artificial (Insumo Operativo):** Así como las fábricas miden kilovatios-hora, las empresas modernas consumen *tokens de IA* (unidades de procesamiento de lenguaje). El gestor debe calcular el ROI evaluando: *¿Cuánto cuesta en tokens automatizar un proceso versus el salario-hora invertido por un empleado humano?*
  - **Tokens de Activos del Mundo Real o RWA (*Real World Assets*):** Representación digital fraccionada de activos físicos intensivos (inventarios, maquinaria, inmuebles, propiedad intelectual) mediante contratos inteligentes (*smart contracts*).

---

### Sección 4: El Ecosistema RWA en México y el Marco Regulatorio
* **Título:** *4. Ingeniería Financiera Avanzada: RWA y la Ley en México*
* **Contenido Narrativo:**
  - **El Vehículo Jurídico (*Off-Chain Wrapper*):** El token no vale por sí mismo, sino por su respaldo legal en México mediante vehículos fiduciarios o sociedades mercantiles.
  - **Marco Regulatorio e Institucional:** 
    - Operan bajo leyes existentes como la *Ley del Mercado de Valores (LMV)*, la *Ley Fintech* y las normativas antilavado (LFPIORPI).
    - No son criptomonedas especulativas libres, sino **Valores Negociables Tokenizados (VNTs)** respaldados por contratos civiles tradicionales.
  - **La Ley de Economía Digital:** Facilita la contratación electrónica, el reconocimiento de documentos digitales y la identidad digital (CURP Digital / Expediente Digital Ciudadano), permitiendo incorporación remota y segura de inversionistas.

---

### Sección 5: Conclusión — El IGE como Brújula Estratégica
* **Título:** *5. Tu Papel como Gestor: Liderando la Transformación*
* **Contenido Narrativo:**
  - La tecnología agéntica y la tokenización no son exclusivas de TI; exigen un liderazgo directivo capaz de rediseñar modelos de negocio y optimizar la cadena de valor.
* **Mensaje de Cierre:**
  > *"Los tokens y la automatización son la brújula definitiva para eliminar la burocracia y permitir que los ingenieros en gestión empresarial lideren la innovación con visión humana y rigor financiero."*

---

## 4. Código HTML/JS Listo para Producción (Monolítico)

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tokens y Automatización: Una Brújula para los Negocios</title>
  <style>
    :root {
      --bg-color: #0F0F0F;
      --card-bg: #1A1A1A;
      --text-main: #F5F5F5;
      --text-muted: #A0A0A0;
      --accent-ted: #EB0028;
      --font-title: clamp(2.2rem, 5vw, 4.2rem);
      --font-subtitle: clamp(1.1rem, 2.2vw, 1.8rem);
      --font-body: clamp(1rem, 1.6vw, 1.35rem);
    }
    body.presenter-mode {
      --font-title: clamp(3rem, 7vw, 5.5rem);
      --font-subtitle: clamp(1.5rem, 3vw, 2.5rem);
      --font-body: clamp(1.3rem, 2.2vw, 1.9rem);
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      background-color: var(--bg-color);
      color: var(--text-main);
      font-family: system-ui, -apple-system, sans-serif;
      overflow: hidden;
    }
    header {
      position: fixed;
      top: 0; left: 0; width: 100%;
      padding: 1.2rem 2.5rem;
      display: flex; justify-content: space-between; align-items: center;
      z-index: 100;
      background: rgba(15, 15, 15, 0.85);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid rgba(255, 255, 255, 0.05);
    }
    .brand { font-weight: 900; font-size: 1.1rem; letter-spacing: 1px; }
    .brand span { color: var(--accent-ted); }
    .slide-counter { font-weight: 700; color: var(--text-muted); font-size: 0.95rem; }
    .presentation-container {
      height: 100vh;
      overflow-y: scroll;
      scroll-snap-type: y mandatory;
      scroll-behavior: smooth;
    }
    .slide {
      height: 100vh; width: 100vw;
      scroll-snap-align: start; scroll-snap-stop: always;
      display: flex; flex-direction: column; justify-content: center; align-items: center;
      padding: 4rem 8%; text-align: center; position: relative;
    }
    .slide-content {
      max-width: 1050px;
      opacity: 0; transform: translateY(30px);
      transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .slide.active .slide-content { opacity: 1; transform: translateY(0); }
    h1, h2 { font-weight: 900; line-height: 1.1; margin-bottom: 1.2rem; font-size: var(--font-title); letter-spacing: -1px; }
    p { font-size: var(--font-body); color: var(--text-muted); line-height: 1.6; margin-bottom: 1.5rem; }
    .callout {
      background: var(--card-bg);
      border-left: 4px solid var(--accent-ted);
      padding: 1.5rem 2rem; border-radius: 0 12px 12px 0;
      text-align: left; margin: 1.5rem 0; font-size: var(--font-subtitle); color: var(--text-main);
    }
    .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; text-align: left; margin-top: 1.5rem; }
    .card { background: var(--card-bg); padding: 1.8rem; border-radius: 12px; border: 1px solid rgba(255,255,255,0.05); }
    .controls { position: fixed; bottom: 2rem; right: 2.5rem; display: flex; gap: 0.8rem; z-index: 100; }
    .btn-ctrl {
      background: var(--card-bg); color: var(--text-main);
      border: 1px solid rgba(255, 255, 255, 0.15);
      padding: 0.7rem 1.2rem; border-radius: 30px; cursor: pointer;
      font-weight: 700; font-size: 0.85rem; transition: all 0.2s ease;
    }
    .btn-ctrl:hover { background: var(--accent-ted); border-color: var(--accent-ted); }
    @media (max-width: 768px) { .grid-2 { grid-template-columns: 1fr; } }
  </style>
</head>
<body>

  <header>
    <div class="brand">TEC<span>NM</span> | Gestión Empresarial</div>
    <div class="slide-counter" id="counter">01 / 06</div>
  </header>

  <div class="presentation-container" id="container">
    
    <!-- Slide 0: Hero -->
    <section class="slide">
      <div class="slide-content">
        <p style="color: var(--accent-ted); font-weight: 700; letter-spacing: 2px;">CONFERENCIA MAGISTRAL</p>
        <h1>Tokens y Automatización</h1>
        <p style="font-size: var(--font-subtitle);">Una Brújula para los Negocios en la Era Digital</p>
        <div class="callout">
          "El Ingeniero en Gestión Empresarial evoluciona de bombero operativo a estratega e innovador mediante la tecnología y los datos."
        </div>
      </div>
    </section>

    <!-- Slide 1: México y Adopción -->
    <section class="slide">
      <div class="slide-content">
        <h2>1. Adopción Tecnológica en México</h2>
        <p>Un ecosistema mixto impulsado por el marco regulatorio del SAT y la madurez digital:</p>
        <div class="grid-2">
          <div class="card">
            <h3 style="color: var(--accent-ted); margin-bottom: 0.8rem;">Corporativos y Grandes Empresas</h3>
            <p style="font-size: 0.95rem;">Más del 43% de empresas con más de 100 trabajadores adoptan automatización avanzada en manufactura y finanzas.</p>
          </div>
          <div class="card">
            <h3 style="color: var(--accent-ted); margin-bottom: 0.8rem;">El Catalizador PyME</h3>
            <p style="font-size: 0.95rem;">La obligatoriedad del CFDI automatizó de forma natural la contabilidad básica; el reto actual es integrar flujos no-code.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Slide 2: IA Agéntica -->
    <section class="slide">
      <div class="slide-content">
        <h2>2. Hacia la IA Agéntica</h2>
        <p>De los bots de reglas fijas a los sistemas autónomos con razonamiento contextual:</p>
        <div class="callout">
          <strong>Impacto Operativo:</strong> Los agentes de IA procesan documentos no estructurados (facturas complejas, contratos) y toman decisiones en tiempo real optimizando el tiempo cognitivo humano.
        </div>
      </div>
    </section>

    <!-- Slide 3: Tokens IA y RWA -->
    <section class="slide">
      <div class="slide-content">
        <h2>3. La Dualidad del Token Empresarial</h2>
        <div class="grid-2">
          <div class="card">
            <h3 style="color: var(--accent-ted); margin-bottom: 0.8rem;">Tokens de Inteligencia Artificial</h3>
            <p style="font-size: 0.95rem;">La nueva unidad de costo variable y consumo operativo. Cada agente y consulta se presupuesta como un insumo estratégico.</p>
          </div>
          <div class="card">
            <h3 style="color: var(--accent-ted); margin-bottom: 0.8rem;">Tokens RWA (Activos Reales)</h3>
            <p style="font-size: 0.95rem;">Fraccionamiento digital de inventarios, inmuebles y maquinaria para abrir nuevas fuentes de fondeo corporativo.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Slide 4: Marco en México -->
    <section class="slide">
      <div class="slide-content">
        <h2>4. Regulación y RWA en México</h2>
        <p>Seguridad jurídica bajo el marco normativo nacional actual:</p>
        <div class="callout">
          Los RWA en México operan como <strong>Valores Negociables Tokenizados (VNTs)</strong> respaldados por fideicomisos y contratos mercantiles tradicionales, apalancados en la Ley de Economía Digital.
        </div>
      </div>
    </section>

    <!-- Slide 5: Conclusión -->
    <section class="slide">
      <div class="slide-content">
        <h2>5. La Brújula del Gestor Moderno</h2>
        <p style="font-size: var(--font-subtitle);">Liderar la transición tecnológica sin perder el sentido humano y estratégico de la organización.</p>
        <div class="callout" style="text-align: center;">
          "Eliminar la burocracia para que los líderes empresariales se dediquen a crear valor real."
        </div>
      </div>
    </section>

  </div>

  <div class="controls">
    <button class="btn-ctrl" id="modeToggle">Modo Exposición</button>
    <button class="btn-ctrl" id="fullscreenToggle">Pantalla Completa</button>
  </div>

  <script>
    const container = document.getElementById('container');
    const slides = document.querySelectorAll('.slide');
    const counter = document.getElementById('counter');
    const modeToggle = document.getElementById('modeToggle');
    const fullscreenToggle = document.getElementById('fullscreenToggle');

    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('active');
          const index = Array.from(slides).indexOf(entry.target) + 1;
          counter.textContent = `0${index} / 0${slides.length}`;
        }
      });
    }, { root: container, threshold: 0.6 });

    slides.forEach(slide => observer.observe(slide));

    modeToggle.addEventListener('click', () => {
      document.body.classList.toggle('presenter-mode');
      modeToggle.textContent = document.body.classList.contains('presenter-mode') ? 'Modo Lectura' : 'Modo Exposición';
    });

    fullscreenToggle.addEventListener('click', () => {
      if (!document.fullscreenElement) { document.documentElement.requestFullscreen(); } 
      else { document.exitFullscreen(); }
    });

    document.addEventListener('keydown', (e) => {
      if (e.key === 'ArrowDown' || e.key === ' ') { container.scrollBy({ top: window.innerHeight, behavior: 'smooth' }); } 
      else if (e.key === 'ArrowUp') { container.scrollBy({ top: -window.innerHeight, behavior: 'smooth' }); }
    });
  </script>
</body>
</html>