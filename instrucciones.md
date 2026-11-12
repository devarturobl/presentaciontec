# Especificaciones Técnicas y Prompt Master: Presentación Web Scrollable Estilo TEDx

Este documento constituye la guía de ingeniería y especificaciones para que un agente de inteligencia artificial desarrollador frontend cree una aplicación web de presentación interactiva mediante desplazamiento vertical (*scrollytelling*). La interfaz combina la estética limpia y moderna característica de las conferencias **TEDx** con una experiencia adaptable para la lectura y la exposición en vivo.

La presentación está diseñada para la conferencia titulada **"Tokens y Automatización: Una Brújula para los Negocios"**, orientada a estudiantes de Licenciatura en Gestión Empresarial.

---

## 1. Prompt Master para el Agente de Inteligencia Artificial

Instrucciones ejecutables para proporcionar directamente a tu agente de IA (como Cursor, Claude Code, ChatGPT o v0) para iniciar la generación de la página web:

> **PROMPT MASTER PARA EL AGENTE DE CÓDIGO:**
> 
> "Actúa como un Diseñador Web Senior y Desarrollador Frontend experto en la creación de experiencias web de presentación interactiva estilo scrollytelling. Tu objetivo es construir un archivo HTML monolítico (Single-File con CSS y JavaScript incrustados) que funcione como una presentación deslizable por scroll vertical para la conferencia *'Tokens y Automatización: Una Brújula para los Negocios'*.
> 
> **Requisitos Principales de la Interfaz:**
> 1. **Diseño Visual Estilo TEDx**: Estética extremadamente limpia, minimalista y de alto contraste. Usa un fondo oscuro profundo (`#0F0F0F`) o claro impoluto (`#FFFFFF`) con acentos rojo carmesí (`#EB0028`) e interlineado amplio.
> 2. **Experiencia de Scroll (Scrollytelling)**: Cada sección de la presentación debe ocupar exactamente el 100% de la altura de la ventana (`100vh`) utilizando `scroll-snap-type: y mandatory`. Al desplazarse hacia abajo, los elementos de texto clave se deben iluminar o resaltar progresivamente mediante `IntersectionObserver`.
> 3. **Interfaz Adaptable para Exposición (Presenter Mode)**:
>    - Letras grandes y tipografía fluida (`clamp()`) con legibilidad garantizada a 5 metros de distancia.
>    - Botón flotante para alternar entre **Modo Lectura** (tamaño estándar, notas visibles) y **Modo Exposición** (tipografía extra grande, máximo contraste, sin distracciones).
>    - Soporte completo para navegación por teclado (flechas arriba/abajo, barra espaciadora y tecla `F` para pantalla completa).
> 4. **Resaltos Visuales (Callouts)**: Incluye cajas de destacado estilizadas para datos numéricos impactantes (ej. *$16 Billones en RWA para 2030*, *30% reducción de costos con IA Agéntica*).
> 
> Implementa el código completo siguiendo la estructura narrativa y técnica detallada en este documento."

---

## 2. Guía de Diseño UI/UX e Identidad Visual

Para lograr el estándar visual inspirado en las conferencias TEDx, la aplicación web debe cumplir con los siguientes lineamientos:

### Paleta de Colores y Jerarquía
* **Fondo Principal (Modo Oscuro Predeterminado)**: `#0F0F0F` (Negro carbón mate, suave a la vista).
* **Superficies y Tarjetas**: `#1A1A1A` con bordes sutiles en `#2A2A2A`.
* **Texto Primario**: `#F5F5F5` (Blanco cálido de alta reflectancia).
* **Texto Secundario**: `#A0A0A0` (Gris neutro para subtítulos y notas).
* **Color de Acento TEDx**: `#EB0028` (Rojo intenso para puntos de inflexión, énfasis y marcas de sección).
* **Resaltado de Texto (Highlight)**: `#FFD700` (Dorado suave) o fondo `#EB0028` con texto blanco para frases clave del discurso.

### Tipografía Adaptable y Escalado
Se utiliza una fuente tipográfica de alta legibilidad sans-serif por su claridad en proyecciones digitales.

```css
:root {
  /* Escalado fluido utilizando clamp() */
  --font-title: clamp(2.5rem, 6vw, 4.8rem);
  --font-subtitle: clamp(1.2rem, 2.5vw, 2.2rem);
  --font-body: clamp(1rem, 1.8vw, 1.5rem);
  --font-highlight: clamp(1.1rem, 2vw, 1.8rem);
}

/* Modo Exposición: Incrementa la escala tipográfica para proyección */
body.presenter-mode {
  --font-title: clamp(3.2rem, 8vw, 6rem);
  --font-subtitle: clamp(1.6rem, 3.5vw, 2.8rem);
  --font-body: clamp(1.4rem, 2.5vw, 2.1rem);
  --font-highlight: clamp(1.5rem, 2.8vw, 2.4rem);
}
```

