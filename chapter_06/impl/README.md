# Making Bar Chart and Scatter Plot

## Bar Chart

No template, use rects to draw manually with 1D dataset.

### Without SVG - divs

- Not recommended, use CSS to style div
```css
div.bar {
			display: inline-block;
			width: 20px;
			height: 75px;
			background-color: teal;
			margin-right: 2px;
		}

```
- Use d3 to apply class ( with `attr("class",foo))
```javascript
d3.select("body").selectAll("div")
		.data(dataset).enter()
		.append("div")
		.classed("bar",true)
		.style("height",function (d) {
			return 20*d+"px";
        });
```

### Use SVG 

- The recommended d3 way
- Create SVG
```javascript

var svg = d3.select("body")
         .append("svg")
         .attr("height",h)
         .attr("width",w);

```
- Add rectangles and set their attributes
```javascript

var rects = svg.selectAll("rect")
         .data(dataset)
         .enter()
         .append("rect")
         .attr("x",function (d,i) {
             return i * (w / dataset.length);;
         })
         .attr("y", function (d) {
             return h-d;
         })
         .attr("height",function(d){
             return d*4;
         })
         .attr("width", w / dataset.length - barPadding)
         .attr("fill", function (d,i) {
             return "rgb("+Math.round(d*i)+","+Math.round(d+20)+", " + Math.round(d * 10) + ")";
         });

```
- Use text() to add labels

```javascript

var labels = svg.selectAll("text")
         .data(dataset).enter()
         .append("text")
         .text(function (d) {
             return d;
         })
         .attr("x", function(d, i) {
             return i * (w / dataset.length) + (w / dataset.length - barPadding) / 2;
         })
         .attr("y", function(d) {
             return (h - d)+14;
         })
         .attr("font-family", "sans-serif")
         .attr("font-size", function(d){
             if((d/5)>10){
                 return 10;
             }else{
                 return d/5;
             }
         })
         .attr("fill", "white")
         .attr("text-anchor", "middle");

```

## Scatter Plot

Use circles to draw with 2D dataset.

### The D3 way with SVG

```javascript

var circles = svg.selectAll("circle")
        .data(dataset).enter()
        .append("circle")
        .attr("r", function (d) {
            return Math.sqrt(h - d[1]);
        })
        .attr("cx",function(d){
            return d[0];
        })
        .attr("cy",function(d,i){
            return d[1];
        })
        .attr("fill","yellow")
        .attr("stroke","teal")
        .attr("stroke-width",function (d) {
            return d/2.0;
        });

```

