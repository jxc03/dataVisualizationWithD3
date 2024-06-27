<h1 align="center">
  Data Visualization With D3
</h1>

<p>
  With this, I learnt how to work with data to create different charts, graphs, hover elements to create a dynamic data visualization.
</p>

## Steps
**S1 - Add Document Elements with D3**<br>
D3 has several methods that let you add and change elements in your document.<br>
The `select()` method selects one element from the document. It takes an argument for the name of the element you want and returns an HTML node for the first element in the document that matches the name. Here's an example:<br>
`const anchor = d3.select("a");`<br>

The above example finds the first anchor tag on the page and saves an HTML node for it in the variable `anchor`. You can use the selection with other methods. The `d3` part of the example is a reference to the D3 object, which is how you access D3 methods.<br>
Two other useful methods are `append()` and `text()`.<br>
The `append()` method takes an argument for the element you want to add to the document. It appends an HTML node to a selected item, and returns a handle to that node.<br>
The `text()` method either sets the text of the selected node, or gets the current text. To set the value, you pass a string as an argument inside the parentheses of the method.<br>

Here's an example that selects an unordered list, appends a list item, and adds text:<br>
`d3.select("ul")`<br>
  `.append("li")`<br>
  `.text("Very important item");`<br>
D3 allows you to chain several methods together with periods to perform a number of actions in a row.<br>

Use the `select` method to select the `body` tag in the document. Then `append` an `h1` tag to it, and add the text `Learning D3` into the `h1` element.

```js
<body>
  <script>
    // Add your code below this line
    d3.select("body")
      .append("h1")
      .text("Learning D3")
    // Add your code above this line
  </script>
</body>
```

**S2 - Select a Group of Elements with D3**<br>
D3 also has the `selectAll()` method to select a group of elements. It returns an array of HTML nodes for all the items in the document that match the input string. Here's an example to select all the anchor tags in a document:<br>
`const anchors = d3.selectAll("a");`<br>
Like the `select()` method, `selectAll()` supports method chaining, and you can use it with other methods.<br>

Select all of the `li` tags in the document, and change their text to the string `list item` by chaining the `.text()` method.

```js
<body>
  <ul>
    <li>Example</li>
    <li>Example</li>
    <li>Example</li>
  </ul>
  <script>
    // Add your code below this line
    d3.selectAll("li")
      .text("list item")
    // Add your code above this line
  </script>
</body>
```

**S3 - Work with Data in D3**<br>
The D3 library focuses on a data-driven approach. When you have a set of data, you can apply D3 methods to display it on the page. Data comes in many formats, but this challenge uses a simple array of numbers.<br>
The first step is to make D3 aware of the data. The `data()` method is used on a selection of DOM elements to attach the data to those elements. The data set is passed as an argument to the method.

A common workflow pattern is to create a new element in the document for each piece of data in the set. D3 has the `enter()` method for this purpose.<br>
When `enter()` is combined with the `data()` method, it looks at the selected elements from the page and compares them to the number of data items in the set. If there are fewer elements than data items, it creates the missing elements.<br>

Here is an example that selects a ul element and creates a new list item based on the number of entries in the array:<br>
`<body>`<br>
  `<ul></ul>`<br>
  `<script>`<br>
    `const dataset = ["a", "b", "c"];`<br>
    `d3.select("ul").selectAll("li")`<br>
      `.data(dataset)`<br>
      `.enter()`<br>
      `.append("li")`<br>
      `.text("New item");`<br>
  `</script><br>`
`</body>`<br>
It may seem confusing to select elements that don't exist yet. This code is telling D3 to first select the `ul` on the page. Next, select all list items, which returns an empty selection. Then the `data()` method reviews the dataset and runs the following code three times, once for each item in the array. The `enter()` method sees there are no `li` elements on the page, but it needs 3 (one for each piece of data in `dataset`). New `li` elements are appended to the `ul` and have the text `New item`.<br>

Select the `body` node, then select all `h2` elements. Have D3 create and append an `h2` tag for each item in the dataset array. The text in the `h2` should say `New Title`. Your code should use the `data()` and `enter()` methods.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    // Add your code below this line
    d3.select("body").selectAll("h2")
      .data(dataset)
      .enter()
      .append("h2")
      .text("New Title")
    // Add your code above this line
  </script>
</body>
```

**S4 - Work with Dynamic Data in D3**<br>
The last two challenges cover the basics of displaying data dynamically with D3 using the `data()` and `enter()` methods. These methods take a data set and, together with the `append()` method, create a new DOM element for each entry in the data set.<br>
In the previous challenge, you created a new `h2` element for each item in the `dataset` array, but they all contained the same text, `New Title`. This is because you have not made use of the data that is bound to each of the `h2` elements.

The D3 `text()` method can take a string or a callback function as an argument:<br>
`selection.text((d) => d)`<br>
In the example above, the parameter `d` refers to a single entry in the dataset that a selection is bound to.<br>
Using the current example as context, the first `h2` element is bound to 12, the second `h2` element is bound to 31, the third `h2` element is bound to 22, and so on.<br>

Change the `text()` method so that each `h2` element displays the corresponding value from the `dataset` array with a single space and the string `USD`. For example, the first heading should be `12 USD`.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    d3.select("body").selectAll("h2")
      .data(dataset)
      .enter()
      .append("h2")
      // Add your code below this line
      .text((d) => d + " USD");
      // Add your code above this line
  </script>
</body>
```

**S5 - Add Inline Styling to Elements**<br>
D3 lets you add inline CSS styles on dynamic elements with the `style()` method.<br>
The `style()` method takes a comma-separated key-value pair as an argument. Here's an example to set the selection's text color to blue:<br>
`selection.style("color","blue");`<br>

Add the `style()` method to the code in the editor to make all the displayed text have a `font-family` of `verdana`.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    d3.select("body").selectAll("h2")
      .data(dataset)
      .enter()
      .append("h2")
      .text((d) => (d + " USD"))
      // Add your code below this line
      .style("font-family","verdana")
      // Add your code above this line
  </script>
</body>
```

**S6 - Change Styles Based on Data**<br>
D3 is about visualization and presentation of data. It's likely you'll want to change the styling of elements based on the data. For example, you may want to color a data point blue if it has a value less than 20, and red otherwise. You can use a callback function in the `style()` method and include the conditional logic. The callback function uses the `d` parameter to represent the data point:<br>
`selection.style("color", (d) => {`<br>
`});`<br>
The `style()` method is not limited to setting the `color` - it can be used with other CSS properties as well.<br>

Add the `style()` method to the code in the editor to set the `color` of the `h2` elements conditionally. Write the callback function so if the data value is less than 20, it returns red, otherwise it returns green.
<b>Note</b>: You can use if-else logic, or the ternary operator.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    d3.select("body").selectAll("h2")
      .data(dataset)
      .enter()
      .append("h2")
      .text((d) => (d + " USD"))
      // Add your code below this line
      .style("color", (d) => {
        if(d < 20) {
          return "red"
        } else {
          return "green"
        }
      })
      // Add your code above this line
  </script>
</body>
```

**S7 - Add Classes with D3**<br>
Using a lot of inline styles on HTML elements gets hard to manage, even for smaller apps. It's easier to add a class to elements and style that class one time using CSS rules. D3 has the `attr()` method to add any HTML attribute to an element, including a class name.<br>
The `attr()` method works the same way that `style()` does. It takes comma-separated values, and can use a callback function. Here's an example to add a class of `container` to a selection:<br>
`selection.attr("class", "container");`<br>
Note that the `class` parameter will remain the same whenever you need to add a class and only the `container` parameter will change.<br>

Add the `attr()` method to the code in the editor and put a class of `bar` on the `div` elements.

```js
<style>
  .bar {
    width: 25px;
    height: 100px;
    display: inline-block;
    background-color: blue;
  }
</style>
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    d3.select("body").selectAll("div")
      .data(dataset)
      .enter()
      .append("div")
      // Add your code below this line
      .attr("class", "bar")
      // Add your code above this line
  </script>
</body>
```

**S8 - Update the Height of an Element Dynamically**<br>
The previous challenges covered how to display data from an array and how to add CSS classes. You can combine these lessons to create a simple bar chart. There are two steps to this:<br>
<ol>
    <li> Create a div for each data point in the array</li>
    <li> Give each div a dynamic height, using a callback function in the style() method that sets height equal to the data value</li>
</ol>

Recall the format to set a style using a callback function:<br>
`selection.style("cssProperty", (d) => d)`<br>

Add the `style()` method to the code in the editor to set the `height` property for each element. Use a callback function to return the value of the data point with the string `px` added to it.

```js
<style>
  .bar {
    width: 25px;
    height: 100px;
    display: inline-block;
    background-color: blue;
  }
</style>
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    d3.select("body").selectAll("div")
      .data(dataset)
      .enter()
      .append("div")
      .attr("class", "bar")
      // Add your code below this line
      .style("height", (d) => d + "px")
      // Add your code above this line
  </script>
</body>
```

**S9 - Change the Presentation of a Bar Chart**<br>
The last challenge created a bar chart, but there are a couple of formatting changes that could improve it:<br>
<ol>
<li>Add space between each bar to visually separate them, which is done by adding a margin to the CSS for the bar class</li>
    <li>Increase the height of the bars to better show the difference in values, which is done by multiplying the value by a number to scale the height</li>
</ol>

First, add a `margin` of `2px` to the `bar` class in the `style` tag. Next, change the callback function in the `style()` method so it returns a value `10` times the original data value (plus the `px`).<br>
<b>Note</b>: Multiplying each data point by the <i>same</i> constant only alters the scale. It's like zooming in, and it doesn't change the meaning of the underlying data.

```js
<style>
  .bar {
    width: 25px;
    height: 100px;
    /* Add your code below this line */
    margin: 2px;
    /* Add your code above this line */
    display: inline-block;
    background-color: blue;
  }
</style>
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    d3.select("body").selectAll("div")
      .data(dataset)
      .enter()
      .append("div")
      .attr("class", "bar")
      .style("height", (d) => (d*10 + "px")) // Change this line
  </script>
</body>
```

