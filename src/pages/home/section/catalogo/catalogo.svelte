<script lang="ts">
  import './catalogo.css';
  import { assetUrl } from '../../../../assets';
  import { onMount } from 'svelte';

  const originalScripts: { attributes: string[][]; content: string }[] = [];
  onMount(() => {
    const previousClass = document.body.className;
    const previousStyle = document.body.getAttribute('style');
    const titleElement = document.head.querySelector('title');
    const previousTitleId = titleElement?.getAttribute('id');
    
    
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
      
      
    };
  });
</script>

<section id="catalogo" class="fondo-principal">
  <div class="contenedor-seccion">
    <div class="catalogo-header">
      <span>Colección Exclusiva</span>
      <h2>Explora nuestros productos</h2>
    </div>

    <div style="display: flex; justify-content: flex-end; margin-bottom: 1.5rem; width: 100%;"><a href="catalogo.html" class="boton-catalogo" style="flex: 0 0 auto !important; width: auto !important; display: inline-flex; padding: 0.65rem 1rem;">Ver catálogo completo</a></div><div class="catalogo-contenido cuadricula">
      <!-- Tarjeta 1 -->
      <article class="catalogo-item">
        <div class="catalogo-imagen">
          <img src={assetUrl("imagenes/helado 1.webp")} alt="Vasos Cool">
        </div>
        <div class="item-contenido">
          <div class="informacion-producto">
            <h3><a href="detalle.html?titulo=Vasos+Cool&amp;precio=&amp;desc=Vasos+de+helados+tradicionales+con+mucho+sabor+natural+y+una+cremosidad+artesanal+irresistible.&amp;img=%2Fimagenes%2Fhelado+1.webp" style="color: inherit; text-decoration: none;">Vasos Cool</a></h3>
            <span class="precio-label">$30.000</span>
          </div>
          <p class="producto-descripcion">
            Vasos de helados tradicionales con mucho sabor natural y una cremosidad artesanal irresistible.
          </p>
          <div class="producto-accion">
            <a href="#catalogo" target="_blank" rel="noopener noreferrer" class="boton-catalogo">Ver detalles</a>
          </div>
        </div>
      </article>

      <!-- Tarjeta 2 -->
      <article class="catalogo-item">
        <div class="catalogo-imagen">
          <img src={assetUrl("imagenes/helado2.jpg")} alt="Paletas mundo green">
        </div>
        <div class="item-contenido">
          <div class="informacion-producto">
            <h3><a href="detalle.html?titulo=Paletas+mundo+green&amp;precio=&amp;desc=Deliciosas+paletas+de+kiwi+natural+ba%C3%B1adas+en+chocolate+oscuro+belga+con+un+toque+crujiente+en+la+punta.&amp;img=%2Fimagenes%2Fhelado2.jpg" style="color: inherit; text-decoration: none;">Paletas mundo green</a></h3>
            <span class="precio-label">$25.000</span>
          </div>
          <p class="producto-descripcion">
            Deliciosas paletas de kiwi natural bañadas en chocolate oscuro belga con un toque crujiente en la punta.
          </p>
          <div class="producto-accion">
            <a href="#catalogo" target="_blank" rel="noopener noreferrer" class="boton-catalogo">Ver detalles</a>
          </div>
        </div>
      </article>

      <!-- Tarjeta 3 -->
      <article class="catalogo-item">
        <div class="catalogo-imagen">
          <img src={assetUrl("imagenes/helado3.jpg")} alt="Banana Split de la casa">
        </div>
        <div class="item-contenido">
          <div class="informacion-producto">
            <h3><a href="detalle.html?titulo=Banana+Split+de+la+casa&amp;precio=&amp;desc=Preparaci%C3%B3n+tradicional+con+banano+fresco%2C+tres+bolas+de+gelato+artesanal%2C+crema+chantilly+y+cereza.&amp;img=%2Fimagenes%2Fhelado3.jpg" style="color: inherit; text-decoration: none;">Banana Split de la casa</a></h3>
            <span class="precio-label">$35.000</span>
          </div>
          <p class="producto-descripcion">
            Preparación tradicional con banano fresco, tres bolas de gelato artesanal, crema chantilly y cereza.
          </p>
          <div class="producto-accion">
            <a href="#catalogo" target="_blank" rel="noopener noreferrer" class="boton-catalogo">Ver detalles</a>
          </div>
        </div>
      </article>
    </div>
  </div>
</section>