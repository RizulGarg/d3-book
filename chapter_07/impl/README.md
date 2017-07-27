# Introducing Scales

Use scales to normalize data - fit in svg better.

## d3.scaleLinear

- Most commonly used

```javascript

var scale = d3.scaleLinear()
              .domain([100, 500])
              .range([10, 350]);

scale(100);  //Returns 10
scale(300);  //Returns 180
scale(500);  //Returns 350

```
- `d3.max` with accessor

The accessor function is an anonymous function to which max() hands off each value in the data array, one at a time, as d. The accessor function specifies how to access the value to be used for the comparison.

```javascript

var dataset = [
                [5, 20], [480, 90], [250, 50], [100, 33], [330, 95],
                [410, 12], [475, 44], [25, 67], [85, 21], [220, 88]
              ];
d3.max(dataset);  // Returns [85, 21].  What???

d3.max(dataset, function(d) {
    return d[0];
});


```

- Other methods

 **`nice()`**

This tells the scale to take whatever input domain that you gave to domain() and expand both ends to the nearest round value. 

 **`rangeRound()`**
    
Use rangeRound() in place of range(), and all values output by the scale will be rounded to the nearest whole number. 
This is useful if you want shapes to have exact pixel values, to avoid the fuzzy edges that could arise with antialiasing.

 **`clamp()`**
 
By default, a linear scale can return values outside of the specified range. 
For example, if given a value outside of its expected input domain, a scale will return a number also outside of the output range. 
Calling clamp(true) on a scale, however, forces all output values to be within the specified range. 
This means excessive values will be rounded to the range’s low or high value (whichever is nearest).

```javascript

var scale = d3.scaleLinear()
                    .domain([0.123, 4.567])
                    .range([0, 500])
                    .nice();

```


## Other Scales

### scaleTime

```javascript
var parseTime = d3.timeParse("%m/%d/%y");

var rowConverter = function(d) {
	return {
		Date: parseTime(d.Date),
		Amount: parseInt(d.Amount)
	};
}
xScale = d3.scaleTime()
			   .domain([
					d3.min(dataset, function(d) { return d.Date; }),
					d3.max(dataset, function(d) { return d.Date; })
				])
			   .range([padding, w - padding]);


// Human readable labels - Jan 2
var formatTime = d3.timeFormat("%b %e");

```



    