**S10 - Learn About SVG in D3**<br>
<i>SVG</i> stands for <i>Scalable Vector Graphics</i>.<br>
Here "scalable" means that, if you zoom in or out on an object, it would not appear pixelated. It scales with the display system, whether it's on a small mobile screen or a large TV monitor.<br>
SVG is used to make common geometric shapes. Since D3 maps data into a visual representation, it uses SVG to create the shapes for the visualization. SVG shapes for a web page must go within an HTML `svg` tag.<br>
CSS can be scalable when styles use relative units (such as `vh`, `vw`, or percentages), but using SVG is more flexible to build data visualizations.<br>

Add an `svg` node to the `body` using `append()`. Give it a `width` attribute set to the provided `w` constant and a `height` attribute set to the provided `h` constant using the `attr()` or `style()` methods for each. You'll see it in the output because there's a `background-color` of pink applied to it in the `style` tag.<br>
<b>Note</b>: When using `attr()` width and height attributes do not have units. This is the building block of scaling - the element will always have a 5:1 width to height ratio, no matter what the zoom level is.

```js
<style>
  svg {
    background-color: pink;
  }
</style>
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    const w = 500;
    const h = 100;
    const svg = d3.select("body")
                  // Add your code below this line
                  .append("svg")
                  .attr("width", w)
                  .style("height", h)
                  // Add your code above this line
  </script>
</body>
```

**S11 - Display Shapes with SVG**<br>
The last challenge created an `svg` element with a given width and height, which was visible because it had a `background-color` applied to it in the `style` tag. The code made space for the given width and height.<br>
The next step is to create a shape to put in the `svg` area. There are a number of supported shapes in SVG, such as rectangles and circles. They are used to display data. For example, a rectangle (`<rect>`) SVG shape could create a bar in a bar chart.<br>

When you place a shape into the `svg` area, you can specify where it goes with `x` and `y` coordinates. The origin point of (0, 0) is in the upper-left corner. Positive values for `x` push the shape to the right, and positive values for `y` push the shape down from the origin point.<br>
To place a shape in the middle of the 500 (width) x 100 (height) `svg` from last challenge, the `x` coordinate would be 250 and the `y` coordinate would be 50.<br>
An SVG `rect` has four attributes. There are the `x` and `y` coordinates for where it is placed in the `svg` area. It also has a `height` and `width` to specify the size.<br>

Add a `rect` shape to the `svg` using `append()`, and give it a `width` attribute of `25` and `height` attribute of `100`. Also, give the `rect` `x` and `y` attributes each set to `0`.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    const w = 500;
    const h = 100;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h)
                  // Add your code below this line
                  .append("rect")
                  .attr("width", 25)
                  .attr("height", 100)
                  .attr("x",0)
                  .attr("y",0)
                  // Add your code above this line
  </script>
</body>
```

**S12 - Create a Bar for Each Data Point in the Set**<br>
The last challenge added only one rectangle to the `svg` element to represent a bar. Here, you'll combine what you've learned so far about `data()`, `enter()`, and SVG shapes to create and append a rectangle for each data point in `dataset`.<br>

A previous challenge showed the format for how to create and append a `div` for each item in `dataset`:<br>
`d3.select("body").selectAll("div")`<br>
  `.data(dataset)`<br>
  `.enter()`<br>
  `.append("div")`<br>
There are a few differences working with `rect` elements instead of `div` elements. The `rect` elements must be appended to an `svg` element, not directly to the `body`. Also, you need to tell D3 where to place each `rect` within the `svg` area. The bar placement will be covered in the next challenge.<br>

Use the `data()`, `enter()`, and `append()` methods to create and append a `rect` for each item in `dataset`. The bars should display all on top of each other; this will be fixed in the next challenge.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    const w = 500;
    const h = 100;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("rect")
       // Add your code below this line
       .data(dataset)
       .enter()
       .append("rect")
       // Add your code above this line
       .attr("x", 0)
       .attr("y", 0)
       .attr("width", 25)
       .attr("height", 100);
  </script>
</body>
```

**S13 - Dynamically Set the Coordinates for Each Bar**<br>
The last challenge created and appended a rectangle to the `svg` element for each point in `dataset` to represent a bar. Unfortunately, they were all stacked on top of each other.
The placement of a rectangle is handled by the `x` and `y` attributes. They tell D3 where to start drawing the shape in the `svg` area. The last challenge set them each to 0, so every bar was placed in the upper-left corner.<br>

For a bar chart, all of the bars should sit on the same vertical level, which means the `y` value stays the same (at 0) for all bars. The `x` value, however, needs to change as you add new bars. Remember that larger `x` values push items farther to the right. As you go through the array elements in `dataset`, the `x` value should increase.<br>

The `attr()` method in D3 accepts a callback function to dynamically set that attribute. The callback function takes two arguments, one for the data point itself (usually `d`) and one for the index of the data point in the array. The second argument for the index is optional. Here's the format:<br>
`selection.attr("property", (d, i) => {`<br>
`})`

It's important to note that you do NOT need to write a `for` loop or use `forEach()` to iterate over the items in the data set. Recall that the `data()` method parses the data set, and any method that's chained after `data()` is run once for each item in the data set.<br>

