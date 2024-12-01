<template>
  <div id="app" class="app">
    <div>
      <Header @search="handleSearch"></Header>
      <div class="container">
        <h1 class="title">Картины эпохи Возрождения</h1>
        <div v-if="filteredPaintings.length === 0" class="no-results">
          Ничего не найдено
        </div>
        <div class="card-list" v-else>
          <Card
            v-for="(item, index) in filteredPaintings"
            :key="index"
            :title="item.title"
            :description="item.description"
            :beforeDiscount="item.beforeDiscount"
            :price="item.price"
            :imageSrc="item.imageSrc"
            :sold="item.sold"
            :images="item.images"
          />
        </div>
      </div>
    </div>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Card from "./components/Card.vue";

export default {
  name: "app",
  components: {
    Header,
    Footer,
    Card,
  },
  data() {
    return {
      paintings: [
        {
          title: "«Рождение Венеры» Сандро Боттичелли",
          description: `На берегу Венеру готовится встретить пора весны и цветения Талло, которая держит в руках пурпурный плащ, чтобы закутать новорождённую богиню. artchive.ru. Нежное лицо героини имеет большое сходство с лицами мадонн, а её поза и очертания тела — с древнегреческими скульптурами. Так живописец подчеркнул взаимосвязь античности и христианства.`,
          beforeDiscount: `2 000 000 $`,
          price: `1 000 000 $`,
          imageSrc: "./src/img/1.png",
          images: [
            "./src/img/1.png",
            "./src/img/slide2.jpg",
            "./src/img/slide2-2.jpeg",
          ],
        },
        {
          title: "«Тайная вечеря»  Леонардо да Винчи",
          description: `На картине представлен момент, описанный в Новом Завете, когда Иисус Христос сообщает, что один из его учеников предаст его. Шедевр Леонардо передаёт эмоциональную реакцию апостолов, услышавших эту новость.`,
          price: `3 000 000 $`,
          imageSrc: "./src/img/2.png",
          images: [
            "./src/img/2.png",
            "./src/img/slide1.jpg",
            "./src/img/slide1-2.jpg",
          ],
        },
        {
          title: "«Сотворение Адама» Микеланджело",
          description: `Фреска изображает момент передачи жизни первому человеку, Адаму, от Бога. Произведение олицетворяет собой момент сотворения человека по образу и подобию Божьему, что является ключевым элементом христианской идеологии.`,
          beforeDiscount: `6 000 000 $`,
          price: `5 000 000 $`,
          imageSrc: "./src/img/3.png",
          images: [
            "./src/img/3.png",
            "./src/img/slide3.jpg",
            "./src/img/slide3-2.jpg",
          ],
        },
        {
          title: "«Урок анатомии» Рембрандт",
          description: `Рембрандт создал картину «Урок анатомии доктора Тульпа после переезда из Лейдена в Амстердам. Переезд был рискованным решением, но художник решился не него, так как это был один из самых богатых городов Европы. Соответственно, и заказчиков полотен там было достаточно.`,
          price: `Продана на аукционе`,
          imageSrc: "./src/img/4.png",
          images: ["./src/img/4.png", "./src/img/slide4.jpg"],
          sold: true,
        },
      ],
      searchQuery: "",
    };
  },
  computed: {
    filteredPaintings() {
      return this.paintings.filter((item) =>
        item.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    handleSearch(query) {
      this.searchQuery = query;
    },
  },
};
</script>

<style>
.container {
  max-width: 1240px;
  margin: 0 auto;
}

.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.title {
  font-size: 24px;
  font-weight: 700;
  margin: 45px 0 40px;
}

.card-list {
  display: flex;
  flex-wrap: wrap;
  gap: 32px;
  margin-bottom: 40px;
}

@media (max-width: 1440px) {
  .container {
    padding: 0 40px;
  }
}

@media (max-width: 768px) {
  .container {
    padding: 0 14px;
  }

  .title {
    text-align: center;
    font-size: 20px;
    margin-bottom: 20px;
  }

  .card-list {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
    margin-bottom: 20px;
  }
}
</style>
