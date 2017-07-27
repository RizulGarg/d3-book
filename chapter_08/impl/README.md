# Introducing Axes

- Visual features unlike `scale` .
```javascript
d3.axisTop // Ticks on top
d3.axisBottom
d3.axisLeft
d3.axisRight // Ticks on right
```
d3.axisTop, d3.axisBottom, d3.axisLeft, and d3.axisRight

- Take `scale` as a parameter 

```javascript

var xAxis = d3.axisBottom()
              .scale(xScale);

```

- Put inside a group, assign a class ( for CSS ), and position using transform's translate.

```javascript

svg.append("g")
    .attr("class", "axis")
    .attr("transform", "translate(0," + (h - padding) + ")")
    .call(xAxis);

```

- Use CSS to style; note svg attributes differ from CSS ones

```css

.axis path,
.axis line {
    stroke: teal;
    shape-rendering: crispEdges;
}

.axis text {
    font-family: Optima, Futura, sans-serif;
    font-weight: bold;
    font-size: 14px;
    fill: teal;
}

```

- Check for ticks.
```javascript

var xAxis = d3.axisBottom()
                  .scale(xScale)
                  .ticks(5);


var xAxis = d3.axisBottom()
                  .scale(xScale)
                  .tickValues([0, 100, 250, 600]);

var formatAsPercentage = d3.format(".1%");

xAxis.tickFormat(formatAsPercentage);


```

