<template>
  <div class="map-container">
    <div id="map" />
  </div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";
import "@/js/leaflet-rotate-src.js";

delete L.Icon.Default.prototype._getIconUrl;
L.Icon.Default.mergeOptions({
  iconRetinaUrl: require("leaflet/dist/images/marker-icon-2x.png"),
  iconUrl: require("leaflet/dist/images/marker-icon.png"),
  shadowUrl: require("leaflet/dist/images/marker-shadow.png"),
});

export default {
  data() {
    return {};
  },
  mounted() {
    var polylinePoints = [
      [19.89588839936505, -101.14837646484375],
      [19.886526032443555, -101.1507797241211],
      [19.88136035171138, -101.14768981933594],
      [19.877808848505918, -101.14562988281249],
      [19.872965761318042, -101.13842010498047],
      [19.846810534206607, -101.14974975585938],
      [19.841966500479668, -101.15489959716797],
      [19.841320618149407, -101.16039276123047],
      [19.835830512275315, -101.16485595703125],
      [19.830986143611504, -101.16588592529297],
      [19.815160176711274, -101.16828918457031],
      [19.796425363822532, -101.16313934326172],
      [19.777365274247924, -101.15730285644531],
      [19.76896518881589, -101.15798950195312],
    ];

    const map = L.map("map", {
      center: [19.69658457421901, -101.19316002784888],
      maxBounds: [
        [20.53903525924762, -102.71705180775498],
        [17.70576149807073, -98.73488640277418],
      ],
      bounds: [
        [20.53903525924762, -102.71705180775498],
        [17.70576149807073, -98.73488640277418],
      ],
      maxBoundsViscocity: 1,
      maxZoom: 14,
      minZoom: 9,
      rotate: true,
      touchRotate: true,
      rotateControl: {
        closeOnZeroBearing: false,
      },
    }).setView([19.69658457421901, -101.19316002784888], 9);

    L.tileLayer("https://tiles.stadiamaps.com/tiles/alidade_smooth/{z}/{x}/{y}{r}.png", {
      attribution:
        '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
      noWrap: true,
      maxZoom: 14,
      tileSize: 256,
    }).addTo(map);

    var marker = L.marker([20.13944895126921, -101.18549416295956])
      .addTo(map)
      .bindPopup("Moroleon", { autoClose: false, closeOnClick: false, closeButton: false })
      .openPopup();
    var marker2 = L.marker([19.507314766838956, -101.60705193094152])
      .addTo(map)
      .bindPopup("Patzcuaro", { autoClose: false, closeOnClick: false, closeButton: false })
      .openPopup();
    var marker3 = L.marker([19.780690889637373, -100.65736620776173])
      .addTo(map)
      .bindPopup("azufres", { autoClose: false, closeOnClick: false, closeButton: false })
      .openPopup();

    var polyline = L.polyline(polylinePoints, { className: "my_polyline" }).addTo(map);
  },
};
</script>

<style lang="scss">
#map {
  height: 180px;
  width: 100%;
  height: 100%;
  display: block;
}

.map-container {
  position: absolute;
  left: 1rem;
  right: 1rem;
  top: 1rem;
  bottom: 1rem;

  .my_polyline {
    stroke: green;
    fill: none;
    stroke-dasharray: 10, 10;
    stroke-width: 5;
  }
}
</style>
