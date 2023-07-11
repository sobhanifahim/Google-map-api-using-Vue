<template>
<div>
  <GoogleMap api-key="AIzaSyBbK7YUH-Ca7iQNBvTEBg-PHzA12tgbQ4E" style="width: 100%; height: 100vh" :center="center" :zoom="13">
    
    <MarkerCluster>
      <Marker v-for="(location, i) in markers" :options="{ position: location.position }" :key="i"> 
            <InfoWindow>
                  <div id="content">
                      <h3>{{location.Address}}</h3>
                </div>
            </InfoWindow>
      </Marker>  
    </MarkerCluster>
    <Polyline :options="lines" />
    <Polygon :options="Triangle" />
  </GoogleMap>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import { GoogleMap, Marker,MarkerCluster,Polyline ,Polygon,InfoWindow} from "vue3-google-map";

export default defineComponent({
  components: { GoogleMap, Marker,MarkerCluster,Polyline,Polygon,InfoWindow },
  setup() { 
    const center = { lat: 23.803, lng: 90.418 };
      const markers = [
      {position:{ lat: 23.741, lng: 90.418 }, Address:"Motijheel"},
      {position:{ lat: 23.754, lng: 90.415 }, Address:"Malibag"},
      {position:{ lat: 23.813, lng: 90.424 },Address:"Jamuna FP"},
      {position:{ lat: 23.741, lng: 90.418 },Address:"Motijheel"},
    ];
    const lines = {
      paths: markers.map(marker => marker.position),
      geodesic: true,
      strokeColor: "#FF0000",
      strokeOpacity: 1.0,
      strokeWeight: 2,
    };
    const Triangle = {
      paths: markers.map(marker => marker.position),
      strokeColor: "#FF0000",
      strokeOpacity: 0.8,
      strokeWeight: 2,
      fillColor: "#FF0000",
      fillOpacity: 0.35,
    };
 

    return { center, markers,lines,Triangle};
  },
});
</script>
