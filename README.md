D3.js
=====
Visualize Your Data
D3.js is cool! I just got lost for a few hours poking around the D3 website and the possibilities seem endless. This tool definitely requires a pretty high level of expertise with Javascript and JSON but it generates some gorgeous, sophisticated charts. checkout the examples :
https://github.com/mbostock/d3/wiki/Gallery

what is D3.js(Data-Driven Documents)?
    D3.js is a JavaScript library for manipulating documents based on data. D3 helps you bring data to life using HTML, SVG(Scalable Vector Graphics) and CSS. D3’s emphasis on web standards gives you the full capabilities of modern browsers without tying yourself to a proprietary framework, combining powerful visualization components and a data-driven approach to DOM manipulation.
    D3.js helps you attach your data to DOM (Document Object Model) elements. Then you can use CSS3, HTML, and/or SVG showcase this data. Finally, you can make the data interactive through the use of D3.js data-driven transformations and transitions.

D3 features:
 I recommend using d3 not any other visualization library because of the following reasons:
 * It works on the web. Data visualizations are only good if
   people see them, and there’s no better place to see them than on the internet, in your browser. Protovis was the first library to make any real headway in this direction, despite other libraries and services that tried. Manyeyes is cool, but it lacks graphic flexibility and the resulting visualizations can’t just live anywhere seamlessly. Prefuse and Flare (both predecessors to D3) are nice, but neither one runs in a browser without a plugin. Quadrigram (previously Impure) has the same plugin problem
 * flexibility is another reason for using D3.
   Since it works seamlessly with existing web technologies, and can manipulate any part of the document object model, it is as flexible as the client side web technology stack (HTML, CSS, SVG). This gives it huge advantages over other tools because it can look like anything you want, and it isn’t limited to small regions of a webpage like Processing.js, Paper.js, Raphael.js, or other canvas or SVG-only based libraries. It also takes advantage of built in functionality that the browser has, simplifying the developer’s job, especially for mouse interaction.

D3 disadvantages:
   DOM manipulation can be extremely slow for large numbers of entries. SVG also has performance limitations when dealing with large quantities of elements. Fortunately for D3, good data visualization rarely requires drawing these quantities of elements on the screen. There is a learning curve to javascript, but this is true of all tools, and with great community support, learning is much easier.

Installing D3.js :
 link directly to the latest release, copy this snippet to the main or index file in your app :
   <script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>
   or download it from here :
   http://d3js.org/
I used the example below for illustration lets make  a donut chart :
<!DOCTYPE html>
<html>
<head>
   <title> Playing with d3</title>
   <script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script> // this will add the D3 library to our app.
</head>
<body>
    <script>
        var data = [10, 50, 80, 40]; // info that we need to append to the chart
        var r = 100; // raduis for the circle , I call it donuts
        var color = d3.scale.ordinal()
                  .range(["red", "green", "orange","blue"]); // coloring the chart.
        var canvas = d3.select("body").append("svg")// adding the svg to the html body(this is always the first step )
               .attr("width", 1500)
               .attr("height", 1500);

        var group = canvas.append("g")
                        .attr("transform", "translate(400, 300)");

        var arc = d3.svg.arc() //create the arcs
                   .innerRadius(200) //the inside circle
                   .outerRadius(r);
        var pie = d3.layout.pie() // this will create what i called pie chart and an object for each element
                   .value(function (d) { return d;});

        var arcs = group.selectAll(".arc") // bind(link) our data to our elements
                    .data(pie(data))
                    .enter()
                    .append("g")  //we append a group for each element
                    .attr("class", "arc"); // every group of element has a class of arc

        arcs.append("path")  // appending a path for each element's object to be showing in the page
              .attr("d", arc)
              .attr("fill", function (d) {return color(d.data); });

        arcs.append("text") // pass the text to the chart (labels)
              .attr("transform", function (d) { return "translate("+ arc.centroid(d)+")";}) //set the labels in there position at the chart
              .attr("text-anchor", "middle")
              .attr("font-size", "2em")
              .text(function (d) {return d.data;});


    </script>

 </body>
 </html>
for more information I include some resources in the end of this blog check them out.

resources:
http://www.d3js.org
http://www.recursion.org/d3-for-mere-mortals/





