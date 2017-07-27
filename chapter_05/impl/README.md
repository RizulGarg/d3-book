# Data

- Use `d3.csv()`

	```javascript
	
	var dataset;  //Declare global var

     d3.csv("food.csv", function(data) {

    //Hand CSV data off to global var,
    //so it's accessible later.
    dataset = data;

    //Call some other functions that
    //generate your visualization, e.g.:
    //generateVisualization();
    //makeAwesomeCharts();
    //makeEvenAwesomerCharts();
    //thankAwardsCommittee();

    });

    ```

- `d3.select()` - creates placeholders for empty selections ( more data points than selections )
- Create a preProcessing function for data
	```javascript
	
	var rowConverter = function(d) {
			return {
					ID: d.id,  //No conversion
					Name: d.name,
					MenusAppeared: parseInt(d.menus_appeared),
					TimesAppeared: parseInt(d.times_appeared),
					FirstAppeared: parseInt(d.first_appeared),
					lastAppeared: parseInt(d.last_appeared),
					LowestPrice: parseFloat(d.lowest_price),
					HighestPrice: parseFloat(d.highest_price),
					};
		}


	d3.csv("../../Datasets/NYPL Menu/Dish-Clean.csv",rowConverter,function(error,data) {
			if(error){
				console.log(error);
			}else{
				dataset = data;
				console.log(data);
			}
    	
	});

	```
- Chain methods 
	
	```javascript

	d3.select("body").selectAll("p")
						 .data(dataset).enter()
						 .append("p").text(function(d) { return "I can count up to " + d; })
						 .style("color", function(d) {
    							if (d < 4) {   //Threshold of 15
        								return "red";
    								} else {
        								return "black";
    								}
					     });
	```
	