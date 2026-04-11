<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>QA Portal</title>

<style>
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto;
  background: #F8FAFC;
  color: #0F172A;
  padding: 16px;
  margin: 0;
}

.container {
  max-width: 640px;
  margin: 0 auto;
}

/* ========================
   MENU
======================== */
.menu {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.menu-item {
  padding: 8px 14px;
  border-radius: 10px;
  border: 1px solid #E2E8F0;
  background: #FFFFFF;
  cursor: pointer;
}

.menu-item.active {
  background: #E0F2FE;
  border-color: #38BDF8;
  color: #0369A1;
}

.badge {
  margin-left: 6px;
}

/* ========================
   SEARCH
======================== */
.search input {
  width: 100%;
  box-sizing: border-box;
  padding: 14px;
  border-radius: 14px;
  border: 1px solid #E2E8F0;
  font-size: 16px;
}

/* ========================
   GRID
======================== */
.grid {
  display: grid;
  gap: 16px;
  margin-top: 20px;
}

/* ========================
   CARD
======================== */
.card {
  background: #FFFFFF;
  padding: 18px;
  border-radius: 16px;
  border: 1px solid #E2E8F0;
}

.title {
  font-weight: 600;
}

/* ========================
   BUTTONS
======================== */
.buttons {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}

.btn {
  flex: 1;
  padding: 12px;
  border-radius: 12px;
  text-align: center;
  text-decoration: none;
  font-weight: 500;
  border: none;
  cursor: pointer;
}

.android {
  background: #DCFCE7;
  color: #166534;
}

.ios {
  background: #F1F5F9;
  color: #334155;
}

/* ========================
   HEALTH
======================== */
.toggle {
  display: flex;
  justify-content: space-between;
  cursor: pointer;
}

.arrow {
  transition: transform 0.2s;
}

.arrow.open {
  transform: rotate(90deg);
}

.services {
  display: none;
  margin-top: 10px;
}

.services.open {
  display: block;
}

.service {
  display: flex;
  justify-content: space-between;
  margin-top: 8px;
}

/* ========================
   WATERMARK
======================== */
.watermark {
  position: fixed;
  bottom: 10px;
  width: 100%;
  text-align: center;
  font-size: 12px;
  color: #94A3B8;
}
</style>
</head>

<body>

<div class="container">

  <!-- MENU -->
  <div class="menu">
    <button class="menu-item active" onclick="showPage('home')">Home</button>
    <button class="menu-item" onclick="showPage('deeplinks')">Deeplinks</button>
    <button class="menu-item" onclick="showPage('health')">
      Health <span id="health-badge" class="badge"></span>
    </button>
  </div>

  <!-- HOME -->
  <div id="home-page">
    <h1>QA Portal 🧪</h1>
    <p style="color:#64748B;">
      Central de testes e validação de ambientes
    </p>

    <div class="grid">
      <div class="card">
        <div class="title">🔗 Deeplinks</div>
        <div class="buttons">
          <button class="btn ios" onclick="showPage('deeplinks')">Acessar</button>
        </div>
      </div>

      <div class="card">
        <div class="title">🚦 Health</div>
        <div class="buttons">
          <button class="btn android" onclick="showPage('health')">Ver status</button>
        </div>
      </div>

      <div class="card">
        <div class="title">🧪 Gerar massa de dados</div>
        <div class="buttons">
          <button class="btn android" onclick="showPage('test-data')">Acessar</button>
        </div>
      </div>

      <div class="card">
        <div class="title">📊 Jira APIs</div>
        <div class="buttons">
          <button class="btn ios" onclick="showPage('jira-api')">Acessar</button>
        </div>
      </div>
    </div>
  </div>

  <!-- TEST DATA -->
  <div id="test-data-page" style="display:none;">
    <h1>🧪 Test Data Factory</h1>
    <p style="color:#64748B;">Geração e busca de massa de dados para testes</p>

    <div class="grid">
      <div class="card">
        <div class="title">Buscar cenário existente</div>
        <div class="buttons">
          <button class="btn android">Buscar</button>
        </div>
      </div>

      <div class="card">
        <div class="title">Criar cliente com pedido</div>
        <div class="buttons">
          <button class="btn ios">Gerar</button>
        </div>
      </div>
    </div>
  </div>

  <!-- JIRA API -->
  <div id="jira-api-page" style="display:none;">
    <h1>📊 Jira APIs</h1>
    <p style="color:#64748B;">Extrações e automações via API</p>

    <div class="grid">
      <div class="card">
        <div class="title">Exportar issues sem resolution</div>
        <div class="buttons">
          <button class="btn android">Gerar CSV</button>
        </div>
      </div>

      <div class="card">
        <div class="title">Exportar dados avançados</div>
        <div class="buttons">
          <button class="btn ios">Executar</button>
        </div>
      </div>
    </div>
  </div>

  <!-- DEEPLINKS -->
  <div id="deeplinks-page" style="display:none;">
    <h1>Deeplinks</h1>

    <div class="search">
      <input id="search" placeholder="Buscar..." />
    </div>

    <div class="grid" id="grid"></div>
  </div>

  <!-- HEALTH -->
  <div id="health-page" style="display:none;">
    <h1>Health 🚦</h1>
    <div class="grid" id="health-grid"></div>
  </div>

</div>

<div class="watermark">Desenvolvido por Chapter QA</div>

<script>

// ========================
// NAV
// ========================
function showPage(page) {
  document.getElementById('home-page').style.display = page === 'home' ? 'block' : 'none';
  document.getElementById('deeplinks-page').style.display = page === 'deeplinks' ? 'block' : 'none';
  document.getElementById('health-page').style.display = page === 'health' ? 'block' : 'none';
  document.getElementById('test-data-page').style.display = page === 'test-data' ? 'block' : 'none';
  document.getElementById('jira-api-page').style.display = page === 'jira-api' ? 'block' : 'none';

  document.querySelectorAll('.menu-item').forEach(b => b.classList.remove('active'));

  if (page === 'home') document.querySelectorAll('.menu-item')[0].classList.add('active');
  if (page === 'deeplinks') document.querySelectorAll('.menu-item')[1].classList.add('active');
  if (page === 'health') {
    document.querySelectorAll('.menu-item')[2].classList.add('active');
    loadHealth();
  }
}

// ========================
// (restante do seu código permanece IGUAL)
// ========================

</script>

</body>
</html>