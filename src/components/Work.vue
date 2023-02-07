<script>
import axios from "axios";

export default {
  data() {
    return {
      work: [],
    };
  },
  created() {
    axios
      .get("/work.json")
      .then((response) => {
        this.work = response.data.items;
      });
  },
  methods: {
    getBadgeColor(badge) {
      const badgeColors = {
        "Client": "#862E9C",
        "Active": "#087F5B",
      }

      if (badge in badgeColors) {
        return badgeColors[badge];
      } else {
        return "#555";
      }
    },
    goToURL(url) {
      window.location.href = url;
    }
  }
};
</script>

<template>
  <div class="workItemsList">
    <div class="workItem" v-for="workitem in work">
      <img 
        class="workImage"
        v-if="workitem.featureImage"
        :src="workitem.featureImage"
        :alt="workitem.title"
      />
      <div class="workItemText">
        <div class="workItemHeader">
          <p class="title">{{ workitem.title }}</p>
          <div class="year" v-if="workitem.year">
            <p>{{ workitem.year }}</p>
          </div>
        </div>
        <div class="badges">
          <div
            class="badge"
            v-for="technology in workitem.technologies"
            :style="{ backgroundColor: getBadgeColor(technology) }"
          >
            <p>{{ technology }}</p>
          </div>
        </div>
        <p class="body">{{ workitem.body }}</p>
        <div
          class="links"
          v-if="Object.keys(workitem?.links || []).length > 0"
          v-for="link in Object.keys(workitem.links)"
        >
          <a
            :href="workitem.links[link]"
            target="_blank"
            rel="noopener noreferrer"
          >
            {{ link }}
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
p {
  color: #fff;
  margin: 0;
}

.workItemsList {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  grid-template-rows: auto;
  grid-gap: 20px;
  margin-top: 30px;
}

.workItem {
  width: 100%;
  background-color: #333;
  border-radius: 30px;
  padding: 30px;
  display: flex;
  flex-direction: row;
}

.workItemText {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.workItemHeader {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.workImage {
  max-width: 300px;
  height: auto;
  object-fit: cover;
  border-radius: 15px;
  margin-right: 20px;
}

.badges {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.badge {
  background-color: #555;
  border-radius: 30px;
  padding: 5px 10px;
  margin-right: 10px;
  margin-top: 10px;
}

.title {
  font-size: 1.75rem;
  font-weight: 400;
}

.body {
  margin-top: 10px;
}

.links {
  margin-top: 10px;
}

.links a {
  color: #ccc;
  margin-right: 10px;
  transition: color 0.2s ease;
}

.links a:hover {
  color: #fff;
}

@media screen and (max-width: 768px) {
  .workItem {
    flex-direction: column;
  }

  .workImage {
    max-width: 100%;
    margin-right: 0;
    margin-bottom: 20px;
  }
}
</style>