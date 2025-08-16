<template>
  <div class="tab-content">
    <div class="profile">
      <!-- Блок с основной информацией -->
      <div class="user-info">
        <img class="avatar" src="https://via.placeholder.com/100" alt="User Photo">
        <div class="details">
          <p><strong>ID:</strong> 132412215</p>
          <p><strong>Username:</strong> @username</p>
          <p><strong>Баланс:</strong> 100 TON</p>
          <p><strong>Подарки:</strong> 8</p>
        </div>
      </div>

      <!-- Инвентарь с подарками -->
      <div class="inventory">
        <h2>Инвентарь 🎁</h2>
        <div class="gifts-grid">
          <div class="gift" v-for="n in 6" :key="n">
            <img src="https://via.placeholder.com/80" alt="Gift">
            <p>Цена: {{ n * 10 }} TON</p>
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
  padding: 10px;
  text-align: center;
  background: #f9f9f9;
}

.gift img {
  width: 80px;
  height: 80px;
  margin-bottom: 5px;
}

/* Кнопки вертикально под подарком */
.buttons-vertical {
  display: flex;
  flex-direction: column;
  gap: 5px;
  margin-top: 5px;
}

.buttons-vertical button {
  padding: 5px 10px;
  font-size: 0.8rem;
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
