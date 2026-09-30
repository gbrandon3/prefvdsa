<script lang="ts">
  import './catalogo.css';
  import { assetUrl } from '../../assets';
  import { onMount } from 'svelte';
  import Navbar from '../home/section/navbar/navbar.svelte';
  import Footer from '../home/section/footer/footer.svelte';
  const originalScripts: { attributes: string[][]; content: string }[] = [{"attributes":[],"content":"\n(() => {\n  const navbar = document.body.querySelector('header, nav, .navbar, #navbar, .barra-navegacion');\n  if (!navbar) return;\n  const update = () => {\n    const fixed = getComputedStyle(navbar).position === 'fixed';\n    document.body.style.setProperty('--pagina-navbar-offset', fixed ? Math.max(0, navbar.getBoundingClientRect().bottom) + 'px' : '0px');\n  };\n  update();\n  const observer = new ResizeObserver(update);\n  observer.observe(navbar);\n  window.addEventListener('resize', update);\n  window.addEventListener('load', update, { once: true });\n})();\n"}];
  onMount(() => {
    const previousClass = document.body.className;
    const previousStyle = document.body.getAttribute('style');
    const titleElement = document.head.querySelector('title');
    const previousTitleId = titleElement?.getAttribute('id');
    
    document.body.className = "pagina-catalogo-cuerpo";
    document.body.setAttribute('style', "");
    const mountedScripts: HTMLScriptElement[] = [];
    let cancelled = false;
    // Re-run the original page scripts after Svelte mounts their original DOM.
    queueMicrotask(async () => {
      for (const original of originalScripts) {
        if (cancelled) break;
        const script = document.createElement('script');
        for (const [name, value] of original.attributes) {
          script.setAttribute(name, name === 'src' ? assetUrl(value) : value);
        }
        script.textContent = original.content.replace(/\b(?:window\.)?location\.search\b/g, '(window.__svelteProductSearch ?? window.location.search)');
        const loaded = script.src ? new Promise<void>((resolve) => {
          script.onload = () => resolve();
          script.onerror = () => resolve();
        }) : Promise.resolve();
        mountedScripts.push(script);
        document.body.appendChild(script);
        await loaded;
      }
    });
    return () => {
      cancelled = true;
      mountedScripts.forEach((script) => script.remove());
      
      document.body.className = previousClass;
      if (previousStyle === null) document.body.removeAttribute('style');
      else document.body.setAttribute('style', previousStyle);
    };
  });
</script>
<svelte:head><meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Explora nuestros productos • Catálogo Oficial</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="">
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&amp;family=Playfair+Display:ital,wght@0,500;0,600;0,700;1,400&amp;display=swap" rel="stylesheet"></svelte:head>


  <!-- 1. Header / Navbar Original del Proyecto (index.html) -->