### Elementos de Interfaz y Navegación
1. **Barra de Progreso Vertical (Right Rail)**: Un indicador discreto a la derecha de la pantalla que muestra pequeños puntos (*dots*) iluminados según la sección activa.
2. **Navegador de Secciones Superior**: Encabezado fino y translúcido que muestra el título de la conferencia y el contador de diapositiva (ej. `02 / 05`).
3. **Controles Flotantes Inferiores**:
   - Botón toggle `[ Modo Exposición ]` / `[ Modo Lectura ]`.
   - Botón `[ Pantalla Completa ]`.

---

## 3. Arquitectura Técnica y Mecánica de Scroll

La arquitectura de la aplicación utiliza APIs nativas del navegador para garantizar 60 FPS de rendimiento sin depender de marcos pesados.

### Estructura de Maquetación CSS (Scroll Snap)
```css
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  overflow-x: hidden;
  background-color: #0F0F0F;
  color: #F5F5F5;
  font-family: system-ui, -apple-system, sans-serif;
  scroll-behavior: smooth;
}

.presentation-container {
  height: 100vh;
  overflow-y: scroll;
  scroll-snap-type: y mandatory;
}

.slide {
  height: 100vh;
  width: 100vw;
  scroll-snap-align: start;
  scroll-snap-stop: always;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 2rem 4rem;
  box-sizing: border-box;
  position: relative;
}
```

### Activación de Resaltos y Transiciones (`IntersectionObserver`)
El efecto de animación progresiva en los textos (*reveal & highlight*) se logra detectando la entrada de cada elemento al encuadre:

```javascript
const observerOptions = {
  root: document.querySelector('.presentation-container'),
  threshold: 0.6
};

const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('active');
      updateNavigation(entry.target.dataset.slideIndex);
    }
  });
}, observerOptions);

document.querySelectorAll('.slide').forEach((slide, index) => {
  slide.dataset.slideIndex = index;
  observer.observe(slide);
});
```

---

## 4. Estructura Narrativa y Contenido de las Secciones

A continuación se detalla el contenido exacto y los apoyos visuales respaldados en la documentación técnica para cada una de las secciones de la presentación web:

### Sección 0: Portada e Introducción (Hero Slide)
* **Encabezado**: *Tokens y Automatización*
* **Subtítulo**: *Una Brújula para los Negocios en la Era Digital*
* **Etiqueta TEDx**: `CONFERENCIA MAGISTRAL | GESTIÓN EMPRESARIAL`
* **Caja de Énfasis Inicial**:
  > "La tecnología no llega para reemplazar al administrador, sino para convertirse en su brújula estratégica."

---

### Sección 1: El Gancho — La Doble Naturaleza del Token
* **Título**: *1. Desmitificando la Palabra: El Doble Motor Tecnológico*
* **Contenido Narrativo**:
  - Explicar la confusión en el mundo corporativo sobre qué es un *Token*.
  - **El Token en Inteligencia Artificial**: Definido como la unidad básica de procesamiento de contexto e información en los modelos de lenguaje (LLMs). Funciona como el átomo que transforma datos crudos en decisiones de negocio.
  - **El Token en Finanzas y RWA**: Representación digital y fraccionada de derechos de propiedad o activos del mundo real (*Real-World Assets*) sobre redes blockchain.
* **Resalto en Pantalla (Callout Box)**:
  > **Concepto Clave**: La inteligencia moderna se procesa en **Tokens de IA**; la propiedad y el capital del futuro se transfieren en **Tokens de RWA**.
* **Dato Impactante**:
  - *Las empresas ya no consumen solo software; consumen inteligencia medida en tokens.*

---

### Sección 2: Automatización Agéntica — De la RPA a los Agentes Inteligentes
* **Título**: *2. La Evolución Operativa: De Tareas a Decisiones*
* **Contenido Narrativo**:
  - **Automatización Robótica de Procesos (RPA)**: Réplica tradicional de tareas manuales repetitivas basada en reglas e interfaces de usuario sin modificar sistemas legados.
  - **IA Agéntica**: La convergencia entre RPA y Modelos de Lenguaje (LLMs) para crear agentes autónomos capaces de interpretar contexto, adaptarse a entornos dinámicos y auto-optimizar procesos corporativos.
* **Matriz Comparativa en Pantalla**:

| Criterio | RPA Tradicional | IA Agéntica |
| :--- | :--- | :--- |
| **Mecanismo** | Reglas rígidas y clics programados | Procesamiento de lenguaje natural y LLM |
| **Adaptabilidad** | Frágil ante cambios en la interfaz | Autónoma y adaptativa al contexto |
| **Toma de Decisiones**| Requiere excepción humana | Evaluación predictiva y ejecución directa |

