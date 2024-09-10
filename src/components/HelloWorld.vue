<template>
  <div class="blind-box-container">
    <header class="store-header">
      <h1 class="store-title">迷你女孩盲盒乐园</h1>
      <p class="store-tagline">在这里，每个盲盒都是一个惊喜！</p>
    </header>

    <nav class="store-nav">
      <ul>
        <li @click="selectTab('home')">主页</li>
        <li @click="selectTab('top')">TOP 盲盒</li>
        <li @click="selectTab('series')">系列</li>
        <li @click="selectTab('contact')">联系客服</li>
      </ul>
    </nav>

    <section v-if="activeTab === 'home'" class="store-about">
      <h2>欢迎光临！</h2>
      <p>迷你女孩盲盒乐园拥有各种类型的盲盒，从普通款到珍贵的史诗款，我们的店铺致力于为您带来无尽的惊喜和乐趣！</p>
    </section>

    <section v-if="activeTab === 'top'" class="top-boxes">
      <h2>Top 盲盒榜</h2>
      <div class="box-types">
        <div class="box-item" v-for="box in topBoxes" :key="box.id" @click="openBoxDetails(box)">
          <img :src="box.image" :alt="box.title" class="box-image" />
          <h4>{{ box.title }}</h4>
          <p>稀有度: {{ box.rarity }} | 概率: {{ box.probability }}%</p>
        </div>
      </div>
    </section>

    <section v-if="activeTab === 'series'" class="showcase">
      <h2>我们的盲盒系列</h2>
      <div class="box-types">
        <div v-for="series in blindBoxSeries" :key="series.id" class="series-item">
          <h3 @click="toggleSeries(series)">{{ series.name }}</h3>
          <div v-if="series.open" class="inner-boxes">
            <div class="box-item" v-for="box in series.boxes" :key="box.id" @click="openBoxDetails(box)">
              <img :src="box.image" :alt="box.title" class="box-image" />
              <h4>{{ box.title }}</h4>
              <p>稀有度: {{ box.rarity }} | 概率: {{ box.probability }}%</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section v-if="activeTab === 'contact'" class="store-about">
      <h2>联系客服</h2>
      <p>如有任何问题，请通过以下方式联系我们：</p>
      <p>邮箱：contact@minigirlbox.com</p>
      <p>电话：123-456-7890</p>
    </section>

    <div v-if="selectedBox" class="box-details">
      <h2>{{ selectedBox.title }}</h2>
      <img :src="selectedBox.image" :alt="selectedBox.title" class="box-image" />
      <p>{{ selectedBox.description }}</p>
      <p>价格: {{ selectedBox.price }}元</p>
      <p>产地: {{ selectedBox.origin }}</p>
      <p>来源: {{ selectedBox.source }}</p>
      <p>稀有度: {{ selectedBox.rarity }}</p>
      <p>概率: {{ selectedBox.probability }}%</p>
      <button @click="closeBoxDetails">关闭</button>
    </div>

    <footer class="store-footer">
      <p>感谢您关注我们的小店，希望每个盲盒都能为您带来欢乐与惊喜！</p>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeTab: 'home',
      selectedBox: null,
      topBoxes: [
        {
          id: 1,
          title: "顶级可爱盲盒",
          image: "https://example.com/images/top-cute-box.jpg",
          rarity: "史诗款",
          probability: 5,
          description: "极具收藏价值的可爱盲盒，收藏家的梦想。",
          price: 99,
          origin: "中国",
          source: "特别版",
        },
        // 其他Top盲盒可以继续添加
      ],
      blindBoxSeries: [
        {
          id: 1,
          name: "可爱系列",
          open: false,
          boxes: [
            {
              id: 1,
              title: "可爱女孩盲盒",
              image: "https://example.com/images/cute-box.jpg",
              rarity: "普通款",
              probability: 70,
              description: "充满梦幻气息的可爱角色。",
              price: 59,
              origin: "中国",
              source: "官方授权",
            },
            {
              id: 2,
              title: "稀有可爱女孩盲盒",
              image: "https://example.com/images/rare-cute-box.jpg",
              rarity: "稀有款",
              probability: 20,
              description: "稀有的可爱角色。",
              price: 69,
              origin: "中国",
              source: "官方授权",
            },
          ],
        },
        {
          id: 2,
          name: "神秘系列",
          open: false,
          boxes: [
            {
              id: 3,
              title: "神秘女孩盲盒",
              image: "https://example.com/images/mystery-box.jpg",
              rarity: "普通款",
              probability: 70,
              description: "探索未知的神秘女孩。",
              price: 59,
              origin: "日本",
              source: "独家代理",
            },
            {
              id: 4,
              title: "稀有神秘女孩盲盒",
              image: "https://example.com/images/rare-mystery-box.jpg",
              rarity: "稀有款",
              probability: 20,
              description: "稀有的神秘角色。",
              price: 69,
              origin: "日本",
              source: "独家代理",
            },
          ],
        },
        // 其他系列可以继续添加
      ],
    };
  },
  methods: {
    selectTab(tab) {
      this.activeTab = tab;
    },
    toggleSeries(series) {
      series.open = !series.open;
    },
    openBoxDetails(box) {
      this.selectedBox = box;
    },
    closeBoxDetails() {
      this.selectedBox = null;
    },
  },
};
</script>
