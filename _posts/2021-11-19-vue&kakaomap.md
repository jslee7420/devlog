---
title: "Vue.js + KAKAOMAP"
excerpt: "Vue.js에 카카오맵 연동하기"

categories:
  - Vue.js
tags:
  - [vue]

toc: true
toc_sticky: true

date: 2021-11-20
last_modified_at: 2021-11-20
---

vue.js와 카카오맵의 연동에 대한 자료가 많지 않아 정리해보았습니다.

## 1. API 숨기기

카카오맵 연동시 API KEY를 발급받아 script에서 API를 불러올때 사용해야 합니다.

script 코드에 API KEY를 하드 코딩으로 박아놓으면 외부에 API KEY가 그대로 노출되게 됩니다.

이를 방지하기 위해 환경변수파일(.env)에 API KEY를 넣어두고 script에서는 불러오도록 합니다.

Vue.js cli 환경에서 **루트 디렉토리**에 .env.local 파일을 생성하고 그 안에 API KEY를 넣어둡니다.

이때 변수명에는 반드시 VUE*APP*가 붙어야합니다.

```
VUE_APP_KAKAO_MAP_API_KEY=1fda1de0a051ddf9f0fff2c82fe04521
```

## 2. 카카오 맵이 표시될 div 태그 생성

```html
<template>
  <div>
    <div id="map"></div>
  </div>
</template>
```

## 3. mounted 작성

```html
<script>
  export default {
    mounted() {
      if (window.kakao && window.kakao.maps) {
        this.initMap();
      } else {
        const script = document.createElement("script");
        /* global kakao */
        script.onload = () => kakao.maps.load(this.initMap);
        script.src = `//dapi.kakao.com/v2/maps/sdk.js?autoload=false&appkey=${process.env.KAKAO_MAP_API_KEY}`;
        document.head.appendChild(script);
      }
    },
  };
</script>
```

## 4. initMap() 메소드 작성

```html
<script>
  export default {
    methods: {
      initMap() {
        var container = document.getElementById("map"); //지도를 담을 영역의 DOM 레퍼런스
        var options = {
          //지도를 생성할 때 필요한 기본 옵션
          center: new kakao.maps.LatLng(33.450701, 126.570667), //지도의 중심좌표.
          level: 3, //지도의 레벨(확대, 축소 정도)
        };

        var map = new kakao.maps.Map(container, options); //지도 생성 및 객체 리턴
        const markerPosition = new kakao.maps.LatLng(
          35.19656853772262,
          129.0807270648317
        );

        const marker = new kakao.maps.Marker({
          position: markerPosition,
        });
        marker.setMap(map);
      },
    },
  };
</script>
```

## 전체 소스 코드

```html
<template>
  <div id="map"></div>
</template>

<script>
  export default {
    mounted() {
      if (window.kakao && window.kakao.maps) {
        this.initMap();
      } else {
        const script = document.createElement("script");
        /* global kakao */
        script.onload = () => kakao.maps.load(this.initMap);
        script.src = `//dapi.kakao.com/v2/maps/sdk.js?autoload=false&appkey=${process.env.KAKAO_MAP_API_KEY}`;
        document.head.appendChild(script);
      }
    },
    methods: {
      initMap() {
        var container = document.getElementById("map"); //지도를 담을 영역의 DOM 레퍼런스
        var options = {
          //지도를 생성할 때 필요한 기본 옵션
          center: new kakao.maps.LatLng(33.450701, 126.570667), //지도의 중심좌표.
          level: 3, //지도의 레벨(확대, 축소 정도)
        };

        var map = new kakao.maps.Map(container, options); //지도 생성 및 객체 리턴
        const markerPosition = new kakao.maps.LatLng(
          35.19656853772262,
          129.0807270648317
        );

        const marker = new kakao.maps.Marker({
          position: markerPosition,
        });
        marker.setMap(map);
      },
    },
  };
</script>

<style scoped>
  #map {
    width: 100%;
    height: calc(100vh - 110px);
  }
</style>
```
