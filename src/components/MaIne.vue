<template>
  <div id="map" style="width: 600px; height: 400px"></div>
</template>

<script>
export default {
  mounted() {
    // Используем ymaps.ready для ожидания загрузки API Яндекс.Карт
    ymaps.ready(() => {
      // Инициализируем карту
      const myMap = new ymaps.Map("map", {
        center: [55.76, 37.64], // Москва
        zoom: 10, // Уровень масштабирования
      });

      // Добавляем метку
      const myPlacemark = new ymaps.Placemark(
        [55.7558, 37.6173],
        {
          // Свойства метки
          hintContent: "Московский Кремль", // Подсказка при наведении
          balloonContent: "<b>Московский Кремль</b><br/>Исторический центр Москвы", // Содержимое балуна
        },
        {
          // Опции метки
          iconLayout: "default#image", // Используем стандартный икон-лейаут
          iconImageHref: "./src/images/exel.jpg", // Замените './path/to/your/icon.png' на реальный путь

          iconImageSize: [21, 31], // Размер иконки
          iconImageOffset: [-10, -31], // Смещение иконки
        }
      );

      // Добавляем метку на карту
      myMap.geoObjects.add(myPlacemark);

      // Добавляем контрол поиска
      const searchControl = new ymaps.control.SearchControl({
        options: {
          provider: "yandex#search",
          useMapBounds: true,
          position: {
            bottom: "5px",
            right: "5px",
          },
        },
      });
      myMap.controls.add(searchControl);
    });
  },
};
</script>

<style scoped>
/* Optional styles for the map container */
#map {
  border: 1px solid #ccc;
}
</style>
