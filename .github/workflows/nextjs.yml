<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Minha Loja de Apps</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f9;
      color: #333;
    }
    header {
      background: #6200ea;
      color: white;
      padding: 12px 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      position: sticky;
      top: 0;
      z-index: 10;
    }
    header h1 {
      font-size: 18px;
    }
    header button {
      background: none;
      border: none;
      color: white;
      font-size: 22px;
      cursor: pointer;
    }
    .container {
      padding: 10px;
    }
    .app-card {
      background: white;
      border-radius: 12px;
      padding: 12px;
      margin-bottom: 12px;
      display: flex;
      align-items: center;
      box-shadow: 0 2px 5px rgba(0,0,0,0.08);
      transition: transform 0.2s;
    }
    .app-card:hover {
      transform: scale(1.01);
    }
    .app-card img {
      width: 64px;
      height: 64px;
      border-radius: 12px;
      margin-right: 12px;
      flex-shrink: 0;
    }
    .app-info {
      flex: 1;
      min-width: 0;
    }
    .app-info h2 {
      font-size: 16px;
      margin-bottom: 4px;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    .app-info p {
      font-size: 13px;
      color: #555;
      max-height: 36px;
      overflow: hidden;
    }
    .app-info small {
      font-size: 12px;
      color: #777;
      display: block;
      margin-top: 4px;
    }
    .download-btn {
      background: #6200ea;
      color: white;
      border: none;
      padding: 8px 14px;
      border-radius: 8px;
      cursor: pointer;
      font-size: 13px;
      flex-shrink: 0;
    }
    /* Tela de pesquisa */
    #search-screen {
      display: none;
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: #fff;
      z-index: 20;
      overflow-y: auto;
    }
    #search-screen header {
      background: #6200ea;
      padding: 12px 16px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    #search-screen header h2 {
      font-size: 16px;
      color: white;
    }
    #search-screen header button {
      background: none;
      border: none;
      color: white;
      font-size: 20px;
      cursor: pointer;
    }
    #search-input {
      width: 100%;
      padding: 10px;
      margin: 12px 0;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 14px;
    }
  </style>
</head>
<body>
  <header>
    <h1>Minha Loja</h1>
    <button onclick="openSearch()">🔍</button>
  </header>
  
  <div class="container" id="app-list"></div>

  <!-- Tela de pesquisa -->
  <div id="search-screen">
    <header>
      <h2>Pesquisar</h2>
      <button onclick="closeSearch()">✖</button>
    </header>
    <div class="container">
      <input type="text" id="search-input" placeholder="Digite o nome do app..." oninput="searchApps()">
      <div id="search-results"></div>
    </div>
  </div>

  <script>
    const API_URL = "https://billing.developerbox.xyz/apimaker/apiforlink.php?token=7zeytk8ibvtnw1r0xtrr";
    let appsData = [];

    async function loadApps() {
      try {
        const response = await fetch(API_URL);
        appsData = await response.json();
        renderApps(appsData, "app-list");
      } catch (error) {
        console.error("Erro ao carregar apps:", error);
        document.getElementById("app-list").innerHTML = "<p>Erro ao carregar apps.</p>";
      }
    }

    function renderApps(data, containerId) {
      const container = document.getElementById(containerId);
      container.innerHTML = "";
      if (!data.length) {
        container.innerHTML = "<p>Nenhum app encontrado.</p>";
        return;
      }
      data.forEach(app => {
        const descricao = (app.descricao || "").replace(/\*\*/g, "").replace(/\n/g, " ");
        const card = document.createElement("div");
        card.className = "app-card";
        card.innerHTML = `
          <img src="${app.img_url}" alt="${app.nome}">
          <div class="app-info">
            <h2>${app.nome}</h2>
            <p>${descricao}</p>
            <small>Dev: ${app.developer} • Versão: ${app.versao}</small>
          </div>
          <a href="${app.link}" target="_blank">
            <button class="download-btn">Baixar</button>
          </a>
        `;
        container.appendChild(card);
      });
    }

    function openSearch() {
      document.getElementById("search-screen").style.display = "block";
      document.getElementById("search-input").focus();
    }

    function closeSearch() {
      document.getElementById("search-screen").style.display = "none";
      document.getElementById("search-input").value = "";
      document.getElementById("search-results").innerHTML = "";
    }

    function searchApps() {
      const query = document.getElementById("search-input").value.toLowerCase();
      const filtered = appsData.filter(app => 
        app.nome.toLowerCase().includes(query)
      );
      renderApps(filtered, "search-results");
    }

    loadApps();
  </script>
</body>
</html>
