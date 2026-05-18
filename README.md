[stock_v4_firebase 2.html](https://github.com/user-attachments/files/27971597/stock_v4_firebase.2.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Stock — Innova Center</title>
<style>
:root{
  --azul:#1A3557;--azul-m:#2563A8;--azul-cl:#D6E4F7;
  --verde:#1A7A4A;--verde-cl:#D4EDDA;
  --amarillo:#856404;--amarillo-cl:#FFF3CD;
  --rojo:#842029;--rojo-cl:#F8D7DA;
  --violeta:#4C3494;--violeta-cl:#EDE9FC;
  --naranja:#92400e;--naranja-cl:#FEF3C7;
  --borde:#ddd;--text:#1a1a1a;--text-s:#555;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:Arial,sans-serif;background:#eef2f7;color:var(--text);font-size:14px}

/* LOGIN */
.login-screen{position:fixed;inset:0;background:var(--azul);display:flex;align-items:center;justify-content:center;z-index:1000;flex-direction:column;gap:24px}
.login-screen.hidden{display:none}
.login-box{background:white;border-radius:16px;padding:32px;width:340px;max-width:95vw;box-shadow:0 8px 40px rgba(0,0,0,.3)}
.login-box h2{font-size:18px;color:var(--azul);margin-bottom:6px;text-align:center}
.login-box p{font-size:13px;color:var(--text-s);text-align:center;margin-bottom:20px}
.user-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:16px}
.user-btn{padding:12px 8px;border:2px solid var(--borde);border-radius:10px;background:white;cursor:pointer;font-size:13px;font-weight:700;text-align:center;transition:all .15s;display:flex;flex-direction:column;align-items:center;gap:6px}
.user-btn:hover{border-color:var(--azul-m);background:var(--azul-cl)}
.user-btn.selected{border-color:var(--azul);background:var(--azul-cl)}
.user-btn .avatar{width:38px;height:38px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:16px;font-weight:700;color:white}
.pin-wrap{display:flex;flex-direction:column;gap:8px;margin-bottom:16px}
.pin-wrap input{padding:10px;border:1px solid var(--borde);border-radius:8px;font-size:18px;letter-spacing:6px;text-align:center;font-family:monospace}
.login-err{color:var(--rojo);font-size:12px;text-align:center;min-height:16px}

/* HEADER */
header{background:var(--azul);color:white;padding:12px 20px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:8px}
header h1{font-size:16px;font-weight:700}
.user-badge{display:flex;align-items:center;gap:8px;background:rgba(255,255,255,.15);border-radius:20px;padding:5px 12px;font-size:12px}
.user-dot{width:24px;height:24px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:11px;font-weight:700;color:white}

/* TABS */
.tabs{background:white;border-bottom:2px solid var(--borde);display:flex;padding:0 14px;overflow-x:auto;gap:0}
.tab{padding:10px 14px;font-size:13px;font-weight:700;color:var(--text-s);cursor:pointer;border-bottom:3px solid transparent;margin-bottom:-2px;white-space:nowrap;transition:color .15s}
.tab:hover{color:var(--azul-m)}
.tab.active{color:var(--azul);border-bottom-color:var(--azul)}
.tab.admin-only{display:none}
.tab.admin-only.show{display:block}

/* TOOLBAR */
.toolbar{background:white;border-bottom:1px solid var(--borde);padding:8px 20px;display:flex;gap:8px;flex-wrap:wrap;align-items:center}
button{padding:7px 13px;border:1px solid var(--borde);border-radius:6px;background:white;cursor:pointer;font-size:13px;font-family:Arial;display:inline-flex;align-items:center;gap:5px;transition:background .15s}
button:hover{background:#f0f4f8}
button.primary{background:var(--azul);color:white;border-color:var(--azul)}
button.primary:hover{background:var(--azul-m)}
button.accent{background:var(--violeta);color:white;border-color:var(--violeta)}
button.accent:hover{background:#3a2675}
button.sm{padding:3px 8px;font-size:12px;border-radius:5px}
button.danger-btn{color:var(--rojo);border-color:var(--rojo-cl)}

/* STATS */
.stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(130px,1fr));gap:10px;padding:12px 20px}
.stat{background:white;border-radius:10px;padding:11px 14px;border:1px solid var(--borde)}
.stat .num{font-size:24px;font-weight:700}
.stat .lbl{font-size:11px;color:var(--text-s);margin-top:2px}
.stat.ok .num{color:var(--verde)}
.stat.warn .num{color:var(--amarillo)}
.stat.danger .num{color:var(--rojo)}

.alert-bar{margin:0 20px 8px;padding:10px 14px;border-radius:8px;background:var(--rojo-cl);border:1px solid #f5c2c7;color:var(--rojo);font-size:12px;display:none;line-height:1.6}
.section{margin:0 20px 20px}
.section h2{font-size:11px;font-weight:700;color:var(--text-s);text-transform:uppercase;letter-spacing:.06em;margin-bottom:8px}
.table-wrap{background:white;border-radius:10px;border:1px solid var(--borde);overflow:auto}
table{width:100%;border-collapse:collapse;min-width:500px}
thead th{background:var(--azul-m);color:white;padding:8px 12px;text-align:left;font-size:12px;font-weight:700;white-space:nowrap}
tbody tr{border-bottom:1px solid #f0f0f0;transition:background .1s}
tbody tr:last-child{border-bottom:none}
tbody tr:hover{background:#f8fbff}
tbody td{padding:7px 12px;font-size:13px;vertical-align:middle}

.badge{display:inline-flex;align-items:center;gap:4px;padding:2px 8px;border-radius:20px;font-size:11px;font-weight:700}
.badge.ok{background:var(--verde-cl);color:var(--verde)}
.badge.warn{background:var(--amarillo-cl);color:var(--amarillo)}
.badge.danger{background:var(--rojo-cl);color:var(--rojo)}
.badge.cfg{background:#e8f4fd;color:#0c4a7c}
.bar-wrap{width:75px;height:5px;background:#e5e5e5;border-radius:3px;display:inline-block;vertical-align:middle;overflow:hidden}
.bar{height:100%;border-radius:3px}
.bar.ok{background:var(--verde)}
.bar.warn{background:#e6a817}
.bar.danger{background:var(--rojo)}
.venc-ok{font-size:11px;color:var(--verde)}
.venc-pronto{font-size:11px;color:var(--amarillo);font-weight:700}
.venc-vencido{font-size:11px;color:var(--rojo);font-weight:700}
.venc-nd{font-size:11px;color:#bbb}

/* HISTORIAL */
.hist-list{padding:4px 0;max-height:280px;overflow-y:auto}
.hist-item{display:flex;justify-content:space-between;align-items:flex-start;padding:7px 14px;border-bottom:1px solid #f0f0f0;font-size:12px;gap:8px}
.hist-item:last-child{border-bottom:none}
.tag{padding:2px 8px;border-radius:10px;font-size:11px;font-weight:700;white-space:nowrap}
.tag.in{background:var(--verde-cl);color:var(--verde)}
.tag.out{background:var(--rojo-cl);color:var(--rojo)}
.tag.proc{background:var(--violeta-cl);color:var(--violeta)}

/* PRESTACIONES */
.prest-row{display:grid;grid-template-columns:1fr auto;gap:8px;align-items:center;padding:8px 12px;background:white;border:1px solid var(--borde);border-radius:8px;margin-bottom:4px}
.prest-row:hover{border-color:var(--azul-cl)}
.prest-name{font-size:13px;font-weight:500}
.prest-dur{font-size:11px;color:var(--text-s);margin-top:1px}
.prest-actions{display:flex;gap:5px;align-items:center}
.cat-title{font-size:12px;font-weight:700;color:var(--azul);text-transform:uppercase;letter-spacing:.04em;padding:8px 12px;background:var(--azul-cl);border-radius:7px;margin-bottom:5px;margin-top:12px}

/* ADMIN */
.admin-card{background:white;border-radius:12px;border:1px solid var(--borde);overflow:hidden;margin-bottom:16px}
.admin-card-head{padding:13px 18px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:8px}
.admin-card-body{padding:14px 18px;font-size:13px;color:var(--text-s);border-bottom:1px solid #f0f0f0}
.admin-list{max-height:300px;overflow-y:auto}
.admin-item{display:flex;align-items:center;justify-content:space-between;padding:9px 18px;border-bottom:1px solid #f4f4f4;gap:8px}
.admin-item:last-child{border-bottom:none}
.admin-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:16px;padding:16px 20px}

/* USUARIOS */
.user-admin-row{display:flex;align-items:center;justify-content:space-between;padding:10px 18px;border-bottom:1px solid #f4f4f4;gap:8px}
.user-admin-row:last-child{border-bottom:none}

/* MODAL */
.overlay{position:fixed;inset:0;background:rgba(0,0,0,.45);display:none;align-items:center;justify-content:center;z-index:200}
.overlay.open{display:flex}
.modal{background:white;border-radius:12px;padding:22px;width:440px;max-width:96vw;box-shadow:0 8px 32px rgba(0,0,0,.2);max-height:90vh;overflow-y:auto}
.modal h3{font-size:15px;font-weight:700;margin-bottom:14px;color:var(--azul)}
.field{display:flex;flex-direction:column;gap:4px;margin-bottom:12px}
.field label{font-size:12px;color:var(--text-s);font-weight:700}
.field input,.field select,.field textarea{padding:8px 10px;border:1px solid var(--borde);border-radius:6px;font-size:13px;font-family:Arial}
.modal-btns{display:flex;gap:8px;justify-content:flex-end;margin-top:16px}
.insumo-line{display:grid;grid-template-columns:1fr 80px 28px;gap:6px;align-items:center;margin-bottom:6px}
.insumo-line select,.insumo-line input{padding:6px 8px;border:1px solid var(--borde);border-radius:6px;font-size:12px;font-family:Arial}
.rm-btn{background:var(--rojo-cl);color:var(--rojo);border:none;border-radius:5px;cursor:pointer;width:26px;height:26px;display:flex;align-items:center;justify-content:center;font-size:15px}
.confirm-box{background:#f8f9fa;border-radius:8px;padding:12px;margin:10px 0}
.confirm-row{display:flex;justify-content:space-between;padding:4px 0;border-bottom:1px solid #eee;font-size:13px}
.confirm-row:last-child{border-bottom:none}
.warn-txt{color:var(--rojo);font-weight:700}
.page{display:none}
.page.active{display:block}
.search-box{padding:6px 10px;border:1px solid var(--borde);border-radius:6px;font-size:13px;font-family:Arial;min-width:180px}
.empty-row{text-align:center;padding:24px;color:var(--text-s);font-size:13px}

/* PIN dots */
.pin-dots{display:flex;gap:8px;justify-content:center;margin:8px 0}
.pin-dot{width:12px;height:12px;border-radius:50%;background:#ddd;transition:background .15s}
.pin-dot.filled{background:var(--azul)}
.numpad{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-top:10px}
.numpad-btn{padding:14px;border:1px solid var(--borde);border-radius:8px;font-size:18px;font-weight:700;cursor:pointer;background:white;transition:background .15s;text-align:center}
.numpad-btn:hover{background:var(--azul-cl)}
.numpad-btn.del{color:var(--rojo)}
</style>

  <!-- ══ FIREBASE SDK ══ -->
  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js";
    import { getFirestore, doc, getDoc, setDoc, onSnapshot, collection, addDoc, query, orderBy, limit } from "https://www.gstatic.com/firebasejs/10.12.0/firebase-firestore.js";

    // ▼▼▼ PEGÁ ACÁ TU firebaseConfig ▼▼▼
    const firebaseConfig = {
      apiKey: "AIzaSyDe6TWoKPOjVc5-boSERJjPfl_JYWiHcgk",
      authDomain: "consultorios-stock.firebaseapp.com",
      projectId: "consultorios-stock",
      storageBucket: "consultorios-stock.firebasestorage.app",
      messagingSenderId: "712455622368",
      appId: "1:712455622368:web:3379df240df0fa25470a85"
    };
    // ▲▲▲ FIN DE CONFIGURACIÓN ▲▲▲

    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    // Exponer al scope global para que el resto del script lo use
    window._db = db;
    window._fbDoc = doc;
    window._fbGetDoc = getDoc;
    window._fbSetDoc = setDoc;
    window._fbOnSnapshot = onSnapshot;
    window._fbCollection = collection;
    window._fbAddDoc = addDoc;
    window._fbQuery = query;
    window._fbOrderBy = orderBy;
    window._fbLimit = limit;
    window._fbReady = true;
    window.dispatchEvent(new Event('firebase-ready'));
  </script>
</head>
<body>

<!-- ══ LOGIN SCREEN ══ -->
<div class="login-screen" id="login-screen">
  <div style="text-align:center;color:white;margin-bottom:4px">
    <div style="font-size:32px">🦷</div>
    <div style="font-size:18px;font-weight:700;margin-top:8px">Consultorio Odontológico</div>
    <div style="font-size:13px;opacity:.7;margin-top:4px">Control de Stock</div>
  </div>
  <div class="login-box">
    <h2>Iniciar sesión</h2>
    <p>Seleccioná tu usuario e ingresá tu PIN</p>
    <div class="user-grid" id="user-grid"></div>
    <div class="pin-wrap" id="pin-wrap" style="display:none">
      <div style="font-size:12px;color:var(--text-s);text-align:center" id="pin-label">Ingresá tu PIN</div>
      <div class="pin-dots" id="pin-dots">
        <div class="pin-dot"></div><div class="pin-dot"></div>
        <div class="pin-dot"></div><div class="pin-dot"></div>
      </div>
      <div class="numpad" id="numpad"></div>
      <div class="login-err" id="login-err"></div>
    </div>
    <button onclick="seleccionarUsuario(null)" style="width:100%;margin-top:4px;font-size:12px;color:var(--text-s)">← Cambiar usuario</button>
  </div>
</div>

<!-- ══ APP ══ -->
<header>
  <div>
    <h1>🦷 Control de Stock — Innova Center</h1>
    <small id="fecha-sub"></small>
  </div>
  <div style="display:flex;align-items:center;gap:10px">
    <div class="user-badge" id="user-badge">
      <div class="user-dot" id="user-dot-header">?</div>
      <span id="user-name-header">—</span>
    </div>
    <button onclick="cerrarSesion()" style="font-size:12px;padding:5px 10px;background:rgba(255,255,255,.15);color:white;border-color:rgba(255,255,255,.3)">Salir</button>
  </div>
</header>

<div class="tabs" id="main-tabs">
  <div class="tab active" onclick="showTab('inventario',this)">📦 Inventario</div>
  <div class="tab" onclick="showTab('prestaciones',this)">🦷 Prestaciones</div>
  <div class="tab" onclick="showTab('historial-tab',this)">📋 Historial</div>
  <div class="tab admin-only" id="tab-admin" onclick="showTab('admin',this)">⚙️ Administración</div>
</div>

<!-- ══ INVENTARIO ══ -->
<div class="page active" id="page-inventario">
  <div class="toolbar">
    <button class="accent" onclick="abrirRegistrar()">🦷 Registrar prestación</button>
    <button onclick="abrirMovimiento(null,'in')">📥 Entrada manual</button>
    <button class="admin-only show" onclick="abrirAgregarMat()">+ Material</button>
    <input type="text" class="search-box" id="buscar-mat" placeholder="Buscar material..." oninput="renderTabla()" style="margin-left:auto">
  </div>
  <div class="stats" id="stats"></div>
  <div class="alert-bar" id="alert-bar"></div>
  <div class="section">
    <h2>Inventario de insumos</h2>
    <div class="table-wrap">
      <table>
        <thead><tr>
          <th>Material / Insumo</th>
          <th style="text-align:center">Stock</th>
          <th style="text-align:center">Mínimo</th>
          <th>Nivel</th>
          <th>Estado</th>
          <th>Vencimiento</th>
          <th>Ubicación</th>
          <th>Acciones</th>
        </tr></thead>
        <tbody id="tabla"></tbody>
      </table>
    </div>
  </div>
  <div class="section">
    <h2>Últimos movimientos</h2>
    <div class="table-wrap"><div class="hist-list" id="hist-mini"></div></div>
  </div>
</div>

<!-- ══ PRESTACIONES ══ -->
<div class="page" id="page-prestaciones">
  <div class="toolbar">
    <button class="accent" onclick="abrirRegistrar()">🦷 Registrar prestación del día</button>
    <button class="admin-only show" onclick="abrirNuevaPrest()">+ Nueva prestación</button>
    <input type="text" class="search-box" id="buscar-prest" placeholder="Buscar prestación..." oninput="renderPrestaciones()">
    <label style="font-size:12px;color:var(--text-s);display:flex;align-items:center;gap:5px;cursor:pointer">
      <input type="checkbox" id="solo-cfg" onchange="renderPrestaciones()"> Solo con insumos
    </label>
  </div>
  <div class="section" style="margin-top:14px">
    <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:8px">
      <h2 style="margin-bottom:0">Prestaciones</h2>
      <span id="prest-count" style="font-size:12px;color:var(--text-s)"></span>
    </div>
    <div id="prest-lista"></div>
  </div>
</div>

<!-- ══ HISTORIAL ══ -->
<div class="page" id="page-historial-tab">
  <div class="toolbar">
    <button onclick="exportCSV()">⬇️ Exportar CSV</button>
    <select id="hist-filtro-user" onchange="renderHistFull()" style="padding:6px 10px;border:1px solid var(--borde);border-radius:6px;font-size:13px">
      <option value="">Todos los usuarios</option>
    </select>
    <button class="admin-only show danger-btn" onclick="if(confirm('¿Borrar todo el historial?')){hist=[];save();renderHistFull();render()}">🗑️ Limpiar</button>
  </div>
  <div class="section" style="margin-top:14px">
    <h2>Todos los movimientos</h2>
    <div class="table-wrap"><div class="hist-list" id="hist-full" style="max-height:520px"></div></div>
  </div>
</div>

<!-- ══ ADMINISTRACIÓN ══ -->
<div class="page" id="page-admin">
  <div class="admin-grid">

    <!-- Usuarios -->
    <div class="admin-card">
      <div class="admin-card-head" style="background:var(--azul)">
        <span style="color:white;font-weight:700;font-size:14px">👤 Usuarios</span>
        <button onclick="abrirNuevoUsuario()" style="font-size:12px;padding:5px 11px;background:white;color:var(--azul);border-color:white">+ Nuevo</button>
      </div>
      <div class="admin-card-body">Gestioná los profesionales y sus PINs. El admin tiene acceso total.</div>
      <div class="admin-list" id="admin-usuarios"></div>
    </div>

    <!-- Insumos -->
    <div class="admin-card">
      <div class="admin-card-head" style="background:var(--azul-m)">
        <span style="color:white;font-weight:700;font-size:14px">📦 Insumos</span>
        <button onclick="abrirAgregarMat()" style="font-size:12px;padding:5px 11px;background:white;color:var(--azul-m);border-color:white">+ Nuevo</button>
      </div>
      <div class="admin-card-body">Editá nombre, stock, mínimo y vencimiento de cada insumo.</div>
      <div class="admin-list" id="admin-insumos"></div>
    </div>

    <!-- Ajuste rápido -->
    <div class="admin-card">
      <div class="admin-card-head" style="background:#2d6a4f">
        <span style="color:white;font-weight:700;font-size:14px">🔧 Ajuste de stock</span>
      </div>
      <div class="admin-card-body">Corregí el stock de cualquier insumo directamente (inventario físico).</div>
      <div style="padding:14px 18px">
        <div class="field"><label>Insumo</label><select id="adj-mat" onchange="previewAdj()" style="width:100%"></select></div>
        <div class="field"><label>Nuevo stock</label><input id="adj-cant" type="number" min="0" step="0.01" oninput="previewAdj()" style="width:100%"></div>
        <div id="adj-preview" style="font-size:12px;color:var(--text-s);margin-bottom:10px;min-height:18px"></div>
        <button class="primary" onclick="confirmarAdj()" style="width:100%">Aplicar ajuste</button>
      </div>
    </div>

    <!-- Respaldo -->
    <div class="admin-card">
      <div class="admin-card-head" style="background:#495057">
        <span style="color:white;font-weight:700;font-size:14px">💾 Respaldo</span>
      </div>
      <div class="admin-card-body">Exportá e importá todos los datos para no perderlos.</div>
      <div style="padding:14px 18px;display:flex;flex-direction:column;gap:8px">
        <button onclick="exportarRespaldo()" style="width:100%">⬇️ Exportar respaldo (.json)</button>
        <label style="width:100%">
          <button onclick="document.getElementById('imp-file').click()" style="width:100%">⬆️ Importar respaldo (.json)</button>
          <input type="file" id="imp-file" accept=".json" style="display:none" onchange="importarRespaldo(this)">
        </label>
        <button onclick="exportCSV()" style="width:100%">📄 Exportar planilla (.csv)</button>
        <button onclick="resetearDatos()" style="width:100%;color:var(--rojo);border-color:var(--rojo-cl)">🗑️ Resetear todos los datos</button>
      </div>
    </div>

  </div>
</div>

<!-- ══ MODALES ══ -->
<!-- Material -->
<div class="overlay" id="modal-mat">
  <div class="modal">
    <h3 id="mat-titulo">Nuevo material</h3>
    <div class="field"><label>Nombre</label><input id="m-nombre" type="text" placeholder="ej: Guantes nitrilo"></div>
    <div class="field"><label>Categoría</label>
      <select id="m-cat">
        <option>General</option><option>Anestesia y cirugía</option><option>Operatoria y resinas</option>
        <option>Endodoncia</option><option>Prótesis y acrílicos</option><option>Ortodoncia</option>
        <option>Prevención</option><option>Instrumental rotatorio</option><option>Implantes</option>
        <option>Esterilización e higiene</option><option>Radiografía</option><option>Varios</option>
      </select>
    </div>
    <div class="field"><label>Stock actual</label><input id="m-stock" type="number" min="0" step="0.01" value="0"></div>
    <div class="field"><label>Stock mínimo (alerta)</label><input id="m-min" type="number" min="0" step="0.01" value="0"></div>
    <div class="field"><label>Fecha de vencimiento (opcional, mes/año)</label><input id="m-venc" type="month"></div>
    <div class="field"><label>Ubicación en el consultorio</label>
      <select id="m-ubic">
        <option value="">-- Sin especificar --</option>
        <option>Mueble de insumos principal</option>
        <option>Cajón operatoria 1</option>
        <option>Cajón operatoria 2</option>
        <option>Cajón operatoria 3</option>
        <option>Heladera</option>
        <option>Depósito / guardado</option>
        <option>Esterilización</option>
        <option>Recepción</option>
        <option>Sala de espera</option>
        <option>Sillón 1</option>
        <option>Sillón 2</option>
        <option>Sillón 3</option>
        <option>Otro</option>
      </select>
    </div>
    <div class="field"><label>Observaciones</label><input id="m-obs" type="text" placeholder="ej: 1 en uso, comprar pronto..."></div>
    <div class="modal-btns">
      <button onclick="cerrar('modal-mat')">Cancelar</button>
      <button class="primary" onclick="guardarMat()">Guardar</button>
    </div>
  </div>
</div>

<!-- Movimiento manual -->
<div class="overlay" id="modal-mov">
  <div class="modal">
    <h3>Registrar movimiento</h3>
    <div class="field"><label>Material</label><select id="mov-mat" style="width:100%"></select></div>
    <div class="field"><label>Tipo</label>
      <select id="mov-tipo">
        <option value="in">📥 Entrada (compra / reposición)</option>
        <option value="out">📤 Salida (consumo / uso)</option>
      </select>
    </div>
    <div class="field"><label>Cantidad</label><input id="mov-cant" type="number" min="0.01" step="0.01" value="1"></div>
    <div class="field"><label>Nota (opcional)</label><input id="mov-nota" type="text"></div>
    <div class="modal-btns">
      <button onclick="cerrar('modal-mov')">Cancelar</button>
      <button class="primary" onclick="confirmarMov()">Confirmar</button>
    </div>
  </div>
</div>

<!-- Configurar insumos de prestación -->
<div class="overlay" id="modal-cfg">
  <div class="modal">
    <h3 id="cfg-titulo">Configurar insumos</h3>
    <div style="font-size:12px;color:var(--text-s);margin-bottom:12px" id="cfg-desc"></div>
    <div style="font-size:11px;font-weight:700;color:var(--text-s);margin-bottom:8px">INSUMOS QUE CONSUME</div>
    <div id="cfg-lines"></div>
    <button onclick="agregarLineaCfg()" style="width:100%;margin-top:4px;color:var(--azul);border-color:var(--azul-cl)">+ Agregar insumo</button>
    <div class="modal-btns">
      <button onclick="cerrar('modal-cfg')">Cancelar</button>
      <button class="primary" onclick="guardarCfg()">Guardar</button>
    </div>
  </div>
</div>

<!-- Registrar prestación -->
<div class="overlay" id="modal-reg">
  <div class="modal">
    <h3>🦷 Registrar prestación</h3>
    <div class="field"><label>Prestación</label>
      <select id="reg-sel" onchange="previewReg()" style="width:100%">
        <option value="">-- Seleccioná --</option>
      </select>
    </div>
    <div class="field"><label>Cantidad de veces</label>
      <input id="reg-cant" type="number" min="1" value="1" oninput="previewReg()">
    </div>
    <div class="field"><label>Paciente / nota (opcional)</label>
      <input id="reg-nota" type="text" placeholder="ej: García, molar inf...">
    </div>
    <div id="reg-preview"></div>
    <div class="modal-btns">
      <button onclick="cerrar('modal-reg')">Cancelar</button>
      <button class="accent" onclick="confirmarReg()">✅ Confirmar y descontar</button>
    </div>
  </div>
</div>

<!-- Nueva prestación -->
<div class="overlay" id="modal-prest">
  <div class="modal">
    <h3 id="prest-titulo">Nueva prestación</h3>
    <div class="field"><label>Nombre</label><input id="p-nombre" type="text" placeholder="ej: Operatoria simple (1 cara)"></div>
    <div class="field"><label>Categoría</label>
      <select id="p-cat">
        <option>Consultas</option><option>Operatoria</option><option>Endodoncia</option>
        <option>Prótesis</option><option>Ortodoncia</option><option>Periodoncia</option>
        <option>Cirugía</option><option>Prevención</option><option>Odontopediatría</option>
        <option>Implantes</option><option>Blanqueamiento</option><option>Otras</option>
      </select>
    </div>
    <div class="field"><label>Duración (opcional)</label><input id="p-dur" type="text" placeholder="ej: 40 minutos"></div>
    <div class="modal-btns">
      <button onclick="cerrar('modal-prest')">Cancelar</button>
      <button class="primary" onclick="guardarPrest()">Guardar</button>
    </div>
  </div>
</div>

<!-- Nuevo usuario -->
<div class="overlay" id="modal-user">
  <div class="modal">
    <h3 id="user-titulo">Nuevo usuario</h3>
    <div class="field"><label>Nombre completo</label><input id="u-nombre" type="text" placeholder="ej: Dra. Paola García"></div>
    <div class="field"><label>Rol</label>
      <select id="u-rol">
        <option value="prof">Profesional</option>
        <option value="admin">Administrador</option>
      </select>
    </div>
    <div class="field"><label>PIN (4 dígitos)</label><input id="u-pin" type="password" maxlength="4" placeholder="****" inputmode="numeric"></div>
    <div class="field"><label>Color</label>
      <select id="u-color">
        <option value="#2563A8">Azul</option><option value="#1A7A4A">Verde</option>
        <option value="#842029">Rojo</option><option value="#4C3494">Violeta</option>
        <option value="#856404">Amarillo</option><option value="#0891b2">Celeste</option>
        <option value="#be185d">Rosa</option><option value="#9a3412">Naranja</option>
      </select>
    </div>
    <div class="modal-btns">
      <button onclick="cerrar('modal-user')">Cancelar</button>
      <button class="primary" onclick="guardarUsuario()">Guardar</button>
    </div>
  </div>
</div>

<script>
// ══════════════════════════════════════════════════════════════════════════════
// DATOS INICIALES
// ══════════════════════════════════════════════════════════════════════════════

const K_MATS='odo_v4_mats', K_HIST='odo_v4_hist', K_CFG='odo_v4_cfg',
      K_PRESTS='odo_v4_prests', K_USERS='odo_v4_users';

// Stock inicial extraído del PDF
const MATS_INIT = [
  {id:1,nombre:'Agua oxigenada 10%',cat:'General',stock:3,minimo:1,venc:null,obs:'1 en uso'},
  {id:2,nombre:'Silicona por condensación Z Plus',cat:'Prótesis y acrílicos',stock:1,minimo:1,venc:'2025-09',obs:'Queda poco'},
  {id:3,nombre:'Silicona liviana Panasil',cat:'Prótesis y acrílicos',stock:4,minimo:2,venc:'2026-02',obs:''},
  {id:4,nombre:'Barbijos x10 blancos',cat:'Esterilización e higiene',stock:5,minimo:2,venc:null,obs:''},
  {id:5,nombre:'Barbijos x10 rosas',cat:'Esterilización e higiene',stock:2,minimo:2,venc:null,obs:''},
  {id:6,nombre:'Compresas x125',cat:'General',stock:1,minimo:1,venc:null,obs:'1 en uso'},
  {id:7,nombre:'Compresas rosas x125',cat:'General',stock:2,minimo:1,venc:null,obs:'1 en uso'},
  {id:8,nombre:'Suctores x100',cat:'General',stock:3,minimo:1,venc:null,obs:'1 en uso'},
  {id:9,nombre:'Algodón 140gr',cat:'General',stock:1,minimo:1,venc:null,obs:''},
  {id:10,nombre:'Vasos descartables x100',cat:'General',stock:29,minimo:5,venc:null,obs:''},
  {id:11,nombre:'Torundas de algodón x50u',cat:'General',stock:17,minimo:5,venc:null,obs:'1 paq x500 nuevo y 1 en uso'},
  {id:12,nombre:'Film para sillón',cat:'Esterilización e higiene',stock:1,minimo:1,venc:null,obs:''},
  {id:13,nombre:'Film para cabezal',cat:'Esterilización e higiene',stock:1,minimo:1,venc:null,obs:''},
  {id:14,nombre:'Gasas x500gr (5x5)',cat:'General',stock:1,minimo:1,venc:null,obs:'En uso'},
  {id:15,nombre:'Gasas grandes',cat:'General',stock:1,minimo:1,venc:null,obs:''},
  {id:16,nombre:'Fijador',cat:'Radiografía',stock:1,minimo:1,venc:'2028-03',obs:''},
  {id:17,nombre:'Revelador',cat:'Radiografía',stock:1,minimo:1,venc:'2028-03',obs:''},
  {id:18,nombre:'Suturas de nylon 4.0 x12',cat:'Anestesia y cirugía',stock:1,minimo:1,venc:null,obs:'10u'},
  {id:19,nombre:'Anestubos Totalcaína',cat:'Anestesia y cirugía',stock:20,minimo:10,venc:'2026-11',obs:''},
  {id:20,nombre:'Ácido fosfórico 35% Densell',cat:'Operatoria y resinas',stock:1,minimo:1,venc:'2028-02',obs:''},
  {id:21,nombre:'Ácido fosfórico 35% Klepp',cat:'Operatoria y resinas',stock:3,minimo:1,venc:'2025-09',obs:''},
  {id:22,nombre:'Cubeta para topicación fluor niños',cat:'Prevención',stock:1,minimo:1,venc:null,obs:''},
  {id:23,nombre:'Radiografías periapicales adulto x100',cat:'Radiografía',stock:1,minimo:1,venc:null,obs:''},
  {id:24,nombre:'Radiografías periapicales niños x100',cat:'Radiografía',stock:1,minimo:1,venc:null,obs:'En uso'},
  {id:25,nombre:'Agujas 21mm cortas x100',cat:'Anestesia y cirugía',stock:1,minimo:1,venc:null,obs:'En uso'},
  {id:26,nombre:'Agujas 12mm extra cortas x100',cat:'Anestesia y cirugía',stock:1,minimo:1,venc:null,obs:'En uso'},
  {id:27,nombre:'Papel de articular',cat:'General',stock:9,minimo:2,venc:null,obs:'9 libros'},
  {id:28,nombre:'Tiras de acetato x100',cat:'Operatoria y resinas',stock:1,minimo:1,venc:null,obs:'En uso'},
  {id:29,nombre:'Tiras de pulido de acero x12',cat:'Instrumental rotatorio',stock:1,minimo:1,venc:null,obs:''},
  {id:30,nombre:'Tiras de pulido resina x150',cat:'Instrumental rotatorio',stock:1,minimo:1,venc:null,obs:''},
  {id:31,nombre:'Brochas para profilaxis x100',cat:'Prevención',stock:1,minimo:1,venc:null,obs:'67u'},
  {id:32,nombre:'Vaselina sólida',cat:'General',stock:2,minimo:1,venc:'2025-01',obs:''},
  {id:33,nombre:'Vaselina líquida',cat:'General',stock:1,minimo:1,venc:null,obs:'Sin fecha de vto'},
  {id:34,nombre:'Hoja de bisturí N°11',cat:'Anestesia y cirugía',stock:29,minimo:5,venc:null,obs:''},
  {id:35,nombre:'Hoja de bisturí N°15',cat:'Anestesia y cirugía',stock:14,minimo:5,venc:null,obs:''},
  {id:36,nombre:'Dycal',cat:'Operatoria y resinas',stock:2,minimo:1,venc:'2025-05',obs:''},
  {id:37,nombre:'Adhesivo Megabond',cat:'Operatoria y resinas',stock:1,minimo:1,venc:'2025-08',obs:''},
  {id:38,nombre:'Pastillas evidenciadoras de placa',cat:'Prevención',stock:4,minimo:1,venc:null,obs:''},
  {id:39,nombre:'Resina Ultrafill A1',cat:'Operatoria y resinas',stock:1,minimo:1,venc:'2026-10',obs:''},
  {id:40,nombre:'Resina Ultrafill A2',cat:'Operatoria y resinas',stock:4,minimo:2,venc:'2028-02',obs:''},
  {id:41,nombre:'Resina Ultrafill A3',cat:'Operatoria y resinas',stock:4,minimo:2,venc:'2028-06',obs:''},
  {id:42,nombre:'Resina Ultrafill A3.5',cat:'Operatoria y resinas',stock:2,minimo:1,venc:'2028-06',obs:''},
  {id:43,nombre:'Resina Ultrafill A4',cat:'Operatoria y resinas',stock:1,minimo:1,venc:'2027-04',obs:''},
  {id:44,nombre:'Resina Ultrafill OA2',cat:'Operatoria y resinas',stock:5,minimo:2,venc:'2027-03',obs:''},
  {id:45,nombre:'Resina Ultrafill OA3',cat:'Operatoria y resinas',stock:2,minimo:1,venc:'2027-07',obs:''},
  {id:46,nombre:'Ultraflow A3',cat:'Operatoria y resinas',stock:2,minimo:1,venc:'2028-06',obs:''},
  {id:47,nombre:'Ultraflow A2',cat:'Operatoria y resinas',stock:0,minimo:1,venc:null,obs:'Sin stock'},
  {id:48,nombre:'Sellador de F.S. y F. fotopolimerizable',cat:'Prevención',stock:1,minimo:1,venc:'2027-08',obs:''},
  {id:49,nombre:'Barrera gingival',cat:'Operatoria y resinas',stock:2,minimo:1,venc:'2026-02',obs:''},
  {id:50,nombre:'Microbrush chico',cat:'General',stock:3,minimo:1,venc:null,obs:''},
  {id:51,nombre:'Microbrush mediano',cat:'General',stock:2,minimo:1,venc:null,obs:''},
  {id:52,nombre:'Transbond',cat:'Ortodoncia',stock:1,minimo:1,venc:'2027-04',obs:''},
  {id:53,nombre:'Placas 0.04',cat:'Ortodoncia',stock:8,minimo:2,venc:null,obs:''},
  {id:54,nombre:'Placas blandas 0.06 blanqueamiento',cat:'Ortodoncia',stock:2,minimo:1,venc:null,obs:''},
  {id:55,nombre:'Placas rígidas 0.06',cat:'Ortodoncia',stock:7,minimo:2,venc:null,obs:''},
  {id:56,nombre:'Placas rígidas 0.08',cat:'Ortodoncia',stock:20,minimo:5,venc:null,obs:''},
  {id:57,nombre:'Placas rígidas rojo',cat:'Ortodoncia',stock:7,minimo:2,venc:null,obs:''},
  {id:58,nombre:'Alcohol 70% 500ml',cat:'Esterilización e higiene',stock:0,minimo:2,venc:null,obs:'Sin stock'},
  {id:59,nombre:'Alcohol 96% 1lt',cat:'Esterilización e higiene',stock:4,minimo:1,venc:null,obs:'1 en uso'},
  {id:60,nombre:'Detergente bienzimático',cat:'Esterilización e higiene',stock:2,minimo:1,venc:null,obs:'1 en uso'},
  {id:61,nombre:'Iodopovidona 500ml',cat:'Esterilización e higiene',stock:2,minimo:1,venc:null,obs:'En uso'},
  {id:62,nombre:'Agua destilada',cat:'General',stock:1,minimo:1,venc:null,obs:'Le queda poco'},
  {id:63,nombre:'Jeringas 1ml',cat:'General',stock:26,minimo:10,venc:null,obs:''},
  {id:64,nombre:'Jeringas 5ml',cat:'General',stock:73,minimo:10,venc:null,obs:''},
  {id:65,nombre:'Jeringas 10ml',cat:'General',stock:89,minimo:10,venc:null,obs:''},
  {id:66,nombre:'Agujas hipodérmicas marrón',cat:'General',stock:71,minimo:10,venc:null,obs:''},
  {id:67,nombre:'Agujas hipodérmicas verde',cat:'General',stock:3,minimo:5,venc:null,obs:''},
  {id:68,nombre:'Kit ortodoncia GUM',cat:'Ortodoncia',stock:3,minimo:1,venc:null,obs:''},
  {id:69,nombre:'Alginato',cat:'Prótesis y acrílicos',stock:2,minimo:1,venc:'2030-02',obs:''},
  {id:70,nombre:'Guantes de latex XS nitrilo',cat:'Esterilización e higiene',stock:6,minimo:2,venc:null,obs:''},
  {id:71,nombre:'Guantes de latex M',cat:'Esterilización e higiene',stock:1,minimo:2,venc:null,obs:''},
  {id:72,nombre:'Guantes de latex M nitrilo',cat:'Esterilización e higiene',stock:1,minimo:2,venc:null,obs:''},
  {id:73,nombre:'Goma dique Blue Santuary',cat:'Endodoncia',stock:1,minimo:1,venc:null,obs:'En uso'},
  {id:74,nombre:'Yeso Densita',cat:'Prótesis y acrílicos',stock:1,minimo:1,venc:null,obs:''},
  {id:75,nombre:'Yeso piedra',cat:'Prótesis y acrílicos',stock:17,minimo:3,venc:null,obs:''},
  {id:76,nombre:'Cuñas de madera x100',cat:'Operatoria y resinas',stock:1,minimo:1,venc:null,obs:''},
  {id:77,nombre:'Resina Camaleónica Kit',cat:'Operatoria y resinas',stock:1,minimo:1,venc:'2027-03',obs:''},
  {id:78,nombre:'Lidocaína',cat:'Anestesia y cirugía',stock:1,minimo:1,venc:'2028-05',obs:''},
  {id:79,nombre:'Fluor en gel neutro Densell',cat:'Prevención',stock:2,minimo:1,venc:'2024-06',obs:''},
  {id:80,nombre:'Fluor en gel neutro Tedequim',cat:'Prevención',stock:1,minimo:1,venc:null,obs:''},
  {id:81,nombre:'Fluor en gel acidulado Densell',cat:'Prevención',stock:2,minimo:1,venc:null,obs:'Uno en uso'},
  {id:82,nombre:'Fluoruro diamino de plata',cat:'Prevención',stock:1,minimo:1,venc:'2024-07',obs:''},
  {id:83,nombre:'Iodoformo Tedequim',cat:'Endodoncia',stock:1,minimo:1,venc:'2028-03',obs:''},
  {id:84,nombre:'Iodoformo Egeo',cat:'Endodoncia',stock:1,minimo:1,venc:'2027-02',obs:'En uso'},
  {id:85,nombre:'Formocresol',cat:'Odontopediatría',stock:4,minimo:1,venc:'2021-04',obs:'Vencido'},
  {id:86,nombre:'Barniz fluoruro de sodio 5%',cat:'Prevención',stock:1,minimo:1,venc:null,obs:'Sin fecha'},
  {id:87,nombre:'Flourogel',cat:'Prevención',stock:1,minimo:1,venc:'2025-04',obs:''},
  {id:88,nombre:'Hidróxido de calcio',cat:'Endodoncia',stock:2,minimo:1,venc:'2019-05',obs:''},
  {id:89,nombre:'Pasta tri antibiótica / Trimix',cat:'Endodoncia',stock:2,minimo:1,venc:'2027-03',obs:''},
  {id:90,nombre:'Pasta lentamente reabsorbible Maisto',cat:'Endodoncia',stock:1,minimo:1,venc:'2028-03',obs:''},
  {id:91,nombre:'Hipoclorito 2.5%',cat:'Endodoncia',stock:1,minimo:1,venc:null,obs:'Preparado en consul'},
  {id:92,nombre:'Kit blanqueamiento Pola Office',cat:'Blanqueamiento',stock:1,minimo:1,venc:'2027-05',obs:'Líquido 07/26 polvo 05/27'},
  {id:93,nombre:'Blanqueamiento ambulatorio 10%',cat:'Blanqueamiento',stock:9,minimo:2,venc:'2027-07',obs:''},
  {id:94,nombre:'Clarident microabrasión',cat:'Blanqueamiento',stock:1,minimo:1,venc:'2024-10',obs:''},
  {id:95,nombre:'Endo Ice Klepp',cat:'Endodoncia',stock:2,minimo:1,venc:null,obs:'En uso'},
  {id:96,nombre:'Z Prime',cat:'Prótesis y acrílicos',stock:1,minimo:1,venc:'2027-09',obs:''},
  {id:97,nombre:'IRM',cat:'Endodoncia',stock:2,minimo:1,venc:'2025-09',obs:''},
  {id:98,nombre:'Ionómero V Tipo 1 Ionomax',cat:'Operatoria y resinas',stock:2,minimo:1,venc:'2025-01',obs:'Uno en uso'},
  {id:99,nombre:'Ionómero V Tipo 2 Ionomax',cat:'Operatoria y resinas',stock:2,minimo:1,venc:'2026-03',obs:''},
  {id:100,nombre:'Ionómero V Tipo 2 Klepp',cat:'Operatoria y resinas',stock:2,minimo:1,venc:'2027-04',obs:''},
  {id:101,nombre:'Endoseal',cat:'Endodoncia',stock:2,minimo:1,venc:'2028-09',obs:''},
  {id:102,nombre:'Cemento Dual All Cem 2',cat:'Prótesis y acrílicos',stock:1,minimo:1,venc:'2027-06',obs:'En uso'},
  {id:103,nombre:'Cemento fosfato de zinc',cat:'Prótesis y acrílicos',stock:1,minimo:1,venc:'2027-06',obs:''},
  {id:104,nombre:'Liner base revestimiento para cavidades',cat:'Operatoria y resinas',stock:2,minimo:1,venc:'2026-07',obs:''},
  {id:105,nombre:'Polvo para profilaxis 100gr Tedequim',cat:'Prevención',stock:2,minimo:1,venc:'2028-05',obs:''},
  {id:106,nombre:'Banda de fibra de vidrio Vactrise',cat:'Operatoria y resinas',stock:2,minimo:1,venc:null,obs:'Una en uso'},
  {id:107,nombre:'Mandril',cat:'Instrumental rotatorio',stock:17,minimo:3,venc:null,obs:''},
  {id:108,nombre:'Discos de pulido morado',cat:'Instrumental rotatorio',stock:9,minimo:2,venc:null,obs:''},
  {id:109,nombre:'Postes de fibra de vidrio x5',cat:'Endodoncia',stock:1,minimo:1,venc:null,obs:''},
  {id:110,nombre:'Postes de fibra de vidrio x100 rojo',cat:'Endodoncia',stock:1,minimo:1,venc:null,obs:''},
  {id:111,nombre:'Postes de fibra de vidrio x100 amarillo',cat:'Endodoncia',stock:1,minimo:1,venc:null,obs:''},
  {id:112,nombre:'Separadores molares verde agua',cat:'Ortodoncia',stock:14,minimo:3,venc:null,obs:''},
  {id:113,nombre:'Separadores interdentales verde',cat:'Ortodoncia',stock:18,minimo:3,venc:null,obs:'1 puesto'},
  {id:114,nombre:'Conos de gutapercha principales 30',cat:'Endodoncia',stock:5,minimo:2,venc:null,obs:''},
  {id:115,nombre:'Conos de gutapercha principales 35',cat:'Endodoncia',stock:11,minimo:2,venc:null,obs:''},
  {id:116,nombre:'Conos de gutapercha accesorios 30',cat:'Endodoncia',stock:10,minimo:2,venc:null,obs:''},
  {id:117,nombre:'Conos de gutapercha accesorios 35',cat:'Endodoncia',stock:3,minimo:2,venc:null,obs:''},
  {id:118,nombre:'Conos de papel 15-25',cat:'Endodoncia',stock:2,minimo:1,venc:null,obs:''},
  {id:119,nombre:'Conos de papel 15-30',cat:'Endodoncia',stock:1,minimo:1,venc:null,obs:''},
  {id:120,nombre:'MTA',cat:'Endodoncia',stock:1,minimo:1,venc:null,obs:'Abierto'},
  {id:121,nombre:'Abrebocas adultos',cat:'General',stock:21,minimo:3,venc:null,obs:''},
  {id:122,nombre:'Abrebocas niños',cat:'General',stock:5,minimo:2,venc:null,obs:''},
  {id:123,nombre:'Cubetas parciales',cat:'Prótesis y acrílicos',stock:20,minimo:3,venc:null,obs:''},
  {id:124,nombre:'Cubetas rimlock',cat:'Prótesis y acrílicos',stock:20,minimo:3,venc:null,obs:''},
  {id:125,nombre:'Cubetas 5/6',cat:'Prótesis y acrílicos',stock:53,minimo:5,venc:null,obs:''},
  {id:126,nombre:'Cubetas 3/4',cat:'Prótesis y acrílicos',stock:36,minimo:5,venc:null,obs:''},
  {id:127,nombre:'Cubetas 1/2',cat:'Prótesis y acrílicos',stock:55,minimo:5,venc:null,obs:''},
  {id:128,nombre:'Monómero x500',cat:'Prótesis y acrílicos',stock:2,minimo:1,venc:'2027-11',obs:''},
  {id:129,nombre:'Acrílico rosa auto 100gr',cat:'Prótesis y acrílicos',stock:1,minimo:1,venc:null,obs:''},
  {id:130,nombre:'Acrílico diente 66 coronas y puentes x100gr',cat:'Prótesis y acrílicos',stock:1,minimo:1,venc:'2027-03',obs:'En uso'},
  {id:131,nombre:'Cubrecamillas 38',cat:'Esterilización e higiene',stock:30,minimo:5,venc:null,obs:''},
  {id:132,nombre:'Batas',cat:'Esterilización e higiene',stock:17,minimo:3,venc:null,obs:''},
  {id:133,nombre:'Cofias',cat:'Esterilización e higiene',stock:24,minimo:5,venc:null,obs:''},
  {id:134,nombre:'Campo para paciente',cat:'Esterilización e higiene',stock:19,minimo:3,venc:null,obs:''},
  // Implantes
  {id:135,nombre:'Membrana reabsorbible colágeno SUS-MEM 1.5x2cm',cat:'Implantes',stock:8,minimo:2,venc:'2026-07',obs:'TISSUM'},
  {id:136,nombre:'Matriz ósea SUS-OSS 0.5g',cat:'Implantes',stock:2,minimo:1,venc:'2029-01',obs:'TISSUM'},
  {id:137,nombre:'Hidroxiapatita BOS-HA 1.0g',cat:'Implantes',stock:1,minimo:1,venc:'2028-03',obs:'TISSUM'},
  {id:138,nombre:'Hidroxiapatita BOS-HA 0.5g',cat:'Implantes',stock:3,minimo:1,venc:'2028-08',obs:'TISSUM'},
  {id:139,nombre:'Implante SIMPLE HI 3.3x8.5 Tree Oss',cat:'Implantes',stock:10,minimo:2,venc:'2030-01',obs:''},
  {id:140,nombre:'Implante SIMPLE HI 3.3x10 Tree Oss',cat:'Implantes',stock:12,minimo:2,venc:'2029-12',obs:''},
  {id:141,nombre:'Implante SIMPLE HI 3.3x11.5 Tree Oss',cat:'Implantes',stock:11,minimo:2,venc:'2029-09',obs:''},
  {id:142,nombre:'Implante SIMPLE HI 3.3x13 Tree Oss',cat:'Implantes',stock:5,minimo:1,venc:'2029-09',obs:''},
  {id:143,nombre:'Implante HS 3.7x10 Tree Oss',cat:'Implantes',stock:4,minimo:1,venc:'2028-10',obs:''},
  {id:144,nombre:'Implante HS 3.7x11.5 Tree Oss',cat:'Implantes',stock:1,minimo:1,venc:'2028-07',obs:''},
  {id:145,nombre:'Implante HS 3.7x13 Tree Oss',cat:'Implantes',stock:14,minimo:2,venc:'2029-01',obs:''},
  {id:146,nombre:'Implante HS 4.3x8.5 Tree Oss',cat:'Implantes',stock:7,minimo:1,venc:'2028-10',obs:''},
  // Ortodoncia - arcos
  {id:147,nombre:'Arco 0.12 NITI SUP',cat:'Ortodoncia',stock:2,minimo:1,venc:null,obs:'Sobres x10'},
  {id:148,nombre:'Arco 0.14 NITI SUP',cat:'Ortodoncia',stock:39,minimo:5,venc:null,obs:''},
  {id:149,nombre:'Arco 0.14 NITI INF',cat:'Ortodoncia',stock:15,minimo:5,venc:null,obs:''},
  {id:150,nombre:'Arco 0.16 NITI SUP',cat:'Ortodoncia',stock:2,minimo:1,venc:null,obs:''},
  {id:151,nombre:'Arco 0.16 NITI INF',cat:'Ortodoncia',stock:2,minimo:1,venc:null,obs:''},
  {id:152,nombre:'Arco 0.18 NITI SUP',cat:'Ortodoncia',stock:4,minimo:1,venc:null,obs:''},
  {id:153,nombre:'Arco 0.18 NITI INF',cat:'Ortodoncia',stock:8,minimo:2,venc:null,obs:''},
  {id:154,nombre:'Arco 0.20 NITI SUP',cat:'Ortodoncia',stock:13,minimo:3,venc:null,obs:''},
  {id:155,nombre:'Arco 0.20 NITI INF',cat:'Ortodoncia',stock:12,minimo:3,venc:null,obs:''},
  {id:156,nombre:'Arco 0.18 ACERO INF',cat:'Ortodoncia',stock:26,minimo:5,venc:null,obs:''},
  {id:157,nombre:'Arco 17x25 NITI SUP',cat:'Ortodoncia',stock:20,minimo:3,venc:null,obs:''},
  {id:158,nombre:'Casos ortodoncia cerámica',cat:'Ortodoncia',stock:16,minimo:2,venc:null,obs:''},
  {id:159,nombre:'Casos ortodoncia metálicos',cat:'Ortodoncia',stock:66,minimo:5,venc:null,obs:''},
  {id:160,nombre:'Tubos 16 x10u',cat:'Ortodoncia',stock:8,minimo:2,venc:null,obs:''},
  {id:161,nombre:'Tubos 26 x10u',cat:'Ortodoncia',stock:9,minimo:2,venc:null,obs:''},
  {id:162,nombre:'Tubos 36 x10u',cat:'Ortodoncia',stock:9,minimo:2,venc:null,obs:''},
  {id:163,nombre:'Tubos 46 x10u',cat:'Ortodoncia',stock:6,minimo:2,venc:null,obs:''},
  {id:164,nombre:'Gomas interdentales 1.8" Medium Morelli 1000u',cat:'Ortodoncia',stock:1,minimo:1,venc:null,obs:'En uso'},
  {id:165,nombre:'Gomas Heavy Jaguar 1.8"',cat:'Ortodoncia',stock:15,minimo:3,venc:null,obs:''},
  {id:166,nombre:'Cadena larga azul 1.5m',cat:'Ortodoncia',stock:1,minimo:1,venc:null,obs:'Rollo cerrado'},
  {id:167,nombre:'Cadena media naranja 1.5m',cat:'Ortodoncia',stock:1,minimo:1,venc:null,obs:'Rollo abierto'},
  {id:168,nombre:'Cemento de ortodoncia Fix',cat:'Ortodoncia',stock:8,minimo:2,venc:null,obs:''},
  {id:169,nombre:'Bloc Sealer',cat:'Endodoncia',stock:1,minimo:1,venc:null,obs:''},
  {id:170,nombre:'Separador de acrílico 250ml',cat:'Prótesis y acrílicos',stock:2,minimo:1,venc:null,obs:''},
  {id:171,nombre:'Material de rebase 40ml',cat:'Prótesis y acrílicos',stock:1,minimo:1,venc:null,obs:'Queda menos de la mitad'},
  {id:172,nombre:'Hilo retractor 000',cat:'Prótesis y acrílicos',stock:2,minimo:1,venc:null,obs:''},
  {id:173,nombre:'Silano',cat:'Prótesis y acrílicos',stock:2,minimo:1,venc:'2028-05',obs:''},
  {id:174,nombre:'Solución fisiológica',cat:'Anestesia y cirugía',stock:1,minimo:1,venc:null,obs:''},
];

// Prestaciones extraídas del PDF (lista propia del consultorio)
const PRESTS_INIT = [
  {id:1,nombre:'Activación de resortes',cat:'Ortodoncia',dur:'15 min'},
  {id:2,nombre:'Agregado de diente en consultorio',cat:'Prótesis',dur:'35 min'},
  {id:3,nombre:'Agregado de retenedor en consultorio',cat:'Prótesis',dur:'35 min'},
  {id:4,nombre:'Ajuste de corona sobre implante',cat:'Implantes',dur:'45-60 min'},
  {id:5,nombre:'Alivio del dolor',cat:'Consultas',dur:'60 min'},
  {id:6,nombre:'Ateneo (plan de acción)',cat:'Consultas',dur:'15 min'},
  {id:7,nombre:'Blanqueamiento (sesión de control)',cat:'Blanqueamiento',dur:'20 min'},
  {id:8,nombre:'Blanqueamiento ambulatorio (confección)',cat:'Blanqueamiento',dur:'45 min'},
  {id:9,nombre:'Blanqueamiento en consultorio',cat:'Blanqueamiento',dur:'90 min'},
  {id:10,nombre:'Cambio de cadena continua',cat:'Ortodoncia',dur:'15 min'},
  {id:11,nombre:'Carilla de resina directa',cat:'Operatoria',dur:'60 min'},
  {id:12,nombre:'Carillas PMMA (cementado)',cat:'Prótesis',dur:'45 min'},
  {id:13,nombre:'Carillas PMMA (tallado y provisorio)',cat:'Prótesis',dur:'90 min'},
  {id:14,nombre:'Carillas porcelana (cementado)',cat:'Prótesis',dur:'30 min'},
  {id:15,nombre:'Carillas porcelana (tallado y provisorio)',cat:'Prótesis',dur:'70 min'},
  {id:16,nombre:'Cementado de brackets',cat:'Ortodoncia',dur:'60 min'},
  {id:17,nombre:'Certificado bucodental',cat:'Consultas',dur:'30 min'},
  {id:18,nombre:'Cirugía de implantes',cat:'Implantes',dur:'120 min'},
  {id:19,nombre:'Cirugía de liberación para ortodoncia',cat:'Cirugía',dur:'40 min'},
  {id:20,nombre:'Cirugía de tercer molar retenido',cat:'Cirugía',dur:'120 min'},
  {id:21,nombre:'Colocación de cicatrizales',cat:'Implantes',dur:'30 min'},
  {id:22,nombre:'Compostura de prótesis removible',cat:'Prótesis',dur:'45 min'},
  {id:23,nombre:'Conservación alveolar (exo + ROG)',cat:'Cirugía',dur:'60 min'},
  {id:24,nombre:'Consulta de implantes',cat:'Implantes',dur:'30 min'},
  {id:25,nombre:'Consulta de urgencia',cat:'Consultas',dur:'20 min'},
  {id:26,nombre:'Consulta especialista',cat:'Consultas',dur:'30 min'},
  {id:27,nombre:'Consulta prótesis',cat:'Prótesis',dur:'30 min'},
  {id:28,nombre:'Contención de ortodoncia fija',cat:'Ortodoncia',dur:'45 min'},
  {id:29,nombre:'Control de implantes',cat:'Implantes',dur:'15 min'},
  {id:30,nombre:'Control de ortodoncia Bianca',cat:'Ortodoncia',dur:'70 min'},
  {id:31,nombre:'Control de ortodoncia Paula',cat:'Ortodoncia',dur:'30 min'},
  {id:32,nombre:'Control de ortopedia',cat:'Ortodoncia',dur:'30 min'},
  {id:33,nombre:'Control de prótesis',cat:'Prótesis',dur:'15 min'},
  {id:34,nombre:'Control ortopedia',cat:'Ortodoncia',dur:'30 min'},
  {id:35,nombre:'Control prótesis/puente adhesivo',cat:'Prótesis',dur:'30 min'},
  {id:36,nombre:'Control traumatismo',cat:'Consultas',dur:'25 min'},
  {id:37,nombre:'Corona metalocerámica (impresión)',cat:'Prótesis',dur:'90 min'},
  {id:38,nombre:'Corona metalocerámica (instalación)',cat:'Prótesis',dur:'30 min'},
  {id:39,nombre:'Corona PMMA (impresión)',cat:'Prótesis',dur:'60 min'},
  {id:40,nombre:'Corona PMMA (instalación)',cat:'Prótesis',dur:'40 min'},
  {id:41,nombre:'Corona porcelana/zirconio (cementado)',cat:'Prótesis',dur:'30 min'},
  {id:42,nombre:'Corona porcelana/zirconio (impresión)',cat:'Prótesis',dur:'90 min'},
  {id:43,nombre:'Cubeta individual (confección)',cat:'Prótesis',dur:'30 min'},
  {id:44,nombre:'Derivación',cat:'Consultas',dur:'30 min'},
  {id:45,nombre:'Elevación de piso de seno maxilar',cat:'Implantes',dur:'90 min'},
  {id:46,nombre:'Entrega de prótesis (post reparación)',cat:'Prótesis',dur:'30 min'},
  {id:47,nombre:'Extracción compleja (con colgajo)',cat:'Cirugía',dur:'45 min'},
  {id:48,nombre:'Extracción en retención mucosa',cat:'Cirugía',dur:'120 min'},
  {id:49,nombre:'Extracción en retención ósea',cat:'Cirugía',dur:'140 min'},
  {id:50,nombre:'Extracción simple',cat:'Cirugía',dur:'40 min'},
  {id:51,nombre:'Férula periodontal',cat:'Periodoncia',dur:'35 min'},
  {id:52,nombre:'Fluor en adultos (cubeta)',cat:'Prevención',dur:'20 min'},
  {id:53,nombre:'Impresión sobre implantes',cat:'Implantes',dur:'60 min'},
  {id:54,nombre:'Incrustación (cementado)',cat:'Operatoria',dur:'45 min'},
  {id:55,nombre:'Incrustación (tallado)',cat:'Operatoria',dur:'60 min'},
  {id:56,nombre:'Instalación contención removible',cat:'Ortodoncia',dur:'15 min'},
  {id:57,nombre:'Instalación de ortopedia',cat:'Ortodoncia',dur:'30 min'},
  {id:58,nombre:'Instalación de prótesis',cat:'Prótesis',dur:'30 min'},
  {id:59,nombre:'Limpieza boca completa',cat:'Prevención',dur:'20 min'},
  {id:60,nombre:'Microabrasión',cat:'Operatoria',dur:'40 min'},
  {id:61,nombre:'Mockup por sector',cat:'Prótesis',dur:'50 min'},
  {id:62,nombre:'Niños biopulpectomía no vital',cat:'Odontopediatría',dur:'60 min'},
  {id:63,nombre:'Niños biopulpectomía vital',cat:'Odontopediatría',dur:'60 min'},
  {id:64,nombre:'Niños cariostático x sesión',cat:'Odontopediatría',dur:'20 min'},
  {id:65,nombre:'Niños consulta',cat:'Odontopediatría',dur:'30 min'},
  {id:66,nombre:'Niños corona estampada (instalación)',cat:'Odontopediatría',dur:'30 min'},
  {id:67,nombre:'Niños corona estampada (toma de impresión)',cat:'Odontopediatría',dur:'40 min'},
  {id:68,nombre:'Niños extracción de elemento temporario',cat:'Odontopediatría',dur:'35 min'},
  {id:69,nombre:'Niños inactivación de caries (IRM)',cat:'Odontopediatría',dur:'35 min'},
  {id:70,nombre:'Niños limpieza y técnica de cepillado',cat:'Odontopediatría',dur:'45 min'},
  {id:71,nombre:'Niños mantenedor de espacio (instalación)',cat:'Odontopediatría',dur:'30 min'},
  {id:72,nombre:'Niños mantenedor de espacio (toma de impresión)',cat:'Odontopediatría',dur:'55 min'},
  {id:73,nombre:'Niños operatoria res/iv',cat:'Odontopediatría',dur:'60 min'},
  {id:74,nombre:'Niños plano inclinado',cat:'Odontopediatría',dur:'60 min'},
  {id:75,nombre:'Niños protección pulpar directa',cat:'Odontopediatría',dur:'35 min'},
  {id:76,nombre:'Niños topicación de fluor',cat:'Odontopediatría',dur:'45 min'},
  {id:77,nombre:'Operatoria compuesta (2 caras)',cat:'Operatoria',dur:'35 min'},
  {id:78,nombre:'Operatoria compuesta (3 caras)',cat:'Operatoria',dur:'45 min'},
  {id:79,nombre:'Operatoria simple (1 cara)',cat:'Operatoria',dur:'40 min'},
  {id:80,nombre:'Ortopedia (instalación aparatología)',cat:'Ortodoncia',dur:'30 min'},
  {id:81,nombre:'Ortopedia (toma de impresión)',cat:'Ortodoncia',dur:'45 min'},
  {id:82,nombre:'Pasta provisoria / IRM (en garantía)',cat:'Operatoria',dur:'20 min'},
  {id:83,nombre:'Perno bola (cementado)',cat:'Prótesis',dur:'5 min'},
  {id:84,nombre:'Perno bola (toma de impresión)',cat:'Prótesis',dur:'60 min'},
  {id:85,nombre:'Perno de fibra de vidrio',cat:'Operatoria',dur:'40 min'},
  {id:86,nombre:'PFV + corona (impresión)',cat:'Prótesis',dur:'30 min'},
  {id:87,nombre:'Piercing dental',cat:'Otras',dur:'30 min'},
  {id:88,nombre:'Placa de contención',cat:'Ortodoncia',dur:'30 min'},
  {id:89,nombre:'Placa miorrelajante (instalación)',cat:'Prótesis',dur:'30 min'},
  {id:90,nombre:'Placa miorrelajante (toma de impresión)',cat:'Prótesis',dur:'30 min'},
  {id:91,nombre:'Placa termoformada (vacuform instalación)',cat:'Ortodoncia',dur:'30 min'},
  {id:92,nombre:'Placa termoformada (vacuform)',cat:'Ortodoncia',dur:'35 min'},
  {id:93,nombre:'Primera consulta',cat:'Consultas',dur:'30 min'},
  {id:94,nombre:'Prot. completa (impresión)',cat:'Prótesis',dur:'20 min'},
  {id:95,nombre:'Prot. completa (instalación)',cat:'Prótesis',dur:'20 min'},
  {id:96,nombre:'Prot. completa (prueba de enfilado)',cat:'Prótesis',dur:'20 min'},
  {id:97,nombre:'Prot. completa (prueba de rodete)',cat:'Prótesis',dur:'25 min'},
  {id:98,nombre:'Prot. cromo cobalto (instalación)',cat:'Prótesis',dur:'20 min'},
  {id:99,nombre:'Prot. cromo cobalto (prueba armazón)',cat:'Prótesis',dur:'30 min'},
  {id:100,nombre:'Prot. cromo cobalto (prueba de enfilado)',cat:'Prótesis',dur:'30 min'},
  {id:101,nombre:'Prot. cromo cobalto (toma de impresión)',cat:'Prótesis',dur:'45 min'},
  {id:102,nombre:'Prot. parcial removible (instalación)',cat:'Prótesis',dur:'15 min'},
  {id:103,nombre:'Prot. parcial removible (prueba de enfilado)',cat:'Prótesis',dur:'30 min'},
  {id:104,nombre:'Prot. parcial removible (prueba de rodete)',cat:'Prótesis',dur:'30 min'},
  {id:105,nombre:'Prot. parcial removible (toma de impresión)',cat:'Prótesis',dur:'30 min'},
  {id:106,nombre:'Prótesis híbrida (instalación)',cat:'Implantes',dur:'30 min'},
  {id:107,nombre:'Prótesis híbrida (prueba armazón y enfilado)',cat:'Implantes',dur:'60 min'},
  {id:108,nombre:'Prótesis híbrida (prueba de enfilado)',cat:'Implantes',dur:'50 min'},
  {id:109,nombre:'Prótesis híbrida (toma de impresión)',cat:'Implantes',dur:'70 min'},
  {id:110,nombre:'Provisorio de acrílico (en consultorio)',cat:'Prótesis',dur:'90 min'},
  {id:111,nombre:'Provisorio de acrílico en protesista (tallado)',cat:'Prótesis',dur:'50 min'},
  {id:112,nombre:'Prueba de enfilado',cat:'Prótesis',dur:'30 min'},
  {id:113,nombre:'Prueba de rodete',cat:'Prótesis',dur:'30 min'},
  {id:114,nombre:'Puente adhesivo de 1 elemento',cat:'Prótesis',dur:'50 min'},
  {id:115,nombre:'Puente adhesivo de 2 o más elementos',cat:'Prótesis',dur:'90 min'},
  {id:116,nombre:'Radiografía periapical',cat:'Diagnóstico',dur:'15 min'},
  {id:117,nombre:'Raspaje y alisado por sector (manual)',cat:'Periodoncia',dur:'45 min'},
  {id:118,nombre:'Rebasado de prótesis (en consultorio)',cat:'Prótesis',dur:'20 min'},
  {id:119,nombre:'Rebasado en laboratorio (toma de impresión)',cat:'Prótesis',dur:'30 min'},
  {id:120,nombre:'Recementado de corona',cat:'Prótesis',dur:'30 min'},
  {id:121,nombre:'Recementado de corona (en garantía)',cat:'Prótesis',dur:'30 min'},
  {id:122,nombre:'Recementado de puente (en garantía)',cat:'Prótesis',dur:'30 min'},
  {id:123,nombre:'Recementado puente',cat:'Prótesis',dur:'30 min'},
  {id:124,nombre:'Reco post endodoncia compleja (tallado)',cat:'Operatoria',dur:'60 min'},
  {id:125,nombre:'Reco post endodoncia simple (cementado)',cat:'Operatoria',dur:'40 min'},
  {id:126,nombre:'Reco post endodoncia simple (tallado)',cat:'Operatoria',dur:'75 min'},
  {id:127,nombre:'Reimplante (ambiente quirúrgico) en garantía',cat:'Implantes',dur:'60 min'},
  {id:128,nombre:'Renovación de consulta',cat:'Consultas',dur:'60 min'},
  {id:129,nombre:'Retiro de ortodoncia',cat:'Ortodoncia',dur:'45 min'},
  {id:130,nombre:'Retiro de sutura',cat:'Cirugía',dur:'5 min'},
  {id:131,nombre:'Retratamiento de conducto',cat:'Endodoncia',dur:'60-90 min'},
  {id:132,nombre:'ROG en implante (misma cirugía)',cat:'Implantes',dur:'15 min'},
  {id:133,nombre:'ROG: regeneración ósea guiada (cirugía)',cat:'Implantes',dur:'45 min'},
  {id:134,nombre:'Selladores',cat:'Prevención',dur:'20 min'},
  {id:135,nombre:'Service prótesis híbrida',cat:'Implantes',dur:'90-120 min'},
  {id:136,nombre:'Teleodontología (primera consulta virtual)',cat:'Consultas',dur:'15 min'},
  {id:137,nombre:'Toma de impresiones',cat:'Prótesis',dur:'15 min'},
  {id:138,nombre:'Tratamiento de conducto uni',cat:'Endodoncia',dur:'60 min'},
  {id:139,nombre:'Tratamiento de conducto bi',cat:'Endodoncia',dur:'60 min'},
  {id:140,nombre:'Tratamiento de conducto multi',cat:'Endodoncia',dur:'30+ min'},
  {id:141,nombre:'Tratamiento intermedio',cat:'Endodoncia',dur:'30 min'},
  {id:142,nombre:'Traumatismo dentario maxilar abordaje',cat:'Cirugía',dur:'90 min'},
  {id:143,nombre:'Service prótesis híbrida (corto)',cat:'Implantes',dur:'90 min'},
];

// Usuarios iniciales
const USERS_INIT = [
  {id:1,nombre:'Administrador',rol:'admin',pin:'1234',color:'#1A3557',iniciales:'AD'},
];

// ══════════════════════════════════════════════════════════════════════════════
// ESTADO
// ══════════════════════════════════════════════════════════════════════════════
// Datos en memoria (se sincronizan con Firebase)
let mats   = [];
let hist   = [];
let cfg    = {};
let prests = [];
let users  = [];

let nextMatId   = mats.reduce((a,m)=>Math.max(a,m.id),0)+1;
let nextPrestId = prests.reduce((a,p)=>Math.max(a,p.id),0)+1;
let nextUserId  = users.reduce((a,u)=>Math.max(a,u.id),0)+1;
let editMatId=null, editPrestId=null, editUserId=null, cfgPrestId=null;
let currentUser = null;
let pinBuffer = '';
let selectedUserId = null;

async function save(){
  if(!window._db) return;
  const db=window._db;
  await Promise.all([
    window._fbSetDoc(window._fbDoc(db,'datos','mats'),   {v:JSON.stringify(mats)}),
    window._fbSetDoc(window._fbDoc(db,'datos','cfg'),    {v:JSON.stringify(cfg)}),
    window._fbSetDoc(window._fbDoc(db,'datos','prests'), {v:JSON.stringify(prests)}),
    window._fbSetDoc(window._fbDoc(db,'datos','users'),  {v:JSON.stringify(users)}),
  ]);
  // Historial: guardar solo el último evento (append)
  if(hist.length>0){
    const last=hist[hist.length-1];
    await window._fbSetDoc(window._fbDoc(db,'datos','hist'), {v:JSON.stringify(hist)});
  }
}

// ══════════════════════════════════════════════════════════════════════════════
// HELPERS
// ══════════════════════════════════════════════════════════════════════════════
function estadoClass(m){ return m.stock<=0?'danger':m.minimo>0&&m.stock<=m.minimo?'warn':'ok'; }
function estadoLabel(m){ return m.stock<=0?'🔴 Agotado':m.minimo>0&&m.stock<=m.minimo?'🟡 Stock bajo':'🟢 Normal'; }
function pct(m){ return !m.minimo?100:Math.min(100,Math.round(m.stock/(m.minimo*3)*100)); }
function hoy(){ return new Date().toLocaleDateString('es-AR'); }
function matNom(id){ const m=mats.find(x=>x.id===id); return m?m.nombre:'?'; }
function insumosDe(pid){ return cfg[pid]||[]; }
function tieneInsumos(pid){ return (cfg[pid]||[]).length>0; }
function isAdmin(){ return currentUser&&currentUser.rol==='admin'; }

function vencStatus(venc){
  if(!venc)return null;
  const hoyD=new Date(); hoyD.setDate(1); hoyD.setHours(0,0,0,0);
  const [y,mo]=venc.split('-').map(Number);
  const vD=new Date(y,mo-1,1);
  const diff=Math.round((vD-hoyD)/(1000*60*60*24));
  if(diff<0)return{clase:'venc-vencido',label:'⛔ Vencido'};
  if(diff<=60)return{clase:'venc-pronto',label:`⚠️ ${formatVenc(venc)}`};
  return{clase:'venc-ok',label:`✅ ${formatVenc(venc)}`};
}
function formatVenc(v){
  if(!v)return'—';
  const [y,mo]=v.split('-');
  const m=['ene','feb','mar','abr','may','jun','jul','ago','sep','oct','nov','dic'];
  return`${m[parseInt(mo)-1]} ${y}`;
}

// ══════════════════════════════════════════════════════════════════════════════
// LOGIN
// ══════════════════════════════════════════════════════════════════════════════
function initLogin(){
  const grid=document.getElementById('user-grid');
  grid.innerHTML=users.map(u=>`
    <button class="user-btn" onclick="seleccionarUsuario(${u.id})">
      <div class="avatar" style="background:${u.color}">${u.iniciales||u.nombre.slice(0,2).toUpperCase()}</div>
      <span>${u.nombre}</span>
      <span style="font-size:10px;color:#888;font-weight:400">${u.rol==='admin'?'Admin':'Prof.'}</span>
    </button>`).join('');
  document.getElementById('pin-wrap').style.display='none';
  document.getElementById('login-err').textContent='';
  pinBuffer='';
  selectedUserId=null;
}

function seleccionarUsuario(id){
  if(!id){
    document.getElementById('pin-wrap').style.display='none';
    document.querySelectorAll('.user-btn').forEach(b=>b.classList.remove('selected'));
    selectedUserId=null; pinBuffer=''; updatePinDots(); return;
  }
  selectedUserId=id;
  document.querySelectorAll('.user-btn').forEach(b=>b.classList.remove('selected'));
  event.currentTarget&&event.currentTarget.classList.add('selected');
  document.getElementById('pin-wrap').style.display='block';
  const u=users.find(x=>x.id===id);
  document.getElementById('pin-label').textContent=`PIN de ${u.nombre}`;
  document.getElementById('login-err').textContent='';
  pinBuffer=''; updatePinDots();
  buildNumpad();
}

function buildNumpad(){
  const np=document.getElementById('numpad');
  const btns=[1,2,3,4,5,6,7,8,9,'⌫',0,'✓'];
  np.innerHTML=btns.map(b=>`<button class="numpad-btn${b==='⌫'?' del':''}" onclick="numpadPress('${b}')">${b}</button>`).join('');
}

function numpadPress(val){
  const err=document.getElementById('login-err');
  if(val==='⌫'){ pinBuffer=pinBuffer.slice(0,-1); updatePinDots(); err.textContent=''; return; }
  if(val==='✓'){ intentarLogin(); return; }
  if(pinBuffer.length>=4)return;
  pinBuffer+=val; updatePinDots();
  if(pinBuffer.length===4) setTimeout(intentarLogin,150);
}

function updatePinDots(){
  document.querySelectorAll('.pin-dot').forEach((d,i)=>d.classList.toggle('filled',i<pinBuffer.length));
}

function intentarLogin(){
  const u=users.find(x=>x.id===selectedUserId);
  if(!u)return;
  if(pinBuffer===u.pin){
    currentUser=u;
    document.getElementById('login-screen').classList.add('hidden');
    document.getElementById('user-name-header').textContent=u.nombre;
    document.getElementById('user-dot-header').textContent=u.iniciales||u.nombre.slice(0,2).toUpperCase();
    document.getElementById('user-dot-header').style.background=u.color;
    // Mostrar/ocultar tab admin
    if(isAdmin()){
      document.getElementById('tab-admin').classList.add('show');
      document.querySelectorAll('.admin-only').forEach(el=>el.classList.add('show'));
    } else {
      document.getElementById('tab-admin').classList.remove('show');
      document.querySelectorAll('.admin-only').forEach(el=>el.classList.remove('show'));
    }
    render();
  } else {
    document.getElementById('login-err').textContent='PIN incorrecto. Intentá de nuevo.';
    pinBuffer=''; updatePinDots();
  }
}

function cerrarSesion(){
  if(!confirm('¿Cerrar sesión?'))return;
  currentUser=null; pinBuffer='';
  document.getElementById('login-screen').classList.remove('hidden');
  initLogin();
}

// ══════════════════════════════════════════════════════════════════════════════
// TABS
// ══════════════════════════════════════════════════════════════════════════════
function showTab(id,el){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.tab').forEach(t=>t.classList.remove('active'));
  document.getElementById('page-'+id).classList.add('active');
  el.classList.add('active');
  if(id==='prestaciones') renderPrestaciones();
  if(id==='historial-tab') renderHistFull();
  if(id==='admin') renderAdmin();
}

// ══════════════════════════════════════════════════════════════════════════════
// RENDER INVENTARIO
// ══════════════════════════════════════════════════════════════════════════════
function render(){
  document.getElementById('fecha-sub').textContent=
    'Actualizado: '+new Date().toLocaleDateString('es-AR',{weekday:'long',year:'numeric',month:'long',day:'numeric'});
  const ok=mats.filter(m=>estadoClass(m)==='ok').length;
  const warn=mats.filter(m=>estadoClass(m)==='warn').length;
  const danger=mats.filter(m=>estadoClass(m)==='danger').length;
  const venc=mats.filter(m=>{const s=vencStatus(m.venc);return s&&(s.clase==='venc-vencido'||s.clase==='venc-pronto');}).length;

  document.getElementById('stats').innerHTML=`
    <div class="stat"><div class="num">${mats.length}</div><div class="lbl">📦 Materiales</div></div>
    <div class="stat ok"><div class="num">${ok}</div><div class="lbl">✅ OK</div></div>
    <div class="stat warn"><div class="num">${warn}</div><div class="lbl">⚠️ Stock bajo</div></div>
    <div class="stat danger"><div class="num">${danger}</div><div class="lbl">🚨 Agotados</div></div>
    <div class="stat ${venc>0?'danger':''}"><div class="num" style="${venc>0?'color:var(--rojo)':''}">${venc}</div><div class="lbl">📅 Venc./Por vencer</div></div>
  `;

  const criticos=mats.filter(m=>m.minimo>0&&m.stock<=m.minimo);
  const vencAlert=mats.filter(m=>{const s=vencStatus(m.venc);return s&&(s.clase==='venc-vencido'||s.clase==='venc-pronto');});
  const ab=document.getElementById('alert-bar');
  const msgs=[];
  if(criticos.length) msgs.push('🚨 <strong>Reponer:</strong> '+criticos.map(m=>m.nombre+(m.stock<=0?' (agotado)':`(quedan ${+m.stock.toFixed(2)})`)).join(' · '));
  if(vencAlert.length) msgs.push('📅 <strong>Vencimiento:</strong> '+vencAlert.map(m=>`${m.nombre} (${formatVenc(m.venc)})`).join(' · '));
  if(msgs.length){ab.style.display='block';ab.innerHTML=msgs.join('<br>');}else{ab.style.display='none';}

  renderTabla();
  renderHistMini();
}

function renderTabla(){
  const q=(document.getElementById('buscar-mat')?.value||'').toLowerCase();
  const lista=q?mats.filter(m=>m.nombre.toLowerCase().includes(q)||m.cat.toLowerCase().includes(q)):mats;
  const tbody=document.getElementById('tabla');
  if(!lista.length){tbody.innerHTML='<tr><td colspan="7" class="empty-row">Sin resultados.</td></tr>';return;}
  tbody.innerHTML=lista.map(m=>{
    const sc=estadoClass(m); const vs=vencStatus(m.venc);
    const acciones=isAdmin()
      ?`<button class="sm" onclick="abrirMovimiento(${m.id},'in')">📥</button>
        <button class="sm" onclick="abrirMovimiento(${m.id},'out')">📤</button>
        <button class="sm" onclick="abrirEditarMat(${m.id})">✏️</button>
        <button class="sm" onclick="eliminarMat(${m.id})">🗑️</button>`
      :`<button class="sm" onclick="abrirMovimiento(${m.id},'in')">📥</button>
        <button class="sm" onclick="abrirMovimiento(${m.id},'out')">📤</button>`;
    return`<tr>
      <td><div style="font-weight:600">${m.nombre}</div><div style="font-size:11px;color:#888">${m.cat}${m.obs?` · ${m.obs}`:''}</div></td>
      <td style="text-align:center;font-weight:700;font-size:15px">${+m.stock.toFixed(2)}</td>
      <td style="text-align:center;color:#777">${m.minimo||'—'}</td>
      <td><span class="bar-wrap"><span class="bar ${sc}" style="width:${pct(m)}%"></span></span></td>
      <td><span class="badge ${sc}">${estadoLabel(m)}</span></td>
      <td><span class="${vs?vs.clase:'venc-nd'}">${vs?vs.label:m.venc?formatVenc(m.venc):'—'}</span></td>
      <td style="font-size:12px;color:#777">${m.ubic||'—'}</td>
      <td style="display:flex;gap:4px;flex-wrap:wrap">${acciones}</td>
    </tr>`;
  }).join('');
}

function renderHistMini(){
  renderHistItems(document.getElementById('hist-mini'),[...hist].reverse().slice(0,15));
}
function renderHistFull(){
  const fu=document.getElementById('hist-filtro-user').value;
  const items=fu?hist.filter(h=>h.userId==fu):hist;
  renderHistItems(document.getElementById('hist-full'),[...items].reverse());
}
function renderHistItems(el,items){
  if(!items.length){el.innerHTML='<div class="empty-row">Sin movimientos aún.</div>';return;}
  el.innerHTML=items.map(h=>{
    const uColor=getUserColor(h.userId);
    const uNom=getUserNom(h.userId);
    if(h.tipo==='proc'){
      const det=(h.insumos||[]).map(i=>`${i.nombre}×${i.cant}`).join(', ');
      return`<div class="hist-item">
        <div>
          <strong>${h.nombre}</strong>${h.nota?' — '+h.nota:''}
          ${det?`<div style="color:var(--text-s);margin-top:2px;font-size:11px">${det}</div>`:''}
        </div>
        <div style="display:flex;align-items:center;gap:6px;flex-shrink:0;flex-direction:column;align-items:flex-end">
          <div style="display:flex;align-items:center;gap:5px">
            <span style="width:18px;height:18px;border-radius:50%;background:${uColor};display:inline-flex;align-items:center;justify-content:center;font-size:9px;font-weight:700;color:white">${uNom}</span>
            <span style="color:#999;font-size:11px">${h.fecha}</span>
          </div>
          <span class="tag proc">🦷${h.veces>1?' ×'+h.veces:''}</span>
        </div>
      </div>`;
    }
    return`<div class="hist-item">
      <span><strong>${h.nombre}</strong>${h.nota?' — '+h.nota:''}</span>
      <div style="display:flex;align-items:center;gap:6px;flex-shrink:0">
        <span style="width:18px;height:18px;border-radius:50%;background:${uColor};display:inline-flex;align-items:center;justify-content:center;font-size:9px;font-weight:700;color:white">${uNom}</span>
        <span style="color:#999;font-size:11px">${h.fecha}</span>
        <span class="tag ${h.tipo}">${h.tipo==='in'?'+':'−'}${h.cant}</span>
      </div>
    </div>`;
  }).join('');
}

function getUserColor(uid){ const u=users.find(x=>x.id==uid); return u?u.color:'#888'; }
function getUserNom(uid){ const u=users.find(x=>x.id==uid); return u?u.iniciales||u.nombre.slice(0,2).toUpperCase():'?'; }

// ══════════════════════════════════════════════════════════════════════════════
// RENDER PRESTACIONES
// ══════════════════════════════════════════════════════════════════════════════
function renderPrestaciones(){
  const q=(document.getElementById('buscar-prest')?.value||'').toLowerCase();
  const soloCfg=document.getElementById('solo-cfg')?.checked;
  let lista=q?prests.filter(p=>p.nombre.toLowerCase().includes(q)||p.cat.toLowerCase().includes(q)):prests;
  if(soloCfg) lista=lista.filter(p=>tieneInsumos(p.id));
  document.getElementById('prest-count').textContent=`${lista.length} prestaciones`;
  if(!lista.length){document.getElementById('prest-lista').innerHTML='<div class="empty-row">Sin resultados.</div>';return;}
  // Agrupar por categoría
  const cats={};
  lista.forEach(p=>{if(!cats[p.cat])cats[p.cat]=[];cats[p.cat].push(p);});
  document.getElementById('prest-lista').innerHTML=Object.entries(cats).map(([cat,ps])=>`
    <div class="cat-title">${cat}</div>
    ${ps.map(p=>{
      const ins=insumosDe(p.id);
      const adminBtns=isAdmin()
        ?`<button class="sm" onclick="abrirCfg(${p.id})" title="Configurar insumos">${ins.length?'✏️':'⚙️'}</button>
           <button class="sm" onclick="abrirEditarPrest(${p.id})">📝</button>
           <button class="sm" onclick="eliminarPrest(${p.id})">🗑️</button>`
        :`<button class="sm" onclick="abrirCfg(${p.id})" title="Ver insumos">${ins.length?'✏️':'⚙️'}</button>`;
      return`<div class="prest-row">
        <div>
          <div class="prest-name">${p.nombre}</div>
          <div class="prest-dur">${p.dur||''}${ins.length?` · <span class="badge cfg">${ins.length} insumo${ins.length>1?'s':''}</span>`:' · <span style="font-size:11px;color:#bbb">sin insumos</span>'}</div>
        </div>
        <div class="prest-actions">
          <button class="sm accent" onclick="abrirRegistrarUno(${p.id})">▶ Registrar</button>
          ${adminBtns}
        </div>
      </div>`;
    }).join('')}`).join('');
}

// ══════════════════════════════════════════════════════════════════════════════
// RENDER ADMIN
// ══════════════════════════════════════════════════════════════════════════════
function renderAdmin(){
  // Usuarios
  const ul=document.getElementById('admin-usuarios');
  ul.innerHTML=users.map(u=>`
    <div class="user-admin-row">
      <div style="display:flex;align-items:center;gap:10px">
        <div style="width:32px;height:32px;border-radius:50%;background:${u.color};display:flex;align-items:center;justify-content:center;font-size:12px;font-weight:700;color:white">${u.iniciales||u.nombre.slice(0,2).toUpperCase()}</div>
        <div>
          <div style="font-weight:600;font-size:13px">${u.nombre}</div>
          <div style="font-size:11px;color:var(--text-s)">${u.rol==='admin'?'Administrador':'Profesional'} · PIN: ${'•'.repeat(u.pin.length)}</div>
        </div>
      </div>
      <div style="display:flex;gap:5px">
        <button class="sm" onclick="abrirEditarUser(${u.id})">✏️</button>
        ${u.id===currentUser?.id?'':`<button class="sm" onclick="eliminarUser(${u.id})">🗑️</button>`}
      </div>
    </div>`).join('');

  // Insumos
  const il=document.getElementById('admin-insumos');
  il.innerHTML=mats.map(m=>{
    const vs=vencStatus(m.venc);
    return`<div class="admin-item">
      <div style="min-width:0">
        <div style="font-size:13px;font-weight:600;overflow:hidden;text-overflow:ellipsis;white-space:nowrap">${m.nombre}</div>
        <div style="font-size:11px;color:var(--text-s)">Stock: <strong>${+m.stock.toFixed(2)}</strong> · ${m.cat} · <span class="${vs?vs.clase:'venc-nd'}">${vs?vs.label:m.venc?formatVenc(m.venc):'sin venc.'}</span></div>
      </div>
      <div style="display:flex;gap:4px;flex-shrink:0">
        <button class="sm" onclick="abrirEditarMat(${m.id})">✏️</button>
        <button class="sm" onclick="eliminarMat(${m.id})">🗑️</button>
      </div>
    </div>`;
  }).join('');

  // Ajuste select
  const sel=document.getElementById('adj-mat');
  if(sel) sel.innerHTML=mats.map(m=>`<option value="${m.id}">${m.nombre} (stock: ${+m.stock.toFixed(2)})</option>`).join('');

  // Historial filtro usuarios
  const fu=document.getElementById('hist-filtro-user');
  if(fu) fu.innerHTML='<option value="">Todos los usuarios</option>'+users.map(u=>`<option value="${u.id}">${u.nombre}</option>`).join('');
}

// ══════════════════════════════════════════════════════════════════════════════
// MODAL: MATERIAL
// ══════════════════════════════════════════════════════════════════════════════
function abrirAgregarMat(){
  editMatId=null;
  document.getElementById('mat-titulo').textContent='Nuevo material';
  ['m-nombre','m-obs'].forEach(id=>document.getElementById(id).value='');
  document.getElementById('m-stock').value=0;
  document.getElementById('m-min').value=0;
  document.getElementById('m-venc').value='';
  document.getElementById('m-cat').value='General';
  document.getElementById('modal-mat').classList.add('open');
  setTimeout(()=>document.getElementById('m-nombre').focus(),50);
}
function abrirEditarMat(id){
  editMatId=id;
  const m=mats.find(x=>x.id===id);
  document.getElementById('mat-titulo').textContent='Editar material';
  document.getElementById('m-nombre').value=m.nombre;
  document.getElementById('m-cat').value=m.cat||'General';
  document.getElementById('m-stock').value=m.stock;
  document.getElementById('m-min').value=m.minimo;
  document.getElementById('m-venc').value=m.venc||'';
  document.getElementById('m-obs').value=m.obs||'';
  document.getElementById('m-ubic').value=m.ubic||'';
  document.getElementById('modal-mat').classList.add('open');
}
function guardarMat(){
  const nombre=document.getElementById('m-nombre').value.trim();
  if(!nombre){alert('Ingresá un nombre.');return;}
  const data={
    nombre, cat:document.getElementById('m-cat').value,
    stock:parseFloat(document.getElementById('m-stock').value)||0,
    minimo:parseFloat(document.getElementById('m-min').value)||0,
    venc:document.getElementById('m-venc').value||null,
    obs:document.getElementById('m-obs').value.trim(),
    ubic:document.getElementById('m-ubic').value||'',
  };
  if(editMatId){ Object.assign(mats.find(x=>x.id===editMatId),data); }
  else { mats.push({id:nextMatId++,...data,consumido:0}); }
  save();render();if(document.getElementById('page-admin').classList.contains('active'))renderAdmin();
  cerrar('modal-mat');
}
function eliminarMat(id){
  if(!confirm('¿Eliminar este material?'))return;
  mats=mats.filter(x=>x.id!==id);
  save();render();if(document.getElementById('page-admin').classList.contains('active'))renderAdmin();
}

// ══════════════════════════════════════════════════════════════════════════════
// MODAL: MOVIMIENTO MANUAL
// ══════════════════════════════════════════════════════════════════════════════
function abrirMovimiento(id,tipo){
  document.getElementById('mov-mat').innerHTML=mats.map(m=>`<option value="${m.id}"${m.id===id?' selected':''}>${m.nombre}</option>`).join('');
  document.getElementById('mov-tipo').value=tipo||'in';
  document.getElementById('mov-cant').value=1;
  document.getElementById('mov-nota').value='';
  document.getElementById('modal-mov').classList.add('open');
  setTimeout(()=>document.getElementById('mov-cant').focus(),50);
}
function confirmarMov(){
  const matId=parseInt(document.getElementById('mov-mat').value);
  const tipo=document.getElementById('mov-tipo').value;
  const cant=parseFloat(document.getElementById('mov-cant').value)||0;
  const nota=document.getElementById('mov-nota').value.trim();
  if(cant<=0){alert('La cantidad debe ser mayor a 0.');return;}
  const m=mats.find(x=>x.id===matId);
  if(tipo==='out'&&cant>m.stock){alert(`Stock insuficiente. Disponible: ${m.stock}`);return;}
  if(tipo==='out'){m.stock=+(m.stock-cant).toFixed(4);m.consumido=(m.consumido||0)+cant;}
  else{m.stock=+(m.stock+cant).toFixed(4);}
  hist.push({fecha:hoy(),nombre:m.nombre,tipo,cant,nota,userId:currentUser?.id});
  save();render();cerrar('modal-mov');
}

// ══════════════════════════════════════════════════════════════════════════════
// MODAL: CONFIGURAR INSUMOS
// ══════════════════════════════════════════════════════════════════════════════
function abrirCfg(pid){
  cfgPrestId=pid;
  const p=prests.find(x=>x.id===pid);
  document.getElementById('cfg-titulo').textContent=`Configurar insumos`;
  document.getElementById('cfg-desc').textContent=p.nombre;
  document.getElementById('cfg-lines').innerHTML='';
  const ins=insumosDe(pid);
  if(ins.length) ins.forEach(i=>agregarLineaCfg(i.matId,i.cant));
  else agregarLineaCfg();
  document.getElementById('modal-cfg').classList.add('open');
}
function agregarLineaCfg(matId=null,cant=1){
  const c=document.getElementById('cfg-lines');
  const d=document.createElement('div');
  d.className='insumo-line';
  const opts=mats.map(m=>`<option value="${m.id}"${m.id===matId?' selected':''}>${m.nombre}</option>`).join('');
  d.innerHTML=`<select>${opts}</select><input type="number" min="0.001" step="0.001" value="${cant}"><button class="rm-btn" onclick="this.parentElement.remove()">×</button>`;
  c.appendChild(d);
}
function guardarCfg(){
  const lines=[...document.querySelectorAll('#cfg-lines .insumo-line')];
  cfg[cfgPrestId]=lines.map(l=>({
    matId:parseInt(l.querySelector('select').value),
    cant:parseFloat(l.querySelector('input').value)||1
  })).filter(i=>i.matId);
  save();
  if(document.getElementById('page-prestaciones').classList.contains('active')) renderPrestaciones();
  cerrar('modal-cfg');
}

// ══════════════════════════════════════════════════════════════════════════════
// MODAL: REGISTRAR PRESTACIÓN
// ══════════════════════════════════════════════════════════════════════════════
function abrirRegistrar(){
  const conIns=prests.filter(p=>tieneInsumos(p.id));
  if(!conIns.length){
    alert('Ninguna prestación tiene insumos configurados todavía.\n\nAndate a "Prestaciones", buscá la práctica y tocá ⚙️ para asignar los insumos que consume.');
    return;
  }
  poblarRegSel(conIns);
  document.getElementById('reg-cant').value=1;
  document.getElementById('reg-nota').value='';
  document.getElementById('reg-preview').innerHTML='';
  document.getElementById('modal-reg').classList.add('open');
}
function abrirRegistrarUno(pid){
  poblarRegSel(prests.filter(p=>tieneInsumos(p.id)));
  document.getElementById('reg-sel').value=pid;
  document.getElementById('reg-cant').value=1;
  document.getElementById('reg-nota').value='';
  previewReg();
  document.getElementById('modal-reg').classList.add('open');
}
function poblarRegSel(lista){
  const cats={};
  lista.forEach(p=>{if(!cats[p.cat])cats[p.cat]=[];cats[p.cat].push(p);});
  document.getElementById('reg-sel').innerHTML=
    '<option value="">-- Seleccioná --</option>'+
    Object.entries(cats).map(([cat,ps])=>
      `<optgroup label="${cat}">${ps.map(p=>`<option value="${p.id}">${p.nombre}</option>`).join('')}</optgroup>`
    ).join('');
}
function previewReg(){
  const pid=parseInt(document.getElementById('reg-sel').value);
  const veces=parseInt(document.getElementById('reg-cant').value)||1;
  if(!pid){document.getElementById('reg-preview').innerHTML='';return;}
  const ins=insumosDe(pid);
  if(!ins.length){document.getElementById('reg-preview').innerHTML='<div style="color:var(--text-s);font-size:12px;padding:8px">Sin insumos configurados.</div>';return;}
  const rows=ins.map(i=>{
    const m=mats.find(x=>x.id===i.matId);
    const total=+(i.cant*veces).toFixed(4);
    const insuf=m&&total>m.stock;
    return`<div class="confirm-row"><span>${m?m.nombre:'?'}</span><span class="${insuf?'warn-txt':''}">−${total}${insuf?` ⚠️(stock:${m?m.stock:0})`:''}</span></div>`;
  }).join('');
  document.getElementById('reg-preview').innerHTML=`<div class="confirm-box">
    <div style="font-size:11px;font-weight:700;color:var(--text-s);margin-bottom:6px">SE DESCUENTA${veces>1?' (×'+veces+')':''}:</div>${rows}</div>`;
}
function confirmarReg(){
  const pid=parseInt(document.getElementById('reg-sel').value);
  const veces=parseInt(document.getElementById('reg-cant').value)||1;
  const nota=document.getElementById('reg-nota').value.trim();
  if(!pid){alert('Seleccioná una prestación.');return;}
  const p=prests.find(x=>x.id===pid);
  const ins=insumosDe(pid);
  if(!ins.length){alert('Sin insumos configurados.');return;}
  const sinStock=ins.filter(i=>{const m=mats.find(x=>x.id===i.matId);return m&&(i.cant*veces)>m.stock;});
  if(sinStock.length){if(!confirm(`⚠️ Stock insuficiente para: ${sinStock.map(i=>matNom(i.matId)).join(', ')}\n\n¿Registrar igual?`))return;}
  const log=[];
  ins.forEach(i=>{
    const m=mats.find(x=>x.id===i.matId); if(!m)return;
    const total=+(i.cant*veces).toFixed(4);
    m.stock=+Math.max(0,m.stock-total).toFixed(4);
    m.consumido=+((m.consumido||0)+total).toFixed(4);
    log.push({nombre:m.nombre,cant:total});
  });
  hist.push({fecha:hoy(),tipo:'proc',nombre:`🦷 ${p.nombre}`,nota,veces,insumos:log,userId:currentUser?.id});
  save();render();cerrar('modal-reg');
  setTimeout(()=>alert('✅ Registrado.\n\nDescontado:\n'+log.map(i=>`• ${i.nombre}: −${i.cant}`).join('\n')),80);
}

// ══════════════════════════════════════════════════════════════════════════════
// MODAL: PRESTACIÓN
// ══════════════════════════════════════════════════════════════════════════════
function abrirNuevaPrest(){
  editPrestId=null;
  document.getElementById('prest-titulo').textContent='Nueva prestación';
  document.getElementById('p-nombre').value='';
  document.getElementById('p-dur').value='';
  document.getElementById('p-cat').value='Consultas';
  document.getElementById('modal-prest').classList.add('open');
  setTimeout(()=>document.getElementById('p-nombre').focus(),50);
}
function abrirEditarPrest(id){
  editPrestId=id;
  const p=prests.find(x=>x.id===id);
  document.getElementById('prest-titulo').textContent='Editar prestación';
  document.getElementById('p-nombre').value=p.nombre;
  document.getElementById('p-dur').value=p.dur||'';
  document.getElementById('p-cat').value=p.cat;
  document.getElementById('modal-prest').classList.add('open');
}
function guardarPrest(){
  const nombre=document.getElementById('p-nombre').value.trim();
  if(!nombre){alert('Ingresá un nombre.');return;}
  const data={nombre,cat:document.getElementById('p-cat').value,dur:document.getElementById('p-dur').value.trim()};
  if(editPrestId){ Object.assign(prests.find(x=>x.id===editPrestId),data); }
  else { prests.push({id:nextPrestId++,...data}); }
  save();renderPrestaciones();cerrar('modal-prest');
}
function eliminarPrest(id){
  if(!confirm('¿Eliminar esta prestación?'))return;
  prests=prests.filter(x=>x.id!==id);
  delete cfg[id];
  save();renderPrestaciones();
}

// ══════════════════════════════════════════════════════════════════════════════
// MODAL: USUARIOS
// ══════════════════════════════════════════════════════════════════════════════
function abrirNuevoUsuario(){
  editUserId=null;
  document.getElementById('user-titulo').textContent='Nuevo usuario';
  ['u-nombre','u-pin'].forEach(id=>document.getElementById(id).value='');
  document.getElementById('u-rol').value='prof';
  document.getElementById('u-color').value='#2563A8';
  document.getElementById('modal-user').classList.add('open');
  setTimeout(()=>document.getElementById('u-nombre').focus(),50);
}
function abrirEditarUser(id){
  editUserId=id;
  const u=users.find(x=>x.id===id);
  document.getElementById('user-titulo').textContent='Editar usuario';
  document.getElementById('u-nombre').value=u.nombre;
  document.getElementById('u-rol').value=u.rol;
  document.getElementById('u-pin').value=u.pin;
  document.getElementById('u-color').value=u.color;
  document.getElementById('modal-user').classList.add('open');
}
function guardarUsuario(){
  const nombre=document.getElementById('u-nombre').value.trim();
  const pin=document.getElementById('u-pin').value.trim();
  if(!nombre){alert('Ingresá un nombre.');return;}
  if(!/^\d{4}$/.test(pin)){alert('El PIN debe tener exactamente 4 dígitos numéricos.');return;}
  const color=document.getElementById('u-color').value;
  const iniciales=nombre.split(' ').map(w=>w[0]).join('').slice(0,2).toUpperCase();
  const data={nombre,rol:document.getElementById('u-rol').value,pin,color,iniciales};
  if(editUserId){ Object.assign(users.find(x=>x.id===editUserId),data); }
  else { users.push({id:nextUserId++,...data}); }
  save();renderAdmin();cerrar('modal-user');
}
function eliminarUser(id){
  if(id===currentUser?.id){alert('No podés eliminar tu propio usuario.');return;}
  if(!confirm('¿Eliminar este usuario?'))return;
  users=users.filter(x=>x.id!==id);
  save();renderAdmin();
}

// ══════════════════════════════════════════════════════════════════════════════
// AJUSTE RÁPIDO
// ══════════════════════════════════════════════════════════════════════════════
function previewAdj(){
  const m=mats.find(x=>x.id===parseInt(document.getElementById('adj-mat')?.value));
  const nuevo=parseFloat(document.getElementById('adj-cant')?.value);
  const prev=document.getElementById('adj-preview');
  if(!m||isNaN(nuevo)){if(prev)prev.textContent='';return;}
  const diff=+(nuevo-m.stock).toFixed(2);
  prev.innerHTML=`Actual: <strong>${+m.stock.toFixed(2)}</strong> → nuevo: <strong>${nuevo}</strong> <span style="color:${diff>=0?'var(--verde)':'var(--rojo)'}">(${diff>=0?'+':''}${diff})</span>`;
}
function confirmarAdj(){
  const matId=parseInt(document.getElementById('adj-mat').value);
  const nuevo=parseFloat(document.getElementById('adj-cant').value);
  if(isNaN(nuevo)||nuevo<0){alert('Valor inválido.');return;}
  const m=mats.find(x=>x.id===matId);
  const viejo=m.stock; m.stock=nuevo;
  hist.push({fecha:hoy(),nombre:m.nombre,tipo:nuevo>=viejo?'in':'out',cant:+Math.abs(nuevo-viejo).toFixed(2),nota:'Ajuste de inventario',userId:currentUser?.id});
  save();render();renderAdmin();
  document.getElementById('adj-cant').value='';
  document.getElementById('adj-preview').textContent='';
  alert(`✅ Stock de "${m.nombre}" ajustado a ${nuevo}.`);
}

// ══════════════════════════════════════════════════════════════════════════════
// RESPALDO
// ══════════════════════════════════════════════════════════════════════════════
function exportarRespaldo(){
  const data={version:4,fecha:new Date().toISOString(),mats,hist,cfg,prests,users};
  const a=document.createElement('a');
  a.href='data:application/json;charset=utf-8,'+encodeURIComponent(JSON.stringify(data,null,2));
  a.download='respaldo_stock_'+new Date().toISOString().slice(0,10)+'.json';
  a.click();
}
function importarRespaldo(input){
  const file=input.files[0]; if(!file)return;
  const reader=new FileReader();
  reader.onload=e=>{
    try{
      const data=JSON.parse(e.target.result);
      if(!data.mats)throw new Error('inválido');
      if(!confirm(`¿Importar respaldo del ${data.fecha?data.fecha.slice(0,10):'?'}?\nEsto reemplazará todos los datos actuales.`))return;
      mats=data.mats||[];hist=data.hist||[];cfg=data.cfg||{};prests=data.prests||[];users=data.users||[];
      nextMatId=mats.reduce((a,m)=>Math.max(a,m.id),0)+1;
      nextPrestId=prests.reduce((a,p)=>Math.max(a,p.id),0)+1;
      nextUserId=users.reduce((a,u)=>Math.max(a,u.id),0)+1;
      save();render();renderAdmin();
      alert('✅ Respaldo importado.');
    }catch(e){alert('Error al leer el archivo.');}
  };
  reader.readAsText(file); input.value='';
}
function exportCSV(){
  let csv='INVENTARIO\nMaterial,Categoría,Stock,Mínimo,Estado,Vencimiento,Obs\n';
  mats.forEach(m=>csv+=`"${m.nombre}","${m.cat}",${m.stock},${m.minimo},"${estadoLabel(m).replace(/[🔴🟡🟢]/g,'').trim()}","${m.venc?formatVenc(m.venc):'—'}","${m.obs||''}"\n`);
  csv+='\nHISTORIAL\nFecha,Usuario,Tipo,Detalle\n';
  [...hist].reverse().forEach(h=>{
    const u=getUserNom(h.userId);
    if(h.tipo==='proc') csv+=`"${h.fecha}","${u}","Prestación","${h.nombre}${h.veces>1?' ×'+h.veces:''}${h.nota?' — '+h.nota:''}"\n`;
    else csv+=`"${h.fecha}","${u}","${h.tipo==='in'?'Entrada':'Salida'}","${h.nombre} ${h.tipo==='in'?'+':'-'}${h.cant}${h.nota?' — '+h.nota:''}"\n`;
  });
  const a=document.createElement('a');
  a.href='data:text/csv;charset=utf-8,\uFEFF'+encodeURIComponent(csv);
  a.download='stock_'+new Date().toISOString().slice(0,10)+'.csv';
  a.click();
}
function resetearDatos(){
  if(!confirm('⚠️ Borrará TODOS los datos.\n¿Estás seguro?'))return;
  if(!confirm('Última confirmación.'))return;
  mats=MATS_INIT;hist=[];cfg={};prests=PRESTS_INIT;users=USERS_INIT;
  nextMatId=mats.reduce((a,m)=>Math.max(a,m.id),0)+1;
  nextPrestId=prests.reduce((a,p)=>Math.max(a,p.id),0)+1;
  nextUserId=users.reduce((a,u)=>Math.max(a,u.id),0)+1;
  save();render();renderAdmin();alert('Datos reseteados a los valores iniciales.');
}

function cerrar(id){document.getElementById(id).classList.remove('open');}
document.querySelectorAll('.overlay').forEach(el=>el.addEventListener('click',e=>{if(e.target===el)el.classList.remove('open');}));

// ══════════════════════════════════════════════════════════════════════════════
// INIT
// ══════════════════════════════════════════════════════════════════════════════
// ══ BOOTSTRAP FIREBASE ══════════════════════════════════════════════════════
function mostrarCargando(msg){
  document.getElementById('login-screen').innerHTML=`
    <div style="text-align:center;color:white">
      <div style="font-size:40px;margin-bottom:16px">🦷</div>
      <div style="font-size:16px;font-weight:700">Consultorio Odontológico</div>
      <div style="font-size:13px;opacity:.7;margin-top:8px">${msg}</div>
      <div style="margin-top:20px;width:40px;height:40px;border:3px solid rgba(255,255,255,.3);border-top-color:white;border-radius:50%;animation:spin .8s linear infinite;margin:20px auto"></div>
    </div>
    <style>@keyframes spin{to{transform:rotate(360deg)}}</style>`;
}

async function cargarDatos(db){
  mostrarCargando('Conectando con la base de datos...');
  try {
    const [dMats,dCfg,dPrests,dUsers,dHist] = await Promise.all([
      window._fbGetDoc(window._fbDoc(db,'datos','mats')),
      window._fbGetDoc(window._fbDoc(db,'datos','cfg')),
      window._fbGetDoc(window._fbDoc(db,'datos','prests')),
      window._fbGetDoc(window._fbDoc(db,'datos','users')),
      window._fbGetDoc(window._fbDoc(db,'datos','hist')),
    ]);
    mats   = dMats.exists()   ? JSON.parse(dMats.data().v)   : MATS_INIT;
    cfg    = dCfg.exists()    ? JSON.parse(dCfg.data().v)    : {};
    prests = dPrests.exists() ? JSON.parse(dPrests.data().v) : PRESTS_INIT;
    users  = dUsers.exists()  ? JSON.parse(dUsers.data().v)  : USERS_INIT;
    hist   = dHist.exists()   ? JSON.parse(dHist.data().v)   : [];

    nextMatId   = mats.reduce((a,m)=>Math.max(a,m.id),0)+1;
    nextPrestId = prests.reduce((a,p)=>Math.max(a,p.id),0)+1;
    nextUserId  = users.reduce((a,u)=>Math.max(a,u.id),0)+1;

    // Si es primera vez, guardar datos iniciales
    if(!dMats.exists()) await save();

    // Escuchar cambios en tiempo real
    window._fbOnSnapshot(window._fbDoc(db,'datos','mats'),   snap=>{if(snap.exists()&&currentUser){mats=JSON.parse(snap.data().v);nextMatId=mats.reduce((a,m)=>Math.max(a,m.id),0)+1;render();if(document.getElementById('page-admin').classList.contains('active'))renderAdmin();}});
    window._fbOnSnapshot(window._fbDoc(db,'datos','hist'),   snap=>{if(snap.exists()&&currentUser){hist=JSON.parse(snap.data().v);renderHistMini();if(document.getElementById('page-historial-tab').classList.contains('active'))renderHistFull();}});
    window._fbOnSnapshot(window._fbDoc(db,'datos','prests'), snap=>{if(snap.exists()&&currentUser){prests=JSON.parse(snap.data().v);nextPrestId=prests.reduce((a,p)=>Math.max(a,p.id),0)+1;if(document.getElementById('page-prestaciones').classList.contains('active'))renderPrestaciones();}});
    window._fbOnSnapshot(window._fbDoc(db,'datos','users'),  snap=>{if(snap.exists()&&currentUser){users=JSON.parse(snap.data().v);nextUserId=users.reduce((a,u)=>Math.max(a,u.id),0)+1;}});
    window._fbOnSnapshot(window._fbDoc(db,'datos','cfg'),    snap=>{if(snap.exists()&&currentUser){cfg=JSON.parse(snap.data().v);}});

    // Restaurar login screen y mostrar usuarios
    document.getElementById('login-screen').innerHTML=`
      <div style="text-align:center;color:white;margin-bottom:4px">
        <img src="data:image/jpeg;base64,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AAAA88888++++KCS/uCD2+LCDCwHc99999999999999999999s4KAAAAAAAAAAAgAQ0888iCSS2+OCyuKC3+KHc8999999999999999999999998PCIAIAAAAAAAAAAQwgweOeuOCy+KS+KCWlV9999999999999999999999999998M988sMMMMIIAAAAAAMMMM8wkIwMQ2OO9999999999999999999999999999998d6Qwwww0888oAAAAMMAMM8wMwMwMv8APfffffffffffffffffffffffffffffffSggAAAAAAEPCAAADGMMIDMDMCJGPPffffffffffffeOMNMcc/fffffffffffffW//LDCAAAMPAAAHMNOMJGJMGLn/ffffffffffduWMNw+jn8PZ+9fffffffffffaefPPDAAANCCADst/wBOduZJyz333333333z3akZBKAAAAAADAtGrv33333333325zzzwAABTygCJf8A/wDw9y7k/ffffffffY5/ij8QAAAAAAAAAAEEtv8AX33333333yjzzwAABTygApP8/wDjXDuU999999989LVKxAAAAAAAAAAAAAAAWlS1999999995188AAAU8sA2PTzDP7Hs99999999rRkFgAAAAAAAAAAAAAAAAAiXu899999998Z84AAAU8sAmOyyyyP/APPffffffecXJYAAAAAAAAAAAAAAAAAAAAKe9ffffffffsQAAAHPPAIjOsssjjfffffffI81GoAAAAAAAAAAAAAAAAAAAAAF6g9fffffffJgAAAEPPPMpDvvjDVfffffffIwCiQAAAASjQwwAAAADSQQyQAAAHDnvffffffbyAAAAMMPMNDDDDPvffffffeYQCwAAAAMBQQTrGB3XmBEcPjQAAA1IdffffffbHzCAAAAMMLDDDDPffffffaJgDoQAAHbwUdd/smsTvDrAJMzbAAAHO0/ffffffHvPAAAAANDCMMMPvfffffZ6QrAAABQ+/8Aa9vM6PLFwhCYbzLGoABHTPX33333xjDyzwwAAgDDzzvT3333310DCoAAAc8wrEDxIIxIAAAABaWNkAAAHZ9/33333ygFHzz30zzwwAEBz333331cB4kAAAgJJMmdiCAAAAAAAADRSesAABzv/wB99999vBBxBx19BR199q9999999qASAAAA5cMnoAAAAAAAAAAAAg6c2AAAVtD999999sKBBBBBB9NJBBw999999sAEzAAAAvDDjAAAAAAAAAAAAAdI56AAAD9v9999999DBBBBBBxx999s999999oBBrAAAAbQ06CAAAAAAAAAAAA6bTvAAAG9P9999998rBBBBBBBBBBBq999999spFFAAAAHkOLpAAAAAAAAAAAARH1IAAAa9T99999983989PJBCDDCCk9999998IQDAAAAQuktuAAAAAAAAAAAUUtaLAAAE9z9999998xiyCy2+CCCCCN9999999gALAAAAAcddEIAAAABAAAAAtgbkAAAAO5P999999onOOOIKyuCCCCvU999998MALhAAAAQPOeNAAAA2IAAATIeBKAAAAzrX999998u7DDDDzzT3P8A84dffffffayAywAAAAAZbjwQABdggAABhgQ6QAAFbmVffffffPx//wD+u88sMMc8D3333333wBEQAAAABA9KBckBCYQgB8bkFsAAABPmd3333331x7L47Lb6oMNOJx3333333w0ASkAAAAB/7z6KE/yJQn+pHUEAAAQbOf333333xobzzDz47YIIJ7AXT333332+AaEAAAAAFAFHPOLGpdEFF1sAAAAA2X3333332oDyA58pD4KoJb4Dt7333333wECw8AAAADQsAAdABJqEFJUAAAAFRe/3333333FaLf8A/PqAC6CC+CqG99999998OR2pAAAAAjz7yAAA0FM1iAAAAtaH99999994i8D/AP8A/wD/AAgqggtgtEn/AH33333xswRMEAAAAAAAAAAAAAAAAAABgYN33333332MrQB//wD/AKgHggggrgLIvPffffffG5IPzgAAAAAAAAAAAAAAABCC/wBX3333333yPZKxD/8A6gCrDDDDSuSsZ999999988LdesAAAAAAAAAAAAAAF9GS999999998hDSu2IAAAWyjDDDDDXuAD099999999s7XPqLAAAAAAAAAAAPL6jN99999999r8DDfOy2OSiOH6yy2LDz/OO0999999998MIi06APBAAAAAfoqWNd999999998DCyLT/ACwwwx/+ggAAktjw888vfffffffffffH+GyoRnuoW3nvfffffffffffBcPDkjm9/73+8wDXffCAAstju2/fffffffffffffffffffffffffffffffffOAAcdLAMjjjjnsnffffffTDDDDHm/ffffffffffffffffffffffffffffffeIDXXTQUbSMAMAAAPffffffcccccQQRNPfffffffffffffffffffffffffffPbvffffbSUdbTTTXfQccdPPfSQQQQXffTs/ffffffffffffffffffffffffffHfccQQcfbSQcffeYQQAAAMNPKAQQXffeANgtPfffffffffffffffffffffOd/8QQQQQQUfaQQQcQQQcMMMLCEPDAANPPPDDHHA9PfffffffffffffffffOaLvYQQQQQQQQVaQQQQQQQcMMMDGMDMNDAMMPPPMMAMamvPffffffffffffFPPvffTQQQQQQQRfYQQSTQSQdPPPIHMDMDGMDDDDDDDTTTWQFFeKmMMPYlIbWsYQQQcffbSQQTTfeQRffffbQQAAAHKHIHIHMBDHPPLTQUccdTScdbfbbTeccTTTTTTTQQccdeccYRXeYQQccfaAAAPCPFKFKBPADDDXfffeMpjssrjigjjmssjjjjDDHOMMMDDPMMJDXMMMPLDBHvLGtmKJECNKFOIQRTTjnspnusjjPPrjgtvjgggghjvussogksstjjuntjjssxzz050265NELELAHfesgjlv8x3+8888/zwV+888jvvrggw0/4wwwx/8A/wD/AAhjn+888z82z555FCPAfeogg3+z+5zvu887z07y9/zyz/8A+M8//PPPPP8APPPPTznPjP7z3P3bbnnmg0UJ/qCF/hA8AU8wwwA8oE4Ac8y6+uOSy+OOCCCCCCOKCW+CCfjDjBdhffffeccAh+CD/CAeiC+DD/8Aw3ononogggAnvogvvIAAAgggggnvgnvv/9oADAMBAAIAAwAAABCMMOIIL6p6pbr7oIZzz7rLAzzzCEU/nMUxzDDDDDDDDDDDDIwwxjDAQwzzwAAAMMIIJ75boL6boIb7Jq57zjAAAx3O9/vMQ5nHDDDDDDDDDz4wwxzjDDDAAQwzwIIII5676Iar8Ib6p77rIAAxzzGf+Md/vM93nDDDDDDLDAAAQwwwwzjDzjCTDwIIIb7p7gbp7Ib6b7oIIZzzDC1+Md/u9/Mc9/rTDDDDDDDDDAwwwwxzwxzzDzAAwxzgTgD2TgXyp7oIZ76IRzzAFf8Aj/zHf7jEc88wwwwwwwwwwwwwwwwwAAEgAM884c4Ad18AU498CC++i+4gAEdznfjVzn//AMQAADDDDDDDDDDDDDDDDDPPPPPOMEBOAHKXaVvFfKAHPhvughBKAtN/cx0eKyx3fPPPPPPPPPPPPPPPPPPPOMPPDPPOAHuHawvuHfAFfJPqgkfE4H//AP8A/wD/AP8A/wC0om8/PPPPPPPPPPPPPPPPNJPAPPPPKBPlv6lv5vaFPaPuggIf/wD/AP8A/wD/AP8A/wD/AP8A/wD/AKR0+888888888888888U88A88040ISszuC/a8JA9876W/8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wDv2THDzzzzzzzzzxzyzjwDxzyyTjBzByYjQnRjPGP/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A+swiACAAAAAAMMIPLHHPEBEJHMDMGJECNOL+/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/APqTzwwsMMMMIIAA0888++y+OWqaWGiYMqh//wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8AqTFsMMMMIwwwoA8886zuTzP3XWWWWCB//wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD/AP8A/wD65QEMMMMPPLPCAEPCVffbdVVVUSawf/8A/wD/AP8A/wD/AP8A/wD7mVlCz3t3/wD/AP8A/wD/AP8A/wD/AP8Ar048sMIAw0c0AA8Z9FJVpp5Vpjj/AP8A/wD/AP8A/wD/AP6zkLoY04hixQfA2/8A/wD/AP8A/wD/AP8A+/DXTzwwBDxwggCusY+IuuvehD//AP8A/wD/AP8A/wCoHR+Vj0zzzzzzwv2Fpn//AP8A/wD/AP8A/wCveLzzwADyjygBtLPP9Nt4e1//AP8A/wD/AP8A62nuX/MfPPPPPPPPPPH81a8//wD/AP8A/wD/AP8AFvPPAAPKPqgJ0z//AOO9cSn/AP8A/wD/AP8A6lcdKljPPPPPPPPPPPPPPIYqu/8A/wD/AP8A/wDrXV88AA8o8sAvieyPSbar/wD/AP8A/wD/AOt6Lp7zzzzzzzzzzzzzzzzzy+ubr/8A/wD/AP8A/u086AA8o+sAXjvLP/Wbi/8A/wD/AP8A6zUnR/PPPPPPPPPPPPPPPPPPPHHO7/8A/wD/AP8A+9XMABTyDzwBumc899en/wD/AP8A/wDqaZzKE888888888888888888888BU7f8A/wD/AP8A/wD6cAJLyzzT69UvPMX2D/8A/wD/AP8AqSYMm88889FBKc088884z7J8888sOUU//wD/AP8A/vHKCS88cM8tF5BB1Jf/AP8A/wD/AKxVYYvPPPNxBxjk/wBg4r1hbYMrXTzwyP1v/wD/AP8A/wDp2OKyS88MocABBB6//wD/AP8A/WM8i18884NhyEdoHnZ7sSsr47sX888hRJ//AP8A/wD/ALmvvggsoshMBvPuIf8A/wD/AP6yXJAPPPORBg7ISpymMhrO88ne6ZtPPBSs+/8A/wD/AP6oDlrvjggpisjjjCv/AP8A/wD67FINPPPA43CgeKd7PxTPPPPMxeyJfPLYE5f/AP8A/wD6kP73vv8A8647I48qL/8A/wD/AOt9iV3zzxvGxqGVhOzzzzzzzyw4jSbzzw90H/8A/wD/AP8A/wA9z/36/wA9vc89L/8A/wD/AP8Arj4B8888WfKv8888888888888rYZf888SrT/AP8A/wD/AP8AiEP/AP8A/wD8vOc8/f8A/wD/AP8A/wCP7FNPPPPI0xFPPPPPPPPPPPLDTU2vPPG459//AP8A/wD6yw//AP8A/wD887zzzv8A/wD/AP8A+0bsnzzzxuxitbzzzzzzzzzzzzsAmXzzxEuOf/8A/wD/APoIPMPPf8c8MMPz/wD/AP8A/wDt+7P8888Pv8Iu888888888884ietK888I7nD/AP8A/wD/APksv8jCsgfOAQY//wD/AP8A/wCgLgDzzzzzNd4TzzzzzzzzzzyVhoc7zzxWtP8A/wD/AP8A/q1fN/NZ9D/tf+N3/wD/AP8A/rI8408888pdZ5c8888x88884/H2eQ888zjj/wD/AP8A/wD+d/3huez7888wpav/AP8A/wD6ibENfPPPEfPv4fPPPB/PPPBgV3SvPPPLESf/AP8A/wD/AKWfLLLIf+fsPM5yD/8A/wD/AOsXwbrzzzyx5Z3NXzz/AKR884+XH+F8886T5r//AP8A/wDuGG+++quOK++6y5B//wD/AP8A/wDV+5/PPPPElqEiHfGwx3OBpdxG1PPPNwz9/wD/AP8A/wCv1sM/8NvOtrKZtzH/AP8A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" alt="Innova Center" style="width:100px;height:100px;border-radius:50%;object-fit:cover;box-shadow:0 4px 20px rgba(0,0,0,.3);margin-bottom:10px">
        <div style="font-size:20px;font-weight:700;letter-spacing:.5px">Innova Center</div>
        <div style="font-size:13px;opacity:.7;margin-top:4px">Control de Stock</div>
      </div>
      <div class="login-box">
        <h2>Iniciar sesión</h2>
        <p>Seleccioná tu usuario e ingresá tu PIN</p>
        <div class="user-grid" id="user-grid"></div>
        <div class="pin-wrap" id="pin-wrap" style="display:none">
          <div style="font-size:12px;color:var(--text-s);text-align:center" id="pin-label">Ingresá tu PIN</div>
          <div class="pin-dots" id="pin-dots">
            <div class="pin-dot"></div><div class="pin-dot"></div>
            <div class="pin-dot"></div><div class="pin-dot"></div>
          </div>
          <div class="numpad" id="numpad"></div>
          <div class="login-err" id="login-err"></div>
        </div>
        <button onclick="seleccionarUsuario(null)" style="width:100%;margin-top:4px;font-size:12px;color:var(--text-s)">← Cambiar usuario</button>
      </div>`;
    document.getElementById('login-screen').classList.remove('hidden');
    initLogin();

  } catch(e) {
    document.getElementById('login-screen').innerHTML=`
      <div style="text-align:center;color:white;max-width:360px;padding:24px">
        <div style="font-size:40px">⚠️</div>
        <div style="font-size:16px;font-weight:700;margin-top:12px">Error de conexión</div>
        <div style="font-size:13px;opacity:.8;margin-top:8px;line-height:1.6">No se pudo conectar con Firebase. Verificá que el firebaseConfig esté bien cargado y que Firestore esté habilitado.<br><br>Error: ${e.message}</div>
        <button onclick="location.reload()" style="margin-top:16px;padding:10px 20px;border-radius:8px;background:white;color:var(--azul);font-weight:700;border:none;cursor:pointer">🔄 Reintentar</button>
      </div>`;
  }
}

// Esperar a que Firebase esté listo
if(window._fbReady){
  cargarDatos(window._db);
} else {
  mostrarCargando('Iniciando...');
  window.addEventListener('firebase-ready', ()=>cargarDatos(window._db), {once:true});
}
</script>
</body>
</html>
