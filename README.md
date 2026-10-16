<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MotoRadar 2026-2027</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  background: #090b10;
  color: #f5f5f5;
  font-family: Arial, sans-serif;
}

header {
  background: #11141d;
  padding: 20px;
  border-bottom: 2px solid #ff3048;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px;
}

.logo {
  font-size: 25px;
  font-weight: bold;
}

.logo span {
  color: #ff3048;
}

nav a {
  color: white;
  text-decoration: none;
  margin: 0 10px;
}

.hero {
  padding: 70px 20px;
  text-align: center;
  background: radial-gradient(circle, #292d40, #090b10 70%);
}

.hero h1 {
  font-size: clamp(35px, 6vw, 65px);
  margin-bottom: 15px;
}

.hero h1 span {
  color: #ff3048;
}

.hero p {
  color: #bdc4d3;
  font-size: 18px;
}

button {
  padding: 12px 17px;
  background: #ff3048;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
}

button:hover {
  background: #d91630;
}

main {
  max-width: 1200px;
  margin: auto;
  padding: 25px 18px 50px;
}

.filters {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin: 20px 0;
}

input, select {
  padding: 12px;
  background: #171b26;
  color: white;
  border: 1px solid #343b4b;
  border-radius: 8px;
  flex: 1;
  min-width: 160px;
}

.grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 20px;
}

.card {
  background: #151923;
  border: 1px solid #303747;
  border-radius: 15px;
  overflow: hidden;
  transition: transform .2s, border-color .2s;
}

.card:hover {
  transform: translateY(-5px);
  border-color: #ff3048;
}

.photo {
  height: 165px;
  background: linear-gradient(135deg, #30374a, #10131b);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 75px;
}

.card-content {
  padding: 18px;
}

.brand {
  color: #36d9ff;
  text-transform: uppercase;
  font-size: 13px;
  font-weight: bold;
}

.card h3 {
  margin-bottom: 8px;
}

.price {
  color: #ff5266;
  font-size: 21px;
  font-weight: bold;
}

.specs {
  color: #c0c6d3;
  line-height: 1.8;
  font-size: 14px;
}

.card button {
  margin-top: 8px;
  margin-right: 5px;
}

.compare {
  margin-top: 50px;
  padding: 20px;
  background: #151923;
  border-radius: 12px;
  overflow-x: auto;
}

table {
  width: 100%;
  border-collapse: collapse;
}

td, th {
  text-align: left;
  padding: 12px;
  border-bottom: 1px solid #343b4b;
}

th {
  color: #36d9ff;
}

footer {
  padding: 25px;
  text-align: center;
  color: #a4adbd;
  border-top: 1px solid #303747;
}

@media (max-width: 800px) {
  .grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 520px) {
  .grid {
    grid-template-columns: 1fr;
  }

  nav a {
    display: inline-block;
    margin: 5px;
  }
}
</style>
</head>

<body>

<header>
  <div class="logo">MOTO<span>RADAR</span> 26/27</div>
  <nav>
    <a href="#inicio">Inicio</a>
    <a href="#catalogo">Catálogo</a>
    <a href="#comparador">Comparador</a>
  </nav>
</header>

<section class="hero" id="inicio">
  <h1>LA VELOCIDAD <span>TIENE NOMBRE</span></h1>
  <p>Descubre, explora y compara motocicletas.</p>
  <a href="#catalogo">
    <button>EXPLORAR MOTOS</button>
  </a>
</section>

<main>
  <section id="catalogo">
    <h2>Catálogo de motocicletas</h2>

    <div class="filters">
      <input id="search" placeholder="Buscar marca o modelo...">

      <select id="category">
        <option value="">Todas las categorías</option>
        <option value="Deportiva">Deportiva</option>
        <option value="Naked">Naked</option>
        <option value="Urbana">Urbana</option>
        <option value="Adventure">Adventure</option>
      </select>

      <select id="sort">
        <option value="default">Orden recomendado</option>
        <option value="price">Menor precio</option>
        <option value="speed">Mayor velocidad</option>
      </select>
    </div>

    <div class="grid" id="motorcycles"></div>
  </section>

  <section class="compare" id="comparador">
    <h2>Comparador de motos</h2>
    <p>Selecciona hasta tres motos para compararlas.</p>
    <div id="comparison">Todavía no has seleccionado motos.</div>
    <button onclick="clearComparison()">Limpiar comparación</button>
  </section>
</main>

<footer>
  MotoRadar 2026–2027 · Precios de referencia en Colombia.
  Verifica las especificaciones con el fabricante.
</footer>

<script>
const motos = [
  {
    id: 1, marca: "Yamaha", modelo: "YZF-R15",
    categoria: "Deportiva", cc: 155,
    velocidad: 140, precio: 16500000
  },
  {
    id: 2, marca: "Yamaha", modelo: "MT-03",
    categoria: "Naked", cc: 321,
    velocidad: 170, precio: 31000000
  },
  {
    id: 3, marca: "Honda", modelo: "CBR500R",
    categoria: "Deportiva", cc: 471,
    velocidad: 180, precio: 42000000
  },
  {
    id: 4, marca: "Honda", modelo: "CB190R",
    categoria: "Naked", cc: 184,
    velocidad: 125, precio: 14500000
  },
  {
    id: 5, marca: "Kawasaki", modelo: "Ninja 400",
    categoria: "Deportiva", cc: 399,
    velocidad: 190, precio: 35000000
  },
  {
    id: 6, marca: "KTM", modelo: "Duke 390",
    categoria: "Naked", cc: 399,
    velocidad: 167, precio: 29000000
  },
  {
    id: 7, marca: "Suzuki", modelo: "Gixxer SF 250",
    categoria: "Deportiva", cc: 249,
    velocidad: 150, precio: 19000000
  },
  {
    id: 8, marca: "Bajaj", modelo: "Pulsar NS200",
    categoria: "Naked", cc: 199,
    velocidad: 136, precio: 12500000
  },
  {
    id: 9, marca: "TVS", modelo: "Apache RTR 200",
    categoria: "Urbana", cc: 197,
    velocidad: 127, precio: 11500000
  },
  {
    id: 10, marca: "BMW Motorrad", modelo: "G 310 R",
    categoria: "Naked", cc: 313,
    velocidad: 143, precio: 30000000
  },
  {
    id: 11, marca: "Kawasaki", modelo: "Z500",
    categoria: "Naked", cc: 451,
    velocidad: 180, precio: 37000000
  },
  {
    id: 12, marca: "Ducati", modelo: "Monster",
    categoria: "Naked", cc: 937,
    velocidad: 240, precio: 75000000
  }
];

const seleccionadas = new Set();

function formatoPrecio(precio) {
  return precio.toLocaleString("es-CO") + " COP";
}

function renderizar() {
  const busqueda =
    document.getElementById("search").value.toLowerCase();

  const categoria =
    document.getElementById("category").value;

  const orden =
    document.getElementById("sort").value;

  let lista = motos.filter(m => {
    const nombre = (m.marca + " " + m.modelo).toLowerCase();

    return nombre.includes(busqueda) &&
      (!categoria || m.categoria === categoria);
  });

  if (orden === "price") {
    lista.sort((a, b) => a.precio - b.precio);
  }

  if (orden === "speed") {
    lista.sort((a, b) => b.velocidad - a.velocidad);
  }

  const contenedor = document.getElementById("motorcycles");

  if (lista.length === 0) {
    contenedor.innerHTML =
      "<p>No encontramos motos con esa búsqueda.</p>";
    actualizarComparacion();
    return;
  }

  contenedor.innerHTML = lista.map(m => `
    <article class="card">
      <div class="photo">🏍️</div>
      <div class="card-content">
        <div class="brand">${m.marca}</div>
        <h3>${m.modelo}</h3>
        <div class="price">${formatoPrecio(m.precio)}</div>
        <div class="specs">
          Categoría: ${m.categoria}<br>
          Cilindrada: ${m.cc} cc<br>
          Velocidad estimada: ${m.velocidad} km/h
        </div>
        <button onclick="comparar(${m.id})">
          ${seleccionadas.has(m.id) ? "Quitar" : "Comparar"}
        </button>
        <button onclick="verDetalles(${m.id})">
          Detalles
        </button>
      </div>
    </article>
  `).join("");

  actualizarComparacion();
}

function comparar(id) {
  if (seleccionadas.has(id)) {
    seleccionadas.delete(id);
  } else {
    if (seleccionadas.size >= 3) {
      alert("Solo puedes comparar tres motos a la vez.");
      return;
    }
    seleccionadas.add(id);
  }
  renderizar();
}

function actualizarComparacion() {
  const lista = motos.filter(m => seleccionadas.has(m.id));
  const contenedor = document.getElementById("comparison");

  if (!lista.length) {
    contenedor.textContent =
      "Todavía no has seleccionado motos.";
    return;
  }

  contenedor.innerHTML = `
    <table>
      <thead>
        <tr>
          <th>Característica</th>
          ${lista.map(m => `<th>${m.marca} ${m.modelo}</th>`).join("")}
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Precio</td>
          ${lista.map(m => `<td>${formatoPrecio(m.precio)}</td>`).join("")}
        </tr>
        <tr>
          <td>Cilindrada</td>
          ${lista.map(m => `<td>${m.cc} cc</td>`).join("")}
        </tr>
        <tr>
          <td>Velocidad estimada</td>
          ${lista.map(m => `<td>${m.velocidad} km/h</td>`).join("")}
        </tr>
        <tr>
          <td>Categoría</td>
          ${lista.map(m => `<td>${m.categoria}</td>`).join("")}
        </tr>
      </tbody>
    </table>
  `;
}

function clearComparison() {
  seleccionadas.clear();
  renderizar();
}

function verDetalles(id) {
  const m = motos.find(moto => moto.id === id);

  alert(
    m.marca + " " + m.modelo +
    "\nCilindrada: " + m.cc + " cc" +
    "\nVelocidad estimada: " + m.velocidad + " km/h" +
    "\nPrecio de referencia: " + formatoPrecio(m.precio) +
    "\n\nVerifica los datos con el fabricante o distribuidor."
  );
}

document.getElementById("search")
  .addEventListener("input", renderizar);

document.getElementById("category")
  .addEventListener("change", renderizar);

document.getElementById("sort")
  .addEventListener("change", renderizar);

renderizar();
</script>

</body>
</html>
