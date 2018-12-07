# [팀 프로젝트] 간첩을 찾아라!
---
<img src="https://user-images.githubusercontent.com/19260410/49653295-d1a36a00-fa77-11e8-8a8a-9b1ee6c472b7.PNG" width="500"></img>
## [ [시연 영상 링크](https://youtu.be/GoBE7Rcq_ks) ]
<br></br>
# 설명
---
- 서울시 자전거 대여소 좌표 정보 API를 활용하여 간첩의 위치를 임의로 설정하고 다음 지도 API를 통해 보여준다. 
- 자신의 촉과 아이템을 활용하여 설정된 간첩 수의 50% 이상을 찾아내면 클리어된다.
- 클리어 후 잡은 간첩들의 이름을 카카오톡 메신저를 통해 전송할 수 있다.
<br></br>
# 참여 인원
---
- 5명
<br></br>
# 지원
---
- Chrome Extension
- Daum 지도 Javscript API
- KakaoLogin API
- KakaoLink API
- 서울시 좌표기반 근접 지하철역 정보 API 
- 서울시 자전거 대여서 좌표 정보 API
<br></br>
# 사용 언어
---
- Java
- Javascript
<br></br>
# 환경
---
- Eclipse version: Photon Release (4.8.0)
- Aws EC2 Server
<br></br>
# 개인 역할
---
- javascript SDK를 이용한 카카오 로그인 API를 통해 로그인 구현.
- javascript SDK를 이용한 카카오 링크 API를 통해 잡은 간첩들의 이름을 메신저로 전송하는 기능 구현.
- 다음 지도 API와 서울시 좌표기반 근접 지하철역 정보 API를 통해 역 근처 간첩 위치 조회 서비스 구현.
~~~javascript
// 간첩 위치 서비스를 위한 ajax 통신 코드
$('#search').on('click', function() {
	var code = '';
	var name = $('#name').val(); // 입력한 역 이름
	
	$('#stNameTx').html('<span style="color:red">검색 중입니다...</span>');
	
	$.ajax({
		url: 'json/station.json', // 서울시 지하철 역 좌표 가져오기.
		dataType: 'json',
				
		success: function(data){
			for (var i = 0; i < data.DATA.length; i++) {
						
				// 입력한 역 이름과 JSON 객체에 저장된 역 이름을 비교하여 일치할 경우 역 코드 리턴
				if (data.DATA[i].station_nm == name) {
					code = data.DATA[i].station_cd;
				}
			}
			getLocation(code); // 역 코드를 매개변수로 넘겨줌. 
		}
	});
});
getLocation(){
	$.ajax({
		// URL + 파라미터(code)로 요청 ( 코드에 따른 지하철역의 위치와 이름 찾기 )
		url : 'http://openAPI.seoul.go.kr:8088/486a7359726d6b6d313135497051644c/xml/SearchLocationOfSTNByIDService/1/5/' + code,
		success : function(data) {
			// 지도 표시
		}
	});
}
~~~
<br></br>
~~~JSON
"DATA": [{
	"line_num": "8",
	"cyber_st_code": "2818",
	"xpoint_wgs": "37.492522",
	"ypoint": "1108579",
	"ypoint_wgs": "127.118234",	
	"xpoint": "525992",
	"station_cd": "2818",
	"station_nm": "가락시장",
	"fr_code": "817"
}]
~~~

