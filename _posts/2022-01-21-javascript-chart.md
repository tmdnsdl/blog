---
title: "Javascript 차트 만들기"
date: 2022-01-21
categories: Javascript
---

### Javascript 차트 만들기

---

Javascript의 라이브러리인 chart.js를 이용하여 데이터 차트를 구현해보자.

<https://www.chartjs.org/docs/latest/>

---

**Html**

```
<script src="resources/js/chart_3.6.2.min.js"></script>
<script src="resources/js/chartjs-plugin-datalabels.min.js"></script>
<div>
    <canvas id="myChart" width="400" height="400"></canvas>
</div>
```

스크립트에 chart.js 파일 경로를 설정해준다.
차트를 넣을 영역에 캔버스에 id 값과 크기를 설정한다.

---

**Javascript**

```
// 차트 데이터 설정
const data = {
        labels: ['품질', '설비', '생산', '물류', '인사', '연구개발'], // x축 데이터
        datasets: [{
            label: 'my chart', // 범례 타이틀
            data: [12, 19, 3, 5, 2, 3], // y축 데이터
            backgroundColor: [ // 바 색상
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [ // 바 테두리 색상
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1, // 바 테두리 굵기
            datalabels : { // 바 내부 데이터 설정
                color : '#616161',
                font : {
                    size : 12
                },
                padding : {
                    bottom : 5
                }
            }
        },
        {
            type : "line",
            label: "data",
            data : [20,27,28,15,33,29],
            borderColor : 'rgb(54, 162, 235)',
            backgroundColor : "rgb(54,162,235)",
            borderWidth : 1,
            fill : false, // 음영 채우기
            datalabels : {
                display :false
            }
        }
        // datasets 은 다중 데이터 지정 가능
        ]
    }

// 차트 설정
const config = {
    plugins : [ChartDataLabels], // datalabels 플러그인 추가
    type: 'bar', // line, bar, doughnut, pie
    data : data,
    options: {
        responsive : false, // 반응형 차트 설정
        maxBarThickness : 20, // bar 굵기 설정
        scales: {
            x: {
	                grid : {
	                	display : false // 눈금 선 표시 여부
	                },
	                axis : 'x',
	                ticks: {
	                    minRotation: 25 // 표시되는 라벨 기울기 설정
	                 },
                    stacked : true // 누적 막대 그래프 여부
	            },
            y: {
	            	grid : {
	                	display : true
	                },
	                axis : 'y',
	                ticks: {
	                    stepSize : 2 // 라벨 값 표시 단위 (2,4,6..)
	                 },
	            },
        },
        indexAxis : 'x', // 가로,세로 축 변경
        plugins : {
            legend : {
                display : false // 범례 추가
            },
            title : {
                display : true, // title
                text : 'chart'
            },
            datalabels : {
                // datalabel 값 위치 설정
                anchor : 'end', // center, start, end
	            align : 'center' // center, start, end, right, bottom, left, top
            }
        }
    }
}

// 기본 폰트
Chart.defaults.font.family = '폰트';
Chart.defaults.font.size = 14;
Chart.defaults.color = '#ffffff';

// title settings
Chart.defaults.plugins.title.font.size = 20
Chart.defaults.plugins.title.font.style = "normal";
Chart.defaults.plugins.title.color = '#FFFFFF';

// 차트 생성
const ctx = document.getElementById('myChart').getContext('2d'); // 2d 차트
const myChart = new Chart(ctx, config);
```

차트의 모양, 데이터를 설정하여 내가 원하는 차트를 그려낼 수 있다.

<https://www.chartjs.org/docs/3.6.2/>에서 옵션, 설정 등에 대해 더 많은 정보를 얻을 수 있다.
