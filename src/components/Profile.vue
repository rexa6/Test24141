<template>
  <div class="tab-content">
    <div class="profile">
      <!-- Блок с основной информацией -->
      <div class="user-info">
        <img class="avatar" :src="user.photo" alt="User Photo">
        <div class="details">
          <p><strong>ID:</strong> {{ user.id }}</p>
          <p><strong>Username:</strong> {{ user.username }}</p>
          <p><strong>Баланс:</strong> {{ user.balance }} TON</p>
          <p><strong>Подарки:</strong> {{ gifts.length }}</p>
        </div>
      </div>

      <!-- Инвентарь с подарками -->
      <div class="inventory">
        <h2>Инвентарь 🎁</h2>
        <div class="gifts-grid">
          <div class="gift" v-for="gift in gifts" :key="gift.id">
            <img :src="gift.image" alt="Gift">
            <p>Цена: {{ gift.price }} TON</p>
            <div class="buttons-vertical">
              <button>Вывести</button>
              <button>Продать</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      telegram_id: null, // будет получен из WebApp
      user: {
        photo: "",
        id: "",
        username: "",
        balance: 0,
      },
      gifts: [],
      apiUrl: "http://100.79.141.81:8000/users/"
    };
  },
  methods: {
    async fetchUser() {
      if (!this.telegram_id) return;
      try {
        const response = await axios.get(`${this.apiUrl}${this.telegram_id}`);
        const data = response.data;
        this.user = {
          id: data.id,
          username: data.username,
          balance: data.balance,
          photo: data.photo
        };
        this.gifts = data.gifts;
      } catch (error) {
        console.error("Ошибка при получении данных юзера:", error);
      }
    },
    withdrawGift(giftId) {
      alert(`Вывести подарок ${giftId}`);
    },
    sellGift(giftId) {
      alert(`Продать подарок ${giftId}`);
    }
  },
  mounted() {
    // Проверяем есть ли WebApp
    if (window.Telegram && window.Telegram.WebApp) {
      const tgUser = window.Telegram.WebApp.initDataUnsafe.user;
      if (tgUser) {
        this.telegram_id = tgUser.id; // автоматически подставляем telegram_id
        this.fetchUser();
      }
    } else {
      console.warn("Это не WebApp Telegram, используем тестовый telegram_id");
      this.telegram_id = 132412215; // тестовый ID для локальной разработки
      this.fetchUser();
    }
  }
};
</script>

<style scoped>
.tab-content {
  width: 100%;
  padding: 20px;
  font-size: 1rem;
}

.profile {
  width: 100%;
}

/* Основная информация */
.user-info {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-bottom: 30px;
}

.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  object-fit: cover;
}

.details p {
  margin: 5px 0;
}

/* Инвентарь */
.inventory h2 {
  margin-bottom: 10px;
}

/* Сетка подарков */
.gifts-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* Ровно 3 подарка в ряду */
  gap: 15px;
}

.gift {
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 15px;
  text-align: center;
  background: rgba(255, 255, 255, 0.08);
}

.gift img {
  width: 100px;
  height: 100px;
  margin-bottom: 10px;
}

/* Кнопки вертикально под подарком */
.buttons-vertical {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 10px;
}

.buttons-vertical button {
  padding: 8px 12px;
  font-size: 0.9rem;
  cursor: pointer;
  background-color: #8a2be2; /* Фиолетовый */
  color: white;
  border: none;
  border-radius: 5px;
}

.buttons-vertical button:hover {
  background-color: #6a1bb0;
}
</style>
