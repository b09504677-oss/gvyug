<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MM2 Shop</title>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: Arial, sans-serif;
    background: #0b0d12;
    color: white;
    min-height: 100vh;
}

header {
    background: #11141c;
    border-bottom: 1px solid #292e3b;
    padding: 18px 30px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: sticky;
    top: 0;
    z-index: 100;
}

.logo {
    font-size: 25px;
    font-weight: bold;
}

.logo span {
    color: #ff334d;
}

.balance {
    background: #1b202b;
    padding: 12px 18px;
    border-radius: 12px;
    font-weight: bold;
}

#tokens {
    color: #ffd43b;
}

.container {
    max-width: 1200px;
    margin: auto;
    padding: 30px 20px;
}

.hero {
    background: linear-gradient(135deg, #191d28, #10131a);
    border: 1px solid #292e3b;
    border-radius: 20px;
    padding: 35px;
    margin-bottom: 25px;
}

.hero h1 {
    font-size: 40px;
    margin-bottom: 10px;
}

.hero p {
    color: #aeb5c3;
    font-size: 17px;
}

.categories {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    margin-bottom: 25px;
}

.category {
    border: 1px solid #343a49;
    background: #171b24;
    color: white;
    padding: 11px 18px;
    border-radius: 10px;
    cursor: pointer;
    transition: .2s;
}

.category:hover,
.category.active {
    background: #ff334d;
    border-color: #ff334d;
}

.section-title {
    margin: 25px 0 15px;
    font-size: 25px;
}

.products {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
    gap: 18px;
}

.card {
    background: #151922;
    border: 1px solid #292e3b;
    border-radius: 16px;
    overflow: hidden;
    transition: .25s;
}

.card:hover {
    transform: translateY(-5px);
    border-color: #ff334d;
}

.skin-image {
    height: 150px;
    background: #202531;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 65px;
}

.card-content {
    padding: 16px;
}

.card h3 {
    margin-bottom: 7px;
}

.rarity {
    font-size: 13px;
    margin-bottom: 12px;
    color: #aaa;
}

.price {
    color: #ffd43b;
    font-weight: bold;
    margin-bottom: 12px;
}

.buy {
    width: 100%;
    border: 0;
    border-radius: 9px;
    padding: 11px;
    background: #ff334d;
    color: white;
    font-weight: bold;
    cursor: pointer;
}

.buy:hover {
    background: #e51f39;
}

.buy:disabled {
    background: #555b68;
    cursor: not-allowed;
}

.inventory {
    margin-top: 40px;
}

.inventory-box {
    background: #11141c;
    border: 1px solid #292e3b;
    border-radius: 16px;
    padding: 20px;
}

.inventory-items {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 12px;
}

.inventory-item {
    background: #1a1f29;
    border-radius: 12px;
    padding: 15px;
    text-align: center;
}

.empty {
    color: #8c94a3;
    padding: 20px 0;
}

.modal {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,.75);
    align-items: center;
    justify-content: center;
    z-index: 500;
}

.modal.show {
    display: flex;
}

.modal-box {
    width: min(420px, 90%);
    background: #171b24;
    border: 1px solid #343a49;
    border-radius: 18px;
    padding: 25px;
    text-align: center;
}

.modal-box h2 {
    margin-bottom: 15px;
}

.modal-box p {
    color: #b8bfcc;
    line-height: 1.5;
    margin-bottom: 20px;
}

.close {
    background: #303644;
    border: 0;
    color: white;
    padding: 10px 18px;
    border-radius: 9px;
    cursor: pointer;
}

footer {
    text-align: center;
    color: #777f8f;
    padding: 40px 20px;
}

@media(max-width:600px) {
    .hero h1 {
        font-size: 30px;
    }

    header {
        padding: 15px;
    }
}
</style>
</head>

<body>

<header>
    <div class="logo">
        🔪 MM2 <span>SHOP</span>
    </div>

    <div class="balance">
        🪙 <span id="tokens">11000</span> жетонов
    </div>
</header>

<main class="container">

    <section class="hero">
        <h1>MM2 Магазин</h1>
        <p>
            Покупай редкие скины за жетоны и собирай свою коллекцию.
        </p>
    </section>

    <div class="categories">
        <button class="category active" onclick="filterSkins('all', this)">
            Все
        </button>

        <button class="category" onclick="filterSkins('Обычный', this)">
            🟢 Обычные
        </button>

        <button class="category" onclick="filterSkins('Легендарный', this)">
            🔵 Легендарные
        </button>

        <button class="category" onclick="filterSkins('Godly', this)">
            🔴 Godly
        </button>

        <button class="category" onclick="filterSkins('Хроматический', this)">
            🌈 Хроматические
        </button>
    </div>

    <h2 class="section-title">🛒 Скины</h2>

    <div id="products" class="products"></div>

    <section class="inventory">
        <h2 class="section-title">🎒 Мой инвентарь</h2>

        <div class="inventory-box">
            <div id="inventory" class="inventory-items"></div>
        </div>
    </section>

</main>

<footer>
    MM2 Shop © 2026
</footer>

<div id="modal" class="modal">
    <div class="modal-box">
        <h2 id="modalTitle">Готово!</h2>
        <p id="modalText"></p>
        <button class="close" onclick="closeModal()">Закрыть</button>
    </div>
</div>

<script>

/* =========================
   НАСТРОЙКИ
========================= */

let tokens = Number(localStorage.getItem("mm2_tokens"));

if (!Number.isFinite(tokens)) {
    tokens = 11000;
}