Change the `x` attribute callback function so it returns the index times 30.<br>
<b>Note</b>: Each bar has a width of 25, so increasing each `x` value by 30 adds some space between the bars. Any value greater than 25 would work in this example.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    const w = 500;
    const h = 100;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => {
         // Add your code below this line
         return i * 30
         // Add your code above this line
       })
       .attr("y", 0)
       .attr("width", 25)
       .attr("height", 100);
  </script>
</body>
```

**S14 - Dynamically Change the Height of Each Bar**<br>
The height of each bar can be set to the value of the data point in the array, similar to how the `x` value was set dynamically.<br>
`selection.attr("property", (d, i) => {`
`})`<br>
Here `d` would be the data point value, and `i` would be the index of the data point in the array.<br>

Change the callback function for the `height` attribute to return the data value times 3.
<b>Note</b>: Remember that multiplying all data points by the same constant scales the data (like zooming in). It helps to see the differences between bar values in this example.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    const w = 500;
    const h = 100;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", 0)
       .attr("width", 25)
       .attr("height", (d, i) => {
         // Add your code below this line
         return d * 3
         // Add your code above this line
       });
  </script>
</body>
```

**S15 - Invert SVG Elements**<br>
You may have noticed the bar chart looked like it's upside-down, or inverted. This is because of how SVG uses (x, y) coordinates.<br>
In SVG, the origin point for the coordinates is in the upper-left corner. An `x` coordinate of 0 places a shape on the left edge of the SVG area. A `y` coordinate of 0 places a shape on the top edge of the SVG area. Higher `x` values push the rectangle to the right. Higher `y` values push the rectangle down.<br>

To make the bars right-side-up, you need to change the way the `y` coordinate is calculated. It needs to account for both the height of the bar and the total height of the SVG area.<br>
The height of the SVG area is 100. If you have a data point of 0 in the set, you would want the bar to start at the bottom of the SVG area (not the top). To do this, the `y` coordinate needs a value of 100. If the data point value were 1, you would start with a y coordinate of 100 to set the bar at the bottom. Then you need to account for the height of the bar of 1, so the final `y` coordinate would be 99.
The `y` coordinate that is `y = heightOfSVG - heightOfBar` would place the bars right-side-up.<br>

Change the callback function for the `y` attribute to set the bars right-side-up. Remember that the `height` of the bar is 3 times the data value `d`.<br>
<b>Note</b>: In general, the relationship is `y = h - m * d`, where `m` is the constant that scales the data points.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    const w = 500;
    const h = 100;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => {
         // Add your code below this line
        return h - 3 * d
         // Add your code above this line
       })
       .attr("width", 25)
       .attr("height", (d, i) => 3 * d);
  </script>
</body>
```

**S16 - Change the Color of an SVG Element**<br>
The bars are in the right position, but they are all the same black color. SVG has a way to change the color of the bars.<br>
In SVG, a `rect` shape is colored with the `fill` attribute. It supports hex codes, color names, and rgb values, as well as more complex options like gradients and transparency.<br>

Add an `attr()` method to set the `fill` of all the bars to the color navy.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    const w = 500;
    const h = 100;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - 3 * d)
       .attr("width", 25)
       .attr("height", (d, i) => 3 * d)
       // Add your code below this line
       .attr("fill", "navy")
       // Add your code above this line
  </script>
</body>
```

**S17 - Add Labels to D3 Elements**<br>
D3 lets you label a graph element, such as a bar, using the SVG `text` element.<br>
Like the `rect` element, a `text` element needs to have `x` and `y` attributes, to place it on the SVG. It also needs to access the data to display those values.<br>
D3 gives you a high level of control over how you label your bars.<br>

The code in the editor already binds the data to each new `text` element. First, append `text` nodes to the `svg`. Next, add attributes for the `x` and `y` coordinates. They should be calculated the same way as the rect ones, except the `y` value for the `text` should make the label sit 3 units higher than the bar. Finally, use the D3 `text()` method to set the label equal to the data point value.<br>
<b>Note</b>: For the label to sit higher than the bar, decide if the `y` value for the `text` should be 3 greater or 3 less than the `y` value for the bar.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    const w = 500;
    const h = 100;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - 3 * d)
       .attr("width", 25)
       .attr("height", (d, i) => 3 * d)
       .attr("fill", "navy");
    svg.selectAll("text")
       .data(dataset)
       .enter()
       // Add your code below this line
       .append("text")
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - 3 * d - 3)
       .text((d) => d)
       // Add your code above this line
  </script>
<body>
```

**S18 - Style D3 Labels**<br>
D3 methods can add styles to the bar labels. The `fill` attribute sets the color of the text for a `text` node. The `style()` method sets CSS rules for other styles, such as `font-family` or `font-size`.<br>

Set the `font-size` of the `text` elements to `25px`, and the color of the text to red.

```js
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    const w = 500;
    const h = 100;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - 3 * d)
       .attr("width", 25)
       .attr("height", (d, i) => d * 3)
       .attr("fill", "navy");
    svg.selectAll("text")
       .data(dataset)
       .enter()
       .append("text")
       .text((d) => d)
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - (3 * d) - 3)
       // Add your code below this line
       .style("font-size", "25px")
       .style("fill", "red")
       // Add your code above this line
  </script>
