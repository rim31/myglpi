<template>
  <div>
    <div class="grid-container">
      <div class="menu-icon">
        <strong>&#9776;</strong>
      </div>
      <header class="header">
        <div class="header_search">Search...</div>
        <div class="title">{{titre}}</div>
        <div class="product">{{product}}</div>
        <div class="price">{{price}}</div>
        <div class="header_avatar">Logout</div>
      </header>
      <aside class="aside">
        <div class="aside_close-icon">
          <strong>&times;</strong>
        </div>
        <ul class="aside_list">
          <li class="aside_list-item">Menu item1</li>
          <li class="aside_list-item">Menu item2</li>
          <li class="aside_list-item">Menu item3</li>
          <li class="aside_list-item">Menu item4</li>
          <li class="aside_list-item">Menu item5</li>
        </ul>
      </aside>
      <main class="main">
        <div class="main_overview">
          <div class="overview_card">
            <div class="overview_card-info">Overview</div>
            <div class="overview_card-icon">Card</div>
          </div>
          <div class="overview_card">
            <div class="overview_card-info">Overview</div>
            <div class="overview_card-icon">Card</div>
          </div>
          <div class="overview_card">
            <div class="overview_card-info">Overview</div>
            <div class="overview_card-icon">Card</div>
          </div>
          <div class="overview_card">
            <div class="overview_card-info">Overview</div>
            <div class="overview_card-icon">Card</div>
          </div>
          <div class="overview_card">
            <div class="overview_card-info">Overview</div>
            <Charts />
          </div>
        </div>

        <div class="main_cards">
          <div class="card">
            <UploadCSV msg="monitoring" />
          </div>
          <div class="card">
            <Charts />
          </div>
          <div class="card">Card</div>
        </div>
      </main>
      <footer class="footer">
        <div class="footer_copyright">&copy;2020</div>
        <div class="footer_byline">Made with &hearts; by oseng</div>
      </footer>
    </div>
    <!-- <UploadCSV msg="monitoring" /> -->
  </div>
</template>

<script>
import { bus } from "./main";
import UploadCSV from "./components/UploadCSV.vue";
import Charts from "./components/Charts.vue";
// import Dashboard from "./components/Dashboard.vue";

export default {
  name: "App",
  data() {
    return {
      titre: "mon titre header", ///////BUS/////////
      price: "",
      product: "",
      myBill: [{ products: "", prices: 0 }]
    };
  },
  components: {
    UploadCSV,
    Charts
    // Dashboard
  },
  created() {
    //////////////// en dehors de methods
    bus.$on("changeHeader", data => {
      this.titre = data;
    });
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}

body {
  margin: 0;
  padding: 0;
  color: white;
  box-sizing: border-box;
  font-family: monospace;
  font-size: 15px;
}

.grid-container {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 50px 1fr 50px;

  grid-template-areas:
    "header"
    "main"
    "footer";
  height: 100vh;
}

.header {
  grid-area: header;
  background-color: whitesmoke;
}

.aside {
  grid-area: aside;
  background-color: darkblue;
}

.main {
  grid-area: main;
  background-color: white;
}

.footer {
  grid-area: footer;
  background-color: whitesmoke;
}

/* flexing header and footer*/
.header,
.footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  color: darkblue;
  padding: 0 15px;
}

/* flexing aside */
.aside {
  display: flex;
  flex-direction: column;
  height: 100%;
  width: 240px;
  position: fixed;
  overflow-y: auto;
  z-index: 2;
  transform: translateX(-245px);
}

.aside.active {
  transform: translateX(0);
}

.aside_list {
  padding: 0;
  margin-top: 85px;
  list-style-type: none;
}

.aside_list-item {
  padding: 20px 20px 20px 40px;
  color: #ddd;
}

.aside_list-item:hover {
  background-color: royalblue;
  cursor: pointer;
}

/* Layout for main content overview  and its cards*/
.main_overview {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  border-bottom: 1px solid lightgreen;
}

.overview_card {
  flex-basis: 250px;
  flex-grow: 1;
  margin: 10px 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 20px;
  /* background-color: seagreen; */
  height: 100px;
  border: 1px solid darkblue;
  border-radius: 4px;
  color: darkblue;
}

/* Layout for main-cards section // below main_overview */
.main_cards {
  margin: 10px;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 500px 200px 300px;
  grid-template-areas:
    "card1"
    "card2"
    "card3";
  grid-gap: 10px;
}

.card {
  /* padding: 20px; */
  border: 1px solid tomato;
  border-radius: 4px;
  color: tomato;
  display: inline-block;
}

.card:first-child {
  grid-area: card1;
}

.card:nth-child(2) {
  grid-area: card2;
}

.card:nth-child(3) {
  grid-area: card3;
}

/* responsive layout */
@media only screen and (min-width: 750px) {
  .grid-container {
    display: grid;
    grid-template-columns: 240px 1fr;
    grid-template-rows: 50px 1fr 50px;
    grid-template-areas:
      "aside header"
      "aside main"
      "aside footer";
    height: 100vh;
  }

  .aside {
    display: flex;
    flex-direction: column;
    position: relative;
    transform: translateX(0);
  }

  .main_cards {
    margin: 10px;
    display: grid;
    grid-template-columns: 2fr 1fr;
    grid-template-rows: 200px 300px;
    grid-template-areas:
      "card1 card2"
      "card1 card3";
    grid-gap: 10px;
  }
}

.menu-icon {
  position: fixed;
  display: flex;
  top: 2px;
  left: 8px;
  align-items: center;
  justify-content: center;
  z-index: 1;
  cursor: pointer;
  padding: 12px;
  color: black;
}

.header_search {
  margin-left: 24px;
}

.aside_close-icon {
  position: absolute;
  visibility: visible;
  top: 20px;
  right: 20px;
  cursor: pointer;
}

@media only screen and (min-width: 750px) {
  .aside_close-icon {
    display: none;
  }
}
</style>
