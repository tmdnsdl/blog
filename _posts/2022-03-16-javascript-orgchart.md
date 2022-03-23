---
title: "Javascript로 조직도를 만들어보자"
date: 2022-03-16
categories: Javascript
---

### Javascript Organization chart 제작

---

구글에서 제공하는 차트 기능으로 웹 페이지에 조직도를 쉽게 표현해보자.

---

**Javascript**

```
<script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
<script type="text/javascript">
    google.charts.load('current', {packages:["orgchart"]});
    google.charts.setOnLoadCallback(drawChart);

    function drawChart() {
      var data = new google.visualization.DataTable();
      data.addColumn('string', 'Name');
      data.addColumn('string', 'Manager');
      data.addColumn('string', 'ToolTip');

      // For each orgchart box, provide the name, manager, and tooltip to show.

      data.addRows([
          ['A', '', 'head'],
          ['A1', 'A', 'head의 하위 항목1'],
          ['A2', 'A', 'head의 하위 항목2'],
          ['A3', 'A', 'head의 하위 항목3'],
          ['A4', 'A', 'head의 하위 항목4']
        ]);

      // Create the chart.
      var chart = new google.visualization.OrgChart(document.getElementById('chart_div'));
      // Draw the chart, setting the allowHtml option to true for the tooltips.
      const option = {'allowHtml':true, 'color':'#ffffff', 'size':'large'}
      chart.draw(data, option);
    }
</script>
```

조직도 데이터에 세개의 칼럼이 있는데 Name은 이름이고
Manager는 상위 항목의 Name을 적으면 해당 상위 항목의 하위 항목으로 조직도가 작성이 된다.
ToolTip은 마우스 오버를 했을때 보이는 툴팁 정보이다.

옵션에 대해서는 다양한 설정 방법이 있으므로
<https://developers.google.com/chart/interactive/docs/gallery/orgchart>에서
관련 내용을 찾아보기를 바란다.

---

**html & css**

```
<style>
    #chart_div .google-visualization-orgchart-table {
        width: 500px;
        height: 250px;
    }
    .google-visualization-orgchart-table td {
        font-family: NotoSans;
    }
</style>
<div class="chart-box">
    <div id="chart_div"></div>
</div>
```

google 조직도 차트의 기능을 자바스크립트에 추가 시키면
chart_div 영역에 조직도 차트를 그릴 수 있다.

orgchart-table css로 조직도의 크기를 설정하고
원하는 폰트를 orgchart-table td에 설정 할 수 있다.

그 외에도 다양하게 스타일을 지정 할 수 있으므로
개발자 도구에서 요소를 찾아 나만의 스타일을 지정해보자.