</body>
```

**S19 - Add a Hover Effect to a D3 Element**<br>
It's possible to add effects that highlight a bar when the user hovers over it with the mouse. So far, the styling for the rectangles is applied with the built-in D3 and SVG methods, but you can use CSS as well.<br>
You set the CSS class on the SVG elements with the `attr()` method. Then the `:hover` pseudo-class for your new class holds the style rules for any hover effects.<br>

Use the `attr()` method to add a class of `bar` to all the `rect` elements. This changes the `fill` color of the bar to brown when you mouse over it.

```js
<style>
  .bar:hover {
    fill: brown;
  }
</style>
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    const w = 500;
    const h = 100;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - 3 * d)
       .attr("width", 25)
       .attr("height", (d, i) => 3 * d)
       .attr("fill", "navy")
       // Add your code below this line
       .attr("class", "bar")
       // Add your code above this line
    svg.selectAll("text")
       .data(dataset)
       .enter()
       .append("text")
       .text((d) => d)
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - (3 * d) - 3);
  </script>
</body>
```

**S20 - Add a Tooltip to a D3 Element**<br>
A tooltip shows more information about an item on a page when the user hovers over that item. There are several ways to add a tooltip to a visualization. This challenge uses the SVG `title` element.<br>
`title` pairs with the `text()` method to dynamically add data to the bars.<br>

Append a `title` element under each `rect` node. Then call the `text()` method with a callback function so the text displays the data value.

```js
<style>
  .bar:hover {
    fill: brown;
  }
</style>
<body>
  <script>
    const dataset = [12, 31, 22, 17, 25, 18, 29, 14, 9];
    const w = 500;
    const h = 100;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("rect")
       .data(dataset)
       .enter()
       .append("rect")
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - 3 * d)
       .attr("width", 25)
       .attr("height", (d, i) => d * 3)
       .attr("fill", "navy")
       .attr("class", "bar")
       // Add your code below this line
       .append("title")
       .text((d) => d)
       // Add your code above this line
    svg.selectAll("text")
       .data(dataset)
       .enter()
       .append("text")
       .text((d) => d)
       .attr("x", (d, i) => i * 30)
       .attr("y", (d, i) => h - (d * 3 + 3))
  </script>
</body>
```

**S21 - Create a Scatterplot with SVG Circles**<br>
A scatter plot is another type of visualization. It usually uses circles to map data points, which have two values each. These values tie to the `x` and `y` axes, and are used to position the circle in the visualization.<br>

SVG has a `circle` tag to create the circle shape. It works a lot like the `rect` elements you used for the bar chart.<br>

Use the `data()`, `enter()`, and `append()` methods to bind `dataset` to new `circle` elements that are appended to the SVG.<br>
<b>Note</b>: The circles won't be visible because we haven't set their attributes yet. We'll do that in the next challenge.

```js
<body>
  <script>
    const dataset = [
                  [ 34,    78 ],
                  [ 109,   280 ],
                  [ 310,   120 ],
                  [ 79,    411 ],
                  [ 420,   220 ],
                  [ 233,   145 ],
                  [ 333,   96 ],
                  [ 222,   333 ],
                  [ 78,    320 ],
                  [ 21,    123 ]
                ];
    const w = 500;
    const h = 500;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("circle")
       // Add your code below this line
       .data(dataset)
       .enter()
       .append("circle")
       // Add your code above this line
  </script>
</body>
```

**S22 - Add Attributes to the Circle Elements**<br>
The last challenge created the `circle` elements for each point in the `dataset`, and appended them to the SVG. But D3 needs more information about the position and size of each `circle` to display them correctly.<br>
A `circle` in SVG has three main attributes. The `cx` and `cy` attributes are the coordinates. They tell D3 where to position the center of the shape on the SVG. The radius (`r` attribute) gives the size of the `circle`.<br>
Just like the `rect` `y` coordinate, the `cy` attribute for a `circle` is measured from the top of the SVG, not from the bottom.<br>

All three attributes can use a callback function to set their values dynamically. Remember that all methods chained after `data(dataset)` run once per item in `dataset`. The `d` parameter in the callback function refers to the current item in `dataset`, which is an array for each point. You use bracket notation, like `d[0]`, to access the values in that array.<br>

Add `cx`, `cy`, and `r` attributes to the `circle` elements. The `cx` value should be the first number in the array for each item in `dataset`. The `cy` value should be based off the second number in the array, but make sure to show the chart right-side-up and not inverted. The `r` value should be `5` for all circles.

```js
<body>
  <script>
    const dataset = [
                  [ 34,    78 ],
                  [ 109,   280 ],
                  [ 310,   120 ],
                  [ 79,    411 ],
                  [ 420,   220 ],
                  [ 233,   145 ],
                  [ 333,   96 ],
                  [ 222,   333 ],
                  [ 78,    320 ],
                  [ 21,    123 ]
                ];
    const w = 500;
    const h = 500;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("circle")
       .data(dataset)
       .enter()
       .append("circle")
       // Add your code below this line
       .attr("cx", (d) => d[0])
       .attr("cy", (d) => w - d[1])
       .attr("r", 5)
       // Add your code above this line
  </script>
