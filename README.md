# Canarias-Habla<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Canarias Habla</title>
  <style>
    body { font-family: sans-serif; margin:0; padding:0; background:#f0f0f0; }
    header, footer { background:#003366; color:white; text-align:center; padding:1rem; }
    nav a { margin:0 1rem; color:white; text-decoration:none; }
    .container { max-width:800px; margin:2rem auto; background:white; padding:1rem; border-radius:5px; }
    .news-item { border-bottom:1px solid #ddd; padding:1rem 0; }
    .news-item:last-child { border:none; }
    .news-item h2 { margin:0 0 .5rem; }
    .admin { margin-top:2rem; padding-top:1rem; border-top:2px solid #003366; }
    .admin input, .admin textarea { width:100%; margin-bottom:.5rem; }
  </style>
</head>
<body>
  <header><h1>Canarias Habla</h1></header>
  <nav>
    <a href="#">Inicio</a>
    <a href="#">Actualidad</a>
    <a href="#">Opinión</a>
    <a href="#">Entrevistas</a>
    <a href="#">Contacto</a>
  </nav>
  <div class="container">
    <div id="news"></div>

    <!-- Panel de administración simulada -->
    <div class="admin">
      <h2>Administrar Noticias</h2>
      <input type="text" id="admin-title" placeholder="Título" />
      <textarea id="admin-content" placeholder="Contenido"></textarea>
      <button id="admin-add">Añadir noticia</button>
    </div>
  </div>
  <footer>&copy; 2025 Canarias Habla. Todos los derechos reservados.</footer>

  <script>
    const newsEl = document.getElementById('news');
    const apiUrl = 'https://api.canarias-habla.fake/news';

    async function loadNews() {
      try {
        const res = await fetch(apiUrl);
        const items = await res.json();
        newsEl.innerHTML = '';
        items.forEach(item => {
          const div = document.createElement('div');
          div.className = 'news-item';
          div.innerHTML = \`
            <h2>\${item.title}</h2>
            <p><small>\${new Date(item.date).toLocaleString()}</small></p>
            <p>\${item.content}</p>\`;
          newsEl.appendChild(div);
        });
      } catch (err) {
        newsEl.innerHTML = '<p>Error cargando noticias.</p>';
      }
    }

    // Modo admin simulado
    document.getElementById('admin-add').onclick = () => {
      const title = document.getElementById('admin-title').value;
      const content = document.getElementById('admin-content').value;
      if (!title || !content) return alert('Faltan campos');
      const item = { title, content, date: new Date().toISOString() };
      // Aquí haría POST a la API:
      // fetch(apiUrl, { method:'POST', body: JSON.stringify(item), headers:{'Content-Type':'application/json'} })
      alert('Noticia añadida (modo demo)');
      loadNews();
    };

    loadNews();
  </script>
</body>
</html>