let inventory = JSON.parse(
    localStorage.getItem("mm2_inventory") || "[]"
);


/* =========================
   СОЗДАНИЕ СКИНОВ
========================= */

const skins = [];


/* Обычные — 20 */

for (let i = 1; i <= 20; i++) {
    skins.push({
        id: "common_" + i,
        name: "Common Knife " + i,
        rarity: "Обычный",
        price: 1000,
        icon: "🔪"
    });
}


/* Легендарные — 15 */

for (let i = 1; i <= 15; i++) {
    skins.push({
        id: "legendary_" + i,
        name: "Legendary Knife " + i,
        rarity: "Легендарный",
        price: 5000,
        icon: "🗡️"
    });
}


/* Godly — 10 */

for (let i = 1; i <= 10; i++) {
    skins.push({
        id: "godly_" + i,
        name: "Godly Knife " + i,
        rarity: "Godly",
        price: 15000,
        icon: "⚔️"
    });
}


/* Хроматические — 5 */

for (let i = 1; i <= 5; i++) {
    skins.push({
        id: "chromatic_" + i,
        name: "Chromatic Knife " + i,
        rarity: "Хроматический",
        price: 20000,
        icon: "🌈"
    });
}


/* =========================
   ОТОБРАЖЕНИЕ
========================= */

function updateBalance() {
    document.getElementById("tokens").textContent =
        tokens.toLocaleString("ru-RU");
}


function renderProducts(list = skins) {

    const container = document.getElementById("products");

    container.innerHTML = "";

    list.forEach(skin => {

        const alreadyOwned =
            inventory.some(item => item.id === skin.id);

        const card = document.createElement("div");

        card.className = "card";

        card.innerHTML = `
            <div class="skin-image">
                ${skin.icon}
            </div>

            <div class="card-content">

                <h3>${skin.name}</h3>

                <div class="rarity">
                    Редкость: ${skin.rarity}
                </div>

                <div class="price">
                    🪙 ${skin.price.toLocaleString("ru-RU")}
                </div>

                <button
                    class="buy"
                    onclick="buySkin('${skin.id}')"
                    ${alreadyOwned ? "disabled" : ""}
                >
                    ${alreadyOwned ? "✓ Уже куплен" : "Купить"}
                </button>

            </div>
        `;

        container.appendChild(card);
    });
}


/* =========================
   ПОКУПКА
========================= */

function buySkin(id) {

    const skin = skins.find(item => item.id === id);

    if (!skin) return;

    if (inventory.some(item => item.id === id)) {
        showModal(
            "Уже есть",
            "Этот скин уже находится в твоём инвентаре."
        );
        return;
    }

    if (tokens < skin.price) {
        showModal(
            "Недостаточно жетонов",
            `Нужно ${skin.price.toLocaleString("ru-RU")} жетонов.`
        );
        return;
    }

    tokens -= skin.price;

    inventory.push({
        id: skin.id,
        name: skin.name,
        rarity: skin.rarity,
        icon: skin.icon,
        equipped: false
    });

    saveData();

    updateBalance();

    renderProducts();

    renderInventory();

    showModal(
        "🎉 Покупка успешна!",
        `${skin.name} добавлен в твой инвентарь.`
    );
}


/* =========================
   ИНВЕНТАРЬ
========================= */

function renderInventory() {

    const container =
        document.getElementById("inventory");

    container.innerHTML = "";

    if (inventory.length === 0) {

        container.innerHTML = `
            <div class="empty">
                Инвентарь пока пуст.
            </div>
        `;

        return;
    }

    inventory.forEach(item => {

        const div = document.createElement("div");

        div.className = "inventory-item";

        div.innerHTML = `
            <div style="font-size:45px">
                ${item.icon}
            </div>

            <strong>${item.name}</strong>

            <div class="rarity">
                ${item.rarity}
            </div>

            <button
                class="buy"
                onclick="equipSkin('${item.id}')"
            >
                ${item.equipped ? "✓ Экипирован" : "Экипировать"}
            </button>
        `;

        container.appendChild(div);
    });
}


/* =========================
   ЭКИПИРОВКА
========================= */

function equipSkin(id) {

    inventory.forEach(item => {
        item.equipped = item.id === id;
    });

    saveData();

    renderInventory();

    const skin = inventory.find(item => item.id === id);

    showModal(
        "⚔️ Скин экипирован",
        `${skin.name} теперь используется твоим игроком.`
    );
}


/* =========================
   ФИЛЬТРЫ
========================= */

function filterSkins(rarity, button) {

    document
        .querySelectorAll(".category")
        .forEach(btn => btn.classList.remove("active"));

    button.classList.add("active");

    if (rarity === "all") {
        renderProducts(skins);
    } else {
        renderProducts(
            skins.filter(skin => skin.rarity === rarity)
        );
    }
}


/* =========================
   СОХРАНЕНИЕ
========================= */

function saveData() {

    localStorage.setItem(
        "mm2_tokens",
        tokens
    );

    localStorage.setItem(
        "mm2_inventory",
        JSON.stringify(inventory)
    );
}


/* =========================
   ОКНО
========================= */

function showModal(title, text) {

    document.getElementById("modalTitle").textContent =
        title;

    document.getElementById("modalText").textContent =
        text;

    document
        .getElementById("modal")
        .classList.add("show");
}


function closeModal() {

    document
        .getElementById("modal")
        .classList.remove("show");
}


/* =========================
   ЗАПУСК
========================= */

updateBalance();

renderProducts();

renderInventory();

</script>

</body>
</html>