<Navbar pageAttributes={{"id":"barra-navegacion","class":"navbar"}} pageLinks={["index.html#heroe","index.html#heroe","index.html#sobre-nosotros","index.html#catalogo","index.html#contacto"]} />

  <!-- 2. Área Principal del Catálogo -->
  <main class="seccion-catalogo-externa">
    <section id="catalogo">
      <div class="contenedor-seccion">
        <div class="catalogo-header">
          <span style="color: #3A2312 !important;">Colección Exclusiva</span>
          <h2 style="color: var(--color-titulos, #e82a61) !important;">Explora nuestros productos</h2>
          <p style="color: #1c2e33 !important; display: -webkit-box !important; -webkit-line-clamp: 3 !important; -webkit-box-orient: vertical !important; overflow: hidden !important; text-overflow: ellipsis !important;">Explora nuestra colección completa de artículos.</p>
        </div>
        <div class="catalogo-grid-wrapper">
        <!-- Tarjeta: Vasos Cool -->
        <div class="card-overlay-hover">
          <div class="card-img-box">
            <img src={assetUrl("imagenes/helado 1.webp")} alt="Foto de Vasos Cool" loading="lazy" onerror="this.onerror=null;this.src='https://images.unsplash.com/photo-1522335789203-aabd1fc54bc9?w=800&amp;auto=format&amp;fit=crop&amp;q=80';">
          </div>
          <div class="card-badge-flotante">
            <span>$30.000</span>
          </div>
          <div class="card-capa-hover">
            <h3>Vasos Cool</h3>
            <span class="card-precio">$30.000</span>
            <p style="display: -webkit-box !important; -webkit-line-clamp: 3 !important; -webkit-box-orient: vertical !important; overflow: hidden !important; text-overflow: ellipsis !important;">Vasos de helados tradicionales con mucho sabor natural y una cremosidad artesanal irresistible.</p>
            <a href="detalle.html?titulo=Vasos%20Cool&amp;precio=%2430.000&amp;img=.%2Fimagenes%2Fhelado%201.webp&amp;desc=Vasos%20de%20helados%20tradicionales%20con%20mucho%20sabor%20natural%20y%20una%20cremosidad%20artesanal%20irresistible." class="card-boton-accion" style="background-color: var(--color-secundario, #3A2312) !important; color: #ffffff !important; text-decoration: none !important;">
              <span style="color: #ffffff !important; font-weight: 600 !important; text-transform: none !important; letter-spacing: normal !important; margin: 0 !important;">Ver detalles</span>
            </a>
          </div>
        </div>

        <!-- Tarjeta: Paletas mundo green -->
        <div class="card-overlay-hover">
          <div class="card-img-box">
            <img src={assetUrl("imagenes/helado2.jpg")} alt="Foto de Paletas mundo green" loading="lazy" onerror="this.onerror=null;this.src='https://images.unsplash.com/photo-1596462502278-27bfdc403348?w=800&amp;auto=format&amp;fit=crop&amp;q=80';">
          </div>
          <div class="card-badge-flotante">
            <span>$25.000</span>
          </div>
          <div class="card-capa-hover">
            <h3>Paletas mundo green</h3>
            <span class="card-precio">$25.000</span>
            <p style="display: -webkit-box !important; -webkit-line-clamp: 3 !important; -webkit-box-orient: vertical !important; overflow: hidden !important; text-overflow: ellipsis !important;">Deliciosas paletas de kiwi natural bañadas en chocolate oscuro belga con un toque crujiente en la punta.</p>
            <a href="detalle.html?titulo=Paletas%20mundo%20green&amp;precio=%2425.000&amp;img=.%2Fimagenes%2Fhelado2.jpg&amp;desc=Deliciosas%20paletas%20de%20kiwi%20natural%20ba%C3%B1adas%20en%20chocolate%20oscuro%20belga%20con%20un%20toque%20crujiente%20en%20la%20punta." class="card-boton-accion" style="background-color: var(--color-secundario, #3A2312) !important; color: #ffffff !important; text-decoration: none !important;">
              <span style="color: #ffffff !important; font-weight: 600 !important; text-transform: none !important; letter-spacing: normal !important; margin: 0 !important;">Ver detalles</span>
            </a>
          </div>
        </div>

        <!-- Tarjeta: Banana Split de la casa -->
        <div class="card-overlay-hover">
          <div class="card-img-box">
            <img src={assetUrl("imagenes/helado3.jpg")} alt="Foto de Banana Split de la casa" loading="lazy" onerror="this.onerror=null;this.src='https://images.unsplash.com/photo-1556911220-e15b29be8c8f?w=800&amp;auto=format&amp;fit=crop&amp;q=80';">
          </div>
          <div class="card-badge-flotante">
            <span>$35.000</span>
          </div>
          <div class="card-capa-hover">
            <h3>Banana Split de la casa</h3>
            <span class="card-precio">$35.000</span>
            <p style="display: -webkit-box !important; -webkit-line-clamp: 3 !important; -webkit-box-orient: vertical !important; overflow: hidden !important; text-overflow: ellipsis !important;">Preparación tradicional con banano fresco, tres bolas de gelato artesanal, crema chantilly y cereza.</p>
            <a href="detalle.html?titulo=Banana%20Split%20de%20la%20casa&amp;precio=%2435.000&amp;img=.%2Fimagenes%2Fhelado3.jpg&amp;desc=Preparaci%C3%B3n%20tradicional%20con%20banano%20fresco%2C%20tres%20bolas%20de%20gelato%20artesanal%2C%20crema%20chantilly%20y%20cereza." class="card-boton-accion" style="background-color: var(--color-secundario, #3A2312) !important; color: #ffffff !important; text-decoration: none !important;">
              <span style="color: #ffffff !important; font-weight: 600 !important; text-transform: none !important; letter-spacing: normal !important; margin: 0 !important;">Ver detalles</span>
            </a>
          </div>
        </div>
        </div>
      </div>
    </section>
  </main>

  <!-- 3. Footer Original del Proyecto (index.html) -->
<Footer pageAttributes={{"class":"sitio-footer fondo-principal","id":"pie-de-pagina"}} pageLinks={["index.html#heroe","index.html#sobre-nosotros","index.html#catalogo","index.html#contacto","https://instagram.com"]} />