</body>
```

**S23 - Add Labels to Scatter Plot Circles**<br>
You can add text to create labels for the points in a scatter plot.<br>
The goal is to display the comma-separated values for the first (`x`) and second (`y`) fields of each item in `dataset`.<br>
The `text` nodes need `x` and `y` attributes to position it on the SVG. In this challenge, the `y` value (which determines height) can use the same value that the `circle` uses for its `cy` attribute. The `x` value can be slightly larger than the `cx` value of the `circle`, so the label is visible. This will push the label to the right of the plotted point.<br>

Label each point on the scatter plot using the `text` elements. The text of the label should be the two values separated by a comma and a space. For example, the label for the first point is `34, 78`. Set the `x` attribute so it's `5` units more than the value you used for the `cx` attribute on the `circle`. Set the `y` attribute the same way that's used for the `cy` value on the `circle`.

```js
<body>
  <script>
    const dataset = [
                  [ 34,    78 ],
                  [ 109,   280 ],
                  [ 310,   120 ],
                  [ 79,    411 ],
                  [ 420,   220 ],
                  [ 233,   145 ],
                  [ 333,   96 ],
                  [ 222,   333 ],
                  [ 78,    320 ],
                  [ 21,    123 ]
                ];
    const w = 500;
    const h = 500;
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("circle")
       .data(dataset)
       .enter()
       .append("circle")
       .attr("cx", (d, i) => d[0])
       .attr("cy", (d, i) => h - d[1])
       .attr("r", 5);
    svg.selectAll("text")
       .data(dataset)
       .enter()
       .append("text")
       // Add your code below this line
       .text((d) => d[0] + ", " + d[1])
       .attr("x", (d, i) => d[0] + 5)
       .attr("y", (d, i) => h - d[1])
       // Add your code above this line
  </script>
</body>
```

**S24 - Create a Linear Scale with D3**<br>
The bar and scatter plot charts both plotted data directly onto the SVG. However, if the height of a bar or one of the data points were larger than the SVG height or width values, it would go outside the SVG area.<br>

In D3, there are scales to help plot data. `scales` are functions that tell the program how to map a set of raw data points onto the pixels of the SVG.<br>
For example, say you have a 100x500-sized SVG and you want to plot Gross Domestic Product (GDP) for a number of countries. The set of numbers would be in the billion or trillion-dollar range. You provide D3 a type of scale to tell it how to place the large GDP values into that 100x500-sized area.<br>

It's unlikely you would plot raw data as-is. Before plotting it, you set the scale for your entire data set, so that the `x` and `y` values fit your SVG width and height.<br>

D3 has several scale types. For a linear scale (usually used with quantitative data), there is the D3 method `scaleLinear()`:<br>
`const scale = d3.scaleLinear()`<br>
By default, a scale uses the identity relationship. The value of the input is the same as the value of the output. A separate challenge covers how to change this.<br>

Change the `scale` variable to create a linear scale. Then set the `output` variable to the scale called with an input argument of `50`.

```js
<body>
  <script>
    // Add your code below this line
    const scale = d3.scaleLinear(); // Create the scale here
    const output = scale(50); // Call scale with an argument here
    // Add your code above this line
    d3.select("body")
      .append("h2")
      .text(output);
  </script>
</body>
```

**S25 - Set a Domain and a Range on a Scale**<br>
By default, scales use the identity relationship. This means the input value maps to the output value. However, scales can be much more flexible and interesting.<br>

Say a dataset has values ranging from 50 to 480. This is the input information for a scale, also known as the domain.<br>
You want to map those points along the `x` axis on the SVG, between 10 units and 500 units. This is the output information, also known as the range.<br>

The `domain()` and `range()` methods set these values for the scale. Both methods take an array of at least two elements as an argument. Here's an example:<br>
`scale.domain([50, 480]);`<br>
`scale.range([10, 500]);`<br>
`scale(50)`<br>
`scale(480)`<br>
`scale(325)`<br>
`scale(750)`<br>
`d3.scaleLinear()`<br>
In order, the following values would be displayed in the console: `10`, `500`, `323.37`, and `807.67`.<br>
Notice that the scale uses the linear relationship between the domain and range values to figure out what the output should be for a given number. The minimum value in the domain (50) maps to the minimum value (10) in the range.<br>

Create a scale and set its domain to `[250, 500]` and range to `[10, 150]`.<br>
<b>Note</b>: You can chain the `domain()` and `range()` methods onto the `scale` variable.

```js
<body>
  <script>
    // Add your code below this line
    const scale = d3.scaleLinear();
    scale.domain([250, 500]);
    scale.range([10, 150]);
    // Add your code above this line
    const output = scale(50);
    d3.select("body")
      .append("h2")
      .text(output);
  </script>
