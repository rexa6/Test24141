<template>
  <div class="tab-content">
    <div class="profile">
      <img class="avatar" src="https://via.placeholder.com/100" alt="User Avatar" />
      <div class="info">
        <p><strong>ID:</strong> 132412215</p>
        <p><strong>Username:</strong> user_name</p>
        <p><strong>Баланс:</strong> 500 TON</p>
        <p><strong>Подарки:</strong> 12</p>
      </div>
    </div>

    <h2>Инвентарь 🎁</h2>
    <div class="gifts-grid">
      <div class="gift" v-for="gift in gifts" :key="gift.id">
        <img :src="gift.image" alt="Gift" />
        <p>Цена: {{ gift.price }} TON</p>
        <div class="buttons-vertical">
          <button @click="useGift(gift)">Использовать</button>
          <button @click="sellGift(gift)">Продать</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gifts: [
        { id: 1, image: "https://via.placeholder.com/100", price: 50 },
        { id: 2, image: "https://via.placeholder.com/100", price: 30 },
        { id: 3, image: "https://via.placeholder.com/100", price: 20 },
        { id: 4, image: "https://via.placeholder.com/100", price: 15 },
      ],
    };
  },
  methods: {
    useGift(gift) {
      alert(`Использовать подарок ID: ${gift.id}`);
    },
    sellGift(gift) {
      alert(`Продать подарок ID: ${gift.id}`);
    },
  },
};
</script>

<style scoped>
.tab-content {
  width: 100%;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.profile {
  display: flex;
  align-items: center;
  margin-bottom: 30px;
}

.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin-right: 20px;
}

.info p {
  margin: 5px 0;
  font-size: 1.1rem;
}

.gifts-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

.gift {
  border: 1px solid #ccc;
  border-radius: 12px;
  padding: 15px;
  text-align: center;
  background: rgba(255, 255, 255, 0.08);
  font-size: 1rem;
}

.gift img {
  width: 100px;
  height: 100px;
  margin-bottom: 10px;
}

.buttons-vertical {
  display: flex;
  flex-direction: column;
  gap: 7px;
  margin-top: 10px;
}

.buttons-vertical button {
  padding: 8px 12px;
  font-size: 0.9rem;
  cursor: pointer;
  background-color: #8a2be2;
  color: white;
  border: none;
  border-radius: 5px;
}

.buttons-vertical button:hover {
  background-color: #6a1bb0;
}
</style>
