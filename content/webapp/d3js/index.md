D3.js
=====


Update Axis
-----------

    #!javascript
    svg.selectAll('g .y.axis').call(yAxis);


Remove
------

    #!javascript
    d3.select("svg").remove();

Date Format
-----------

To Create formats:

    #!javascript
    var rawFormat = d3.time.format("%Y%m%d%H%M");
    var newFormat = d3.time.format("%Y-%m-%d  %H:%M");

To parse the data:

    #!javascript

    // timestamp is a string like "201809010805", this returns a Date object
    var date = rawFormat.parse(timestamp);

To convert a Date object to string

    // return a string like "2018-09-01  08:05"
    var str = newFormat(date)
    
For a full list of formats: [https://github.com/mbostock/d3/wiki/Time-Formatting](https://github.com/mbostock/d3/wiki/Time-Formatting)


Add Grid Lines
--------------

    #!javascript

    // function to generate axis(the axis is essentially a function)
    function getYAxis() {
        return d3.svg.axis()
            .scale(y)
            .orient("left")
    }

    // Add initial Y Axis with ticks
    svg.append("g")
        .attr("class", "y axis")
        .call(getYAxis())

    // Add initial grid line(dummy Y Axis)
    svg.append('g')
        .attr('class', 'grid-line')
        .call(
            getYAxis()
                .tickFormat("")             // Hide tick text
                .tickSize(-width, 0, 0)     // Set tick width so it expands all the way to the right
        )

    function updateChart(data) {
        svg.selectAll('g .y.axis')
            .call(getYAxis());

        svg.selectAll('g .grid-line')
            .call(
                getYAxis()
                    .tickFormat("")             
                    .tickSize(-width, 0, 0)      
            );
    }