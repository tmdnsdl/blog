---
title: "Javascript 차트 만들기"
date: 2022-01-21
categories: Javascript
---

### Javascript 차트 만들기

---

Javascript의 라이브러리인 chart.js를 이용하여 데이터 차트를 구현해보자.
<https://github.com/chartjs/Chart.js/releases/tag/v3.6.2>에서 다운로드가 가능하다.

---

**Html**

```
<script src="resources/js/chart.js"></script>
<canvas id="myChart" width="400" height="400"></canvas>
```

footer에 chart.js 파일 경로를 설정해준다.
차트를 넣을 영역에 캔버스에 id 값과 크기를 설정한다.

---

**Javascript**

```
const ctx = document.getElementById('myChart').getContext('2d'); // 2d 차트
const myChart = new Chart(ctx, {
    type: 'bar', // 바 차트
    data: {
        labels: ['품질', '설비', '생산', '물류', '인사', '연구개발'],
        datasets: [{
            label: 'my dataset',
            data: [12, 19, 3, 5, 2, 3],
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
        }]
    },
    options: {
        responsive : false, // 반응형
        scales: {
            x: {
                stacked : true // 누적 막대 그래프 표시
            },
            y: {
                stacked : true
            }
        },
        indexAxis : 'x', // 인덱스 축 설정
        plugins : {
            legend : {
                display : false
            },
            datalabels : {
                color : 'white',
                font : {
                    size : 12
                }
            },
            showValue : {
                fontStyle : 'Helvetica',
                color : 'black',
                fontSize : 20
            }
        }
    }
});
```

<https://www.chartjs.org/docs/3.6.2/>에서 옵션, 설정 등에 대해 더 많은 정보를 얻을 수 있다.
