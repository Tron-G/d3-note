<!--
 * @Author: tron
 * @Date: 2023-03-16 19:44:10
 * @LastEditTime: 2023-03-16 20:04:03
 * @FilePath: \bar-test\note.md
-->
## d3绘制饼图
```javascript
/**
 * @description:绘制小饼图
 * @param {object} svg
 * @param {number} precent 绘制的比例
 * @param {number} x svg中坐标
 * @param {number} y
 * @param {number} r 半径
 * @param {object} colors 色系
 * @param {number} id 区分不同饼图
 * @return {*}
 */
function Pie(svg, precent, x, y, r, colors, id) {
  const angle = precent * Math.PI * 2;
  const new_data = [
    { startAngle: 0, endAngle: angle },
    { startAngle: angle, endAngle: Math.PI * 2 },
  ];

  const arcPath = d3.arc().innerRadius(0).outerRadius(r);
  svg
    .selectAll(".pie" + id)
    .data(new_data)
    .enter()
    .append("path")
    .attr("class", "pie" + id)
    .attr("d", function (d) {
      return arcPath(d);
    })
    .attr("fill", function (d, i) {
      return colors[i];
    })
    // .attr("stroke", "blue")
    .attr("transform", "translate(" + x + "," + y + ")");
}
```


绘制两个饼图，一个百分之30，一个百分之70：
```javascript
    const data = [0.3, 0.7];
    drawPie(svg, data[0], 200, 200, 100, ["#2ec7c9", "#ddd"], 0);
    drawPie(svg, data[1], 500, 200, 100, ["#2ec7c9", "#ddd"], 1);
```

## 旋转坐标系


```javascript
for (let i = 0; i < rect_col_num; i++) {
    svg
      .append("g")
      .append("text")
      .text(data[i])
      .attr("x",(rect_length + border_width) * i )
      .attr("y", chart_info.topbar_height - 10)
      .attr(
        "transform",
        "translate(" +
          (chart_info.left_info_width * 2 +
            20 +
            i * (rect_length + border_width)) +
          "," +
          -i * (rect_length + border_width) +
          ")  rotate(90)"
      )
      .style("font-size", "12px");
  }

```