<template>
  <div class="fullpage-container">
    <div class="fullpage-wp" v-fullpage="opts" ref="example">
      <div class="page-1 page">
        <section>
          <!-- <v-parallax src="./static/logo.png"> -->
          <v-layout column align-center justify-center>
            <p class="part-1"></p>
            <h1 class="brand-heading" v-animate="{value: 'bounceInLeft'}">안녕하세요</h1>
            <p class="intro-text" v-animate="{value: 'bounceInRight'}">주주커플의 모바일 청첩장 입니다.<br />방문해주셔서 감사합니다.</p>
          </v-layout>
        </section>
      </div>
      <div class="page-2 page">
        <p class="part-2"></p>
        <h1 class="part-2" v-animate="{value: 'bounceInLeft', delay: 0}">주동훈 & 이주미</h1>
        <br />
        <pre class="part-2" v-animate="{value: 'bounceInRight', delay: 100}">
평생을 같이하고 싶은 사람을 만났습니다.
서로 아껴주고 이해하며
사랑 베풀며 살고 싶습니다.
저희 약속 위에 따뜻한 격려로 축복해
주셔서 힘찬 출발의 디딤이 되어 주십시오.
        </pre>
        <p class="part-2" v-animate="{value: 'bounceInLeft', delay: 200}">주성돈, 우연단 의 장남 동훈<br />이남종, 송복자 의 장녀 주미</p>
        <br />
        <p class="part-2" v-animate="{value: 'bounceInRight', delay: 400}">2018년 5월 26일 (토요일) 오후 1시<br />그랜드컨벤션웨딩 1층 컨벤션홀</p>
      </div>
      <div class="page-3 page">
        <v-carousel :cycle="false" hide-delimiters style="height:100%" class="carousel-panel">
          <v-carousel-item v-for="(item, i) in items" :src="item.src" :key="i"></v-carousel-item>
        </v-carousel>
      </div>
      <div class="page-4 page">
        <p class="part-4"></p>
        <h2 class="part-4" v-animate="{value: 'bounceInLeft', delay: 0}">오시는길</h2>
        <p class="part-4"><div id="map" style="width:80%;height:60%;"></div></p>
        <p class="part-4" v-animate="{value: 'bounceInRight', delay: 0}">그랜드컨벤션웨딩 TEL 054-637-1000<br />경북 영주시 원당로 80<br />(경북 영주시 휴천3동 40-2)</p>
        <button type="button" class="btn btn-outline-primary" v-on:click="kakaoNaviCall">카카오내비</button>
        <button type="button" class="btn btn-outline-secondary">T맵 내비</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Main',
  mounted () {
    var map = new naver.maps.Map('map');
    var myaddress = '경북 영주시 원당로 80';// 도로명 주소나 지번 주소만 가능 (건물명 불가!!!!)
    naver.maps.Service.geocode({address: myaddress}, function(status, response) {
      if (status !== naver.maps.Service.Status.OK) {
        console.log(myaddress + '의 검색 결과가 없거나 기타 네트워크 에러');
        return;
      }
      var result = response.result;
      // 검색 결과 갯수: result.total
      // 첫번째 결과 결과 주소: result.items[0].address
      // 첫번째 검색 결과 좌표: result.items[0].point.y, result.items[0].point.x
      var myaddr = new naver.maps.Point(result.items[0].point.x, result.items[0].point.y);
      map.setCenter(myaddr); // 검색된 좌표로 지도 이동
      // 마커 표시
      var marker = new naver.maps.Marker({
        position: myaddr,
        map: map
      });
      // 마커 클릭 이벤트 처리
      naver.maps.Event.addListener(marker, "click", function(e) {
        if (infowindow.getMap()) {
          infowindow.close();
        } else {
          infowindow.open(map, marker);
        }
      });
      // 마크 클릭시 인포윈도우 오픈
      var infowindow = new naver.maps.InfoWindow({
        content: '<h5>그랜드컨벤션웨딩</h5> TEL 054-637-1000 <br />경북 영주시 원당로 80'
      });
    });

    Kakao.init('20ab922a498f1485fcd5d70954b6a5c9');
  },
  data () {
    return {
      opts: {
        start: 3,
        dir: 'v',
        duration: 100,
        beforeChange: function (prev, next) {
        },
        afterChange: function (prev, next) {
        }
      },
      items: [
        { src: './static/image/01first.jpg' },
        { src: './static/image/02.jpg' },
        { src: './static/image/03.jpg' }
      ]
    }
  },
  methods: {
    moveNext () {
      this.$refs.example.$fullpage.moveNext() //Move to the next page
    },
    kakaoNaviCall () {
      Kakao.Navi.start({
        name: "그랜드컨벤션웨딩",
        x: 128.623455,
        y: 36.819962,
        coordType: 'wgs84'
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.fullpage-container {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  padding-top: 60px;
}
.page-1 > img {
  height: 100%;
}
.carousel-panel img {
  width: 100%;
}
#map {
  position: absolute;
	top:0;
	bottom: 0;
	left: 0;
	right: 0;
  margin: auto;
}
</style>