* **Resalto de Impacto Empresarial**:
  > La integración de IA Agéntica reduce hasta un **30% los costos operativos** y acelera en un **50% los tiempos de ciclo** en los procesos de negocio.

---

### Sección 3: Tokenización de Activos Reales (RWA) y Acceso al Capital
* **Título**: *3. Redefiniendo el Acceso al Capital Empresarial*
* **Contenido Narrativo**:
  - El problema histórico de la iliquidez de activos físicos (bienes raíces, maquinaria, proyectos de infraestructura).
  - La solución mediante **Propiedad Fraccionada**: Convertir activos de alto valor en tokens digitales accesibles, permitiendo financiar proyectos sin depender únicamente del crédito bancario tradicional.
  - Ejemplos de adopción institucional: Emisión de fondos tokenizados por BlackRock (*BUIDL*), depósitos de JPMorgan (*Kinexys*) y la iniciativa de Mastercard para reemplazar números físicos de tarjetas por tokens criptográficos (*"Tokenize Everything"*).
* **Métrica Destacada (Estilo Big Number TEDx)**:
  > **$16 BILLONES DE DÓLARES**
  > Proyección de activos del mundo real (RWA) tokenizados a nivel global para el año 2030 (equivalente al 10% del PIB mundial).

---

### Sección 4: La Convergencia — Algoritmos que Pagan y Deciden Solos
* **Título**: *4. El Fin del Efectivo: Pagos Programables y Smart Contracts*
* **Contenido Narrativo**:
  - La unión de la IA y los activos digitales da lugar a **sistemas financieros autoejecutables**.
  - **Stablecoins en Tesorería Corporativa**: Reducción de costos de transferencia transfronteriza e integración en nóminas globales a través de rieles digitales de liquidación instantánea 24/7.
  - **Contratos Inteligentes**: Automatización de financiamiento, préstamos y pagos de garantías sin burocracia ni intermediarios.
* **Resalto Táctico para el Administrador**:
  > La contabilidad y el cumplimiento normativo pasan de ser revisiones trimestrales a **auditorías continuas e instantáneas en tiempo real**.

---

### Sección 5: Conclusión — El Rol del Gestor Empresarial
* **Título**: *5. Tu Papel como Líder: Del Trabajo Operativo a la Estrategia*
* **Contenido Narrativo**:
  - Desafío a los estudiantes de Gestión Empresarial: La automatización y la tokenización no son responsabilidad exclusiva del área de Sistemas o TI, sino la competencia central de la dirección corporativa.
  - Liberar al talento humano de tareas repetitivas para enfocarlo en la innovación, la empatía y la toma de decisiones estratégicas.
* **Mensaje Final Inspirador (Cierre Estilo TEDx)**:
  > *"Los tokens y la automatización no están diseñados para eliminar la gestión humana, sino para eliminar la burocracia y permitir que los líderes se dediquen a crear valor real."*

---

## 5. Código Semilla HTML/CSS/JavaScript (Prototipo Funcional)