</body>
```

**S26 - Use the d3.max and d3.min Functions to Find Minimum and Maximum Values in a Dataset**<br>
The D3 methods `domain()` and `range()` set that information for your scale based on the data. There are a couple methods to make that easier.<br>
Often when you set the domain, you'll want to use the minimum and maximum values within the data set. Trying to find these values manually, especially in a large data set, may cause errors.<br>
D3 has two methods - `min()` and `max()` to return this information. Here's an example:<br>
`const exampleData = [34, 234, 73, 90, 6, 52];`<br>
`d3.min(exampleData)`<br>
`d3.max(exampleData)`<br>

A dataset may have nested arrays, like the `[x, y]` coordinate pairs that were in the scatter plot example. In that case, you need to tell D3 how to calculate the maximum and minimum. Fortunately, both the `min()` and `max()` methods take a callback function. In this example, the callback function's argument `d` is for the current inner array. The callback needs to return the element from the inner array (the `x` or `y` value) over which you want to compute the maximum or minimum. Here's an example for how to find the min and max values with an array of arrays:<br>
`const locationData = [[1, 7],[6, 3],[8, 3]];`<br>
`const minX = d3.min(locationData, (d) => d[0]);`<br>
`minX` would have the value `1`.<br>

The `positionData` array holds sub arrays of x, y, and z coordinates. Use a D3 method to find the maximum value of the z coordinate (the third value) from the arrays and save it in the `output` variable.

```js
<body>
  <script>
    const positionData = [[1, 7, -4],[6, 3, 8],[2, 9, 3]]
    // Add your code below this line
    const output = d3.max(positionData, (d) => d[2]); // Change this line
    // Add your code above this line
    d3.select("body")
      .append("h2")
      .text(output)
  </script>
</body>
```

**S27 - Use Dynamic Scales**<br>
The D3 `min()` and `max()` methods are useful to help set the scale.<br>

Given a complex data set, one priority is to set the scale so the visualization fits the SVG container's width and height. You want all the data plotted inside the SVG so it's visible on the web page.<br>

The example below sets the x-axis scale for scatter plot data. The `domain()` method passes information to the scale about the raw data values for the plot. The `range()` method gives it information about the actual space on the web page for the visualization.
In the example, the domain goes from 0 to the maximum in the set. It uses the `max()` method with a callback function based on the x values in the arrays. The range uses the SVG's width (`w`), but it includes some padding, too. This puts space between the scatter plot dots and the edge of the SVG.<br>
`const dataset = [`<br>
  `[ 34,    78 ],`<br>
  `[ 109,   280 ],`<br>
  `[ 310,   120 ],`<br>
  `[ 79,    411 ],`<br>
  `[ 420,   220 ],`<br>
  `[ 233,   145 ],`<br>
  `[ 333,   96 ],`<br>
  `[ 222,   333 ],`<br>
  `[ 78,    320 ],`<br>
  `[ 21,    123 ]`<br>
`];`<br>
`const w = 500;`<br>
`const h = 500;`<br>
`const padding = 30;`<br>
`const xScale = d3.scaleLinear()`<br>
  `.domain([0, d3.max(dataset, (d) => d[0])])`<br>
  `.range([padding, w - padding]);`<br>
The padding may be confusing at first. Picture the x-axis as a horizontal line from 0 to 500 (the width value for the SVG). Including the padding in the `range()` method forces the plot to start at 30 along that line (instead of 0), and end at 470 (instead of 500).<br>

Use the `yScale` variable to create a linear y-axis scale. The domain should start at zero and go to the maximum `y` value in the set. The range should use the SVG height (`h`) and include padding.<br>
<b>Note</b>: Remember to keep the plot right-side-up. When you set the range for the y coordinates, the higher value (height minus padding) is the first argument, and the lower value is the second argument.

```js
<body>
  <script>
    const dataset = [
                  [ 34,    78 ],
                  [ 109,   280 ],
                  [ 310,   120 ],
                  [ 79,    411 ],
                  [ 420,   220 ],
                  [ 233,   145 ],
                  [ 333,   96 ],
                  [ 222,   333 ],
                  [ 78,    320 ],
                  [ 21,    123 ]
                ];
    const w = 500;
    const h = 500;
    // Padding between the SVG boundary and the plot
    const padding = 30;
    // Create an x and y scale
    const xScale = d3.scaleLinear()
                    .domain([0, d3.max(dataset, (d) => d[0])])
                    .range([padding, w - padding]);
    // Add your code below this line
    const yScale = d3.scaleLinear()
                    .domain([0, d3.max(dataset, (d) => d[1])])
                    .range([h - padding, padding]);
    // Add your code above this line
    const output = yScale(411); // Returns 30
    d3.select("body")
      .append("h2")
      .text(output)
  </script>