Tu agente de IA puede utilizar este bloque de código como plantilla base para generar la versión final:

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

    /* Navbar Flotante */
    header {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      padding: 1.2rem 2.5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      z-index: 100;
      background: rgba(15, 15, 15, 0.75);
      backdrop-filter: blur(12px);
      border-bottom: 1px solid rgba(255, 255, 255, 0.05);
    }

    .brand {
      font-weight: 900;
      font-size: 1.1rem;
      letter-spacing: 1px;
    }

    .brand span { color: var(--accent-ted); }

    .slide-counter {
      font-weight: 700;
      color: var(--text-muted);
      font-size: 0.95rem;
    }

    /* Contenedor Principal con Scroll Snap */
    .presentation-container {
      height: 100vh;
      overflow-y: scroll;
      scroll-snap-type: y mandatory;
      scroll-behavior: smooth;
    }

    .slide {
      height: 100vh;
      width: 100vw;
      scroll-snap-align: start;
      scroll-snap-stop: always;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 4rem 10%;
      text-align: center;
      position: relative;
    }

    .slide-content {
      max-width: 1000px;
      opacity: 0;
      transform: translateY(30px);
      transition: all 0.8s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .slide.active .slide-content {
      opacity: 1;
      transform: translateY(0);
    }

    h1, h2 {
      font-weight: 900;
      line-height: 1.1;
      margin-bottom: 1.5rem;
      font-size: var(--font-title);
      letter-spacing: -1px;
    }

    p {
      font-size: var(--font-body);
      color: var(--text-muted);
      line-height: 1.6;
      margin-bottom: 2rem;
    }

    /* Cajas de Resalto */
    .callout {
      background: var(--card-bg);
      border-left: 4px solid var(--accent-ted);
      padding: 1.5rem 2rem;
      border-radius: 0 12px 12px 0;
      text-align: left;
      margin: 2rem 0;
      font-size: var(--font-subtitle);
      color: var(--text-main);
    }

    .stat-number {
      font-size: clamp(3rem, 8vw, 6.5rem);
      font-weight: 900;
      color: var(--accent-ted);
      line-height: 1;
      margin-bottom: 0.5rem;
    }

    /* Panel de Control Flotante */
    .controls {
      position: fixed;
      bottom: 2rem;
      right: 2.5rem;
      display: flex;
      gap: 0.8rem;
      z-index: 100;
    }

    .btn-ctrl {
      background: var(--card-bg);
      color: var(--text-main);
      border: 1px solid rgba(255, 255, 255, 0.15);
      padding: 0.7rem 1.2rem;
      border-radius: 30px;
      cursor: pointer;
      font-weight: 700;
      font-size: 0.85rem;
      transition: all 0.2s ease;
    }

    .btn-ctrl:hover {
      background: var(--accent-ted);
      border-color: var(--accent-ted);
    }
  </style>
</head>
<body>

  <header>
    <div class="brand">TEDx<span>Talks</span> | Gestión Empresarial</div>
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
          "La tecnología no llega para reemplazar al administrador, sino para convertirse en su brújula estratégica."
        </div>
      </div>
    </section>

    <!-- Slide 1: Los Tokens -->
    <section class="slide">
      <div class="slide-content">
        <h2>1. La Doble Naturaleza del Token</h2>
        <p>Un solo término que impulsa dos motores empresariales simultáneos:</p>
        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; text-align: left; margin-top: 2rem;">
          <div style="background: var(--card-bg); padding: 1.8rem; border-radius: 12px;">
            <h3 style="color: var(--accent-ted); margin-bottom: 0.8rem;">Token en Inteligencia Artificial</h3>
            <p style="font-size: 0.95rem;">La unidad básica de procesamiento de contexto de los LLMs. Es el átomo que transforma datos en decisiones.</p>
          </div>
          <div style="background: var(--card-bg); padding: 1.8rem; border-radius: 12px;">
            <h3 style="color: var(--accent-ted); margin-bottom: 0.8rem;">Token Financiero (RWA)</h3>
            <p style="font-size: 0.95rem;">La representación digital y fraccionada de activos reales en blockchain para democratizar el capital.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Slide 2: Stat Impact -->
    <section class="slide">
      <div class="slide-content">
        <div class="stat-number">$16 BILLONES</div>
        <p style="font-size: var(--font-subtitle); color: var(--text-main);">Proyección de Activos del Mundo Real (RWA) tokenizados para 2030 (10% del PIB mundial).</p>
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
      modeToggle.textContent = document.body.classList.contains('presenter-mode') 
        ? 'Modo Lectura' 
        : 'Modo Exposición';
    });

    fullscreenToggle.addEventListener('click', () => {
      if (!document.fullscreenElement) {
        document.documentElement.requestFullscreen();
      } else {
        document.exitFullscreen();
      }
    });

    document.addEventListener('keydown', (e) => {
      if (e.key === 'ArrowDown' || e.key === ' ') {
        container.scrollBy({ top: window.innerHeight, behavior: 'smooth' });
      } else if (e.key === 'ArrowUp') {
        container.scrollBy({ top: -window.innerHeight, behavior: 'smooth' });
      } else if (e.key.toLowerCase() === 'f') {
        fullscreenToggle.click();
      }
    });
  </script>
</body>
</html>
```

---

## 6. Lista de Verificación y Criterios de Aceptación (QA)

Antes de dar por concluida la generación de la página web por parte de tu agente de IA, verifica los siguientes puntos:

- [ ] **Desplazamiento Fluido**: Cada movimiento de rueda o flechas ajusta de manera exacta la pantalla al inicio de la diapositiva (`scroll-snap`).
- [ ] **Legibilidad de Exposición**: Al activar el **Modo Exposición**, los títulos son legibles desde una distancia mínima de 5 metros.
- [ ] **Contraste Accesible**: Cumplimiento del estándar WCAG AAA para texto blanco sobre fondo oscuro (`#0F0F0F`).
- [ ] **Cero Librerías Externas Pesadas**: Funcionamiento autónomo utilizando exclusivamente CSS nativo y JavaScript Vanilla sin sobrecargar el rendimiento.
- [ ] **Fundamentación Técnica**: Cita implícita y adecuada de los conceptos de tokenización de IA, RWA ($16 Billones), IA Agéntica y automatización de procesos.