</body>
```

**S28 - Use a Pre-Defined Scale to Place Elements**<br>
With the scales set up, it's time to map the scatter plot again. The scales are like processing functions that turn the `x` and `y` raw data into values that fit and render correctly on the SVG. They keep the data within the screen's plotting area.<br>

You set the coordinate attribute values for an SVG shape with the scaling function. This includes `x` and `y` attributes for `rect` or `text` elements, or `cx` and `cy` for `circles`. Here's an example:<br>
`shape`<br>
  `.attr("x", (d) => xScale(d[0]))`<br>
Scales set shape coordinate attributes to place the data points onto the SVG. You don't need to apply scales when you display the actual data value, for example, in the `text()` method for a tooltip or label.<br>

Use `xScale` and `yScale` to position both the `circle` and `text` shapes onto the SVG. For the `circles`, apply the scales to set the `cx` and `cy` attributes. Give them a radius of `5` units, too.<br>
For the `text` elements, apply the scales to set the `x` and `y` attributes. The labels should be offset to the right of the dots. To do this, add `10` units to the `x` data value before passing it to the `xScale`.

```js
<body>
  <script>
    const dataset = [
                  [ 34,     78 ],
                  [ 109,   280 ],
                  [ 310,   120 ],
                  [ 79,   411 ],
                  [ 420,   220 ],
                  [ 233,   145 ],
                  [ 333,   96 ],
                  [ 222,    333 ],
                  [ 78,    320 ],
                  [ 21,   123 ]
                ];
    const w = 500;
    const h = 500;
    const padding = 60;
    const xScale = d3.scaleLinear()
                     .domain([0, d3.max(dataset, (d) => d[0])])
                     .range([padding, w - padding]);
    const yScale = d3.scaleLinear()
                     .domain([0, d3.max(dataset, (d) => d[1])])
                     .range([h - padding, padding]);
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("circle")
       .data(dataset)
       .enter()
       .append("circle")
       // Add your code below this line
       .attr("cx", (d) => xScale(d[0]))
       .attr("cy", (d) => yScale(d[1]))
       .attr("r", 5)
       // Add your code above this line
    svg.selectAll("text")
       .data(dataset)
       .enter()
       .append("text")
       .text((d) =>  (d[0] + ", "
 + d[1]))
       // Add your code below this line
       .attr("x", (d) => xScale(d[0] + 10))
       .attr("y", (d) => yScale(d[1]))
       // Add your code above this line
  </script>
</body>
```

**S29 - Add Axes to a Visualization**<br>
Another way to improve the scatter plot is to add an x-axis and a y-axis.<br>

D3 has two methods, `axisLeft()` and `axisBottom()`, to render the y-axis and x-axis, respectively. Here's an example to create the x-axis based on the `xScale` in the previous challenges:<br>
`const xAxis = d3.axisBottom(xScale);`<br>

The next step is to render the axis on the SVG. To do so, you can use a general SVG component, the `g` element. The `g` stands for group. Unlike `rect`, `circle`, and `text`, an axis is just a straight line when it's rendered. Because it is a simple shape, using `g` works. The last step is to apply a `transform` attribute to position the axis on the SVG in the right place. Otherwise, the line would render along the border of the SVG and wouldn't be visible. SVG supports different types of `transforms`, but positioning an axis needs `translate`. When it's applied to the `g` element, it moves the whole group over and down by the given amounts. Here's an example:<br>
`const xAxis = d3.axisBottom(xScale);`<br>
`svg.append("g")`<br>
   `.attr("transform", "translate(0, " + (h - padding) + ")")`<br>
   `.call(xAxis);`<br>
The above code places the x-axis at the bottom of the SVG. Then it's passed as an argument to the `call()` method. The y-axis works in the same way, except the `translate` argument is in the form `(x, 0)`. Because translate is a string in the `attr()` method above, you can use concatenation to include variable values for its arguments.

The scatter plot now has an x-axis. Create a y-axis in a variable named `yAxis` using the `axisLeft()` method. Then render the axis using a `g` element. Make sure to use a `transform` attribute to translate the axis by the amount of padding units right, and `0` units down. Remember to `call()` the axis.

```js
<body>
  <script>
    const dataset = [
                  [ 34,     78 ],
                  [ 109,   280 ],
                  [ 310,   120 ],
                  [ 79,   411 ],
                  [ 420,   220 ],
                  [ 233,   145 ],
                  [ 333,   96 ],
                  [ 222,    333 ],
                  [ 78,    320 ],
                  [ 21,   123 ]
                ];
    const w = 500;
    const h = 500;
    const padding = 60;
    const xScale = d3.scaleLinear()
                     .domain([0, d3.max(dataset, (d) => d[0])])
                     .range([padding, w - padding]);
    const yScale = d3.scaleLinear()
                     .domain([0, d3.max(dataset, (d) => d[1])])
                     .range([h - padding, padding]);
    const svg = d3.select("body")
                  .append("svg")
                  .attr("width", w)
                  .attr("height", h);
    svg.selectAll("circle")
       .data(dataset)
       .enter()
       .append("circle")
       .attr("cx", (d) => xScale(d[0]))
       .attr("cy",(d) => yScale(d[1]))
       .attr("r", (d) => 5);
    svg.selectAll("text")
       .data(dataset)
       .enter()
       .append("text")
       .text((d) =>  (d[0] + "," + d[1]))
       .attr("x", (d) => xScale(d[0] + 10))
       .attr("y", (d) => yScale(d[1]))
    const xAxis = d3.axisBottom(xScale);
    // Add your code below this line
    const yAxis = d3.axisLeft(yScale);
    // Add your code above this line
    svg.append("g")
       .attr("transform", "translate(0," + (h - padding) + ")")
       .call(xAxis);
    // Add your code below this line
    svg.append("g")
         .attr("transform", "translate(" + (padding) + ",0)")
         .call(yAxis)
    // Add your code above this line
  </script>
</body>
```
