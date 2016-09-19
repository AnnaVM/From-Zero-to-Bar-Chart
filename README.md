# Zero to Bar Chart with D3 v4

### Who is this for?

This is a walk through for those just getting started with the D3 library or those familiar with the library looking for an alternative to the standard Let's Make a Bar Chart Part [I](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=4&cad=rja&uact=8&ved=0ahUKEwjclImNmZzPAhVD3mMKHUKOCQkQjBAIJTAD&url=https%3A%2F%2Fbl.ocks.org%2Fmbostock%2F7322386&usg=AFQjCNHLhVkHcxaoCx1W3A8aCLs4oU2Hqg&sig2=ITg7T7CwsOUK1U4hlDIgWw&bvm=bv.133178914,d.cGc), [II](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjclImNmZzPAhVD3mMKHUKOCQkQjBAIJzAC&url=https%3A%2F%2Fbost.ocks.org%2Fmike%2Fbar%2F2%2F&usg=AFQjCNHn4eRIkc_-KCxfy5VuH9hhKwxnmA&sig2=-MwD9VXrlgZFNpErVXM4XA&bvm=bv.133178914,d.cGc) and [III](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwjclImNmZzPAhVD3mMKHUKOCQkQjBAIIzAB&url=https%3A%2F%2Fbost.ocks.org%2Fmike%2Fbar%2F3%2F&usg=AFQjCNFNoLbYperkYjMEOdv2W9sUMjBTRQ&sig2=FG2GzLGfpUgCJLRH-yf44g&bvm=bv.133178914,d.cGc). If you haven't see those yet, you may want to start there. Not because this walk through's more difficult, but rather because those tutorials are likely to give you an even more robust foundation of knowledge.

This aim of this tutorial is walk you through the create of a bar chart with v4 and little more.

### Who is this NOT for?

- Experts D3 developers
- Those comfortable feeling there own way around the documentation
- Practitioners looking for D3 development best practice

### How to use this
Before you get going, you should have text editor in front of you, a browser open as well as the console open. We'll be using these tools to step through the tutorial. I **strongly** encourage you to branch out by adding your own styles.

After you have given this documentation a once over go back and add your own data.

I would love to see you [create you own blocks](https://bost.ocks.org/mike/block/) to reference later. Your blocks are also helpful for other just getting started.

### Installation

### Why bar charts?

Our goal when visualizing data is to get a message across to the viewer as efficiently and accurately as possible. To do this we need to choose our encodings wisely. Not always, but very often, bar charts are a great choice.

![Preattentive Attributes](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/preattentive-attributes.png)

The image above displays several attributes we can manipulate with our data. Which attributes you choose will affect how your data is precieved. Duh, right? Well, not every encoding is created equally.

Length happens to be one of the best, if not the best, tool for comparing factors along one dimension. Sometimes the best solution is the simplest.

### Work flow
1. Get the data
    * Categorical: What factors will you aggregate your data by.
    * Quantitative: Choose a measure to define the weight of visual encoding.
2. Think about your messaging
    * When you create a bar chart you are each bar has a different length. Meaning each bar has a different ability to grab our attention. We want to create an axis such that each bar has as much length as possible. The limit here is the size of your screen. We can also sort our bars. Sorting the bars properly brings the most important information to our attention that much faster.
3. Code
		1. Put up the raw HTML skeleton
    2. Title
    3. Create Space for Your Chart
    4. Position a g element using the margin convention
    5. Declare scales and axis
    6. Bring in the data
    7. Sort the data to bring our insight to the viewers attention
    8. Set the domain
    9. Append Our Axis
    10. Add bars
    11. Apply Styles

### Let's Get Going

#### Our Data

We're working with a csv file you can access [here](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/data.csv). You may notice that the canonicle Let's Make a Bar Chart uses a tsv file. I wanted to make this walk through even more universal ,so I converted that file into a csv for you.

#### What Message Do We Want to Communicate

Like I said above, bar charts always have an angle. Since our data is ordinal by nature, we have a choice. And what I mean by ordinal is that there is an implied order. Other examples of ordinal data are the months of the year and ranking of Olymipic Metals. The alphabet has an implied order as well.

The choice we have to make in between respecting the order of the letters of the alphabet or sorting them by the measure defining the length of our bars. My argument is for sorting. I like to relieve our audience from as much as possible. Those who read our chart have plenty to make sense of already. Why not sort that so that the letters most frequently used in the english language pop out immediately. To leave the letters unsorted does tell the story of where along the alphabet are the most letters used, but that isn't the message here. We could also encode the vowels with a different hue so they stand out if we want to tell that story.

#### The Naked Bones

The documents we're driving with data live in the DOM, so we need to create some scaffolding to before we begin appending SVGs to our screen.

```html
<!DOCTYPE html>
<head>
  <meta charset="utf-8">
  <script src="https://d3js.org/d3.v4.min.js"></script>
  <style></style>
</head>
<body>
  <script></script>
</body>
```

#### Title

Every chart should have a role. The best way to define a charts purpose is by giving your chart a clear title. We'll do this with a simple p tag which will be styled later.

```html
<p>Relative frequencices of the letters of the English language</p>
```

Place the p tag inside your body tag just before the empty script tags.

#### Append Your svg and g to the Screen

Now that our screen has a message to tell we can create some space to tell our story. For that we need to place an SVG element on the screen will a smaller g positioned appropriately. You can read more about why we do this in the [Margin Convention](MARGIN CONVENTION LINK) docs.

Inside your script tags inserd the code below.

```javascript
var margin = {
    top: 20,
    right: 20,
    bottom: 30,
    left: 40
  };

var width = 960 - margin.left - margin.right;
var height = 500 - margin.top - margin.bottom;

var svg = d3.select("body").append("svg")
    .attr("width", width + margin.left + margin.right)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");
```

Here we are declaring a couple varibles used to set the size of our space. We are appending an svg to our body and g element to our svg. Again, why we append a g element to our SVG makes more sense in the Margin Convention documentation.

Note that 960x500 are demensions rendered inside bl.ocks.org. Feel free to change the size of your SVG to suit your needs. I trying to get into the habit of creating bl.ock friendly charts, which is why we're choosing those dimensions.

I hesitate to explain the transform attribute, becuase there is much more you can do then translate, but I will say this, translate takes a string in between the parenthesis in the the form of (x, y). If you want to use variables for the x,y make sure they converted into a string.

#### Create Scales and Axis

Some say scales are the most important device in all your D3 development. They're used to convert data into to pixels. An easier way to think of scales is by thinking of them as translating data space into screen space. If that still doesn't think about the metric conversion you need to do when you travel outside the United States. For someone like me who's used to gauging distance in miles, I feed kilometers into a converter and get miles in return. D3 scales take in our data and return a number that makes sense our screen.

```javascript
var x = d3.scaleLinear()
      .range([0, width]);

var y = d3.scaleBand()
    .range([height, 0]);
```

Place this code inside the script tags, just underneath the last block you copy/pasted.

This code is declaring a range for x from 0 to the width we've specified. The range is referring to screen space. Since we're creating horizontal bars, x is what we'll stretch our measure along. And since our measure is a continuous number we want to use a linear scale. We feed in a some value from our data and we'll get that value returned is if it were place on a number line. In this case our number line is the x-axis.

The y-axis is a bit different. We basically want a discrete row for each letter. In D3 those rows are called bands, when we're building a bar chart. If we were plotting circles we would be using scalePoint. Without getting into bands too deeply, I would encourage you to think about these bands as the space in between one letter and the next.

Also, note that we are only setting the range. We want to set up as much as we can before introducing the data as possible.

Now let's declare those axis generators.

```javascript
var xAxis = d3.axisTop(x)
    .ticks(10, "%");

var yAxis = d3.axisLeft(y);
```

You can place this just below the last code block you copy/pasted.

Axis generators in D3 do a good amount of work for us. They create text labels, tick marks and zero lines. Whether you want to see all those elements is your call, but D3 give them to you by default.

For our xAxis we chose axisTop so our text shows up above the line. The x argument we feed in there is our scale created earlier. Since our measure is a percentage we can format <Get a better understanding of what ticks is doing.>.

The only specification we state in our y-axis declaration is that we want the text to show on the left and to use the y scale we created earlier.

#### We're Ready for the Data

```javascript
d3.csv("data.csv", function(error, data) {
  if (error) throw error;

  data.forEach(function(d) {
    return d.frequency = +d.frequency;
  });

  data.sort(function(a, b) {
    return a.frequency - b.frequency;
  });

});
```

Insert this code just below the last block of code you copy/pasted.

Here we are using one of D3's utility functions <Find out what this is actually called.> to read in our data from the csv file.

After the data is read we need to do a bit of processing. The csv file format stores you data as strings. For D3 we are going to need to run some arithmetic operations and we cannot do that if our data isn't in a number format. Javascript keeps numerical format simple by only having one numerical data type, number. The easiest way to convert a string to a number in JavaScript is by placing a mathematical operator in front of the string. The compiler will look at the operation trying to be run and convert your string to a number. With a number can calculate the right scales and width each bar needs to be.

With or frequency data converted to a number we can also sort our bars approriately. See if you can figure out how our sorting function works on strings by commenting our the code block tied to the forEach and rerunning the code.

Remember, the reason we want to sort our bars is to bring the most important information to our viewers attention as quickly as possible.

#### Declare the Limits of Our Data

We are physically limited by the size of our screens. We need a way to communicate that limitation to our data. The scales created earlier are our means of communicating that message. Earlier when we delcare a range for each scale we were defining the physical limitations such as width and height. Now that we have data we can finish out our scales with domains.

```javascript
x.domain([0, d3.max(data, function(d) { return d.frequency; })]);

y.domain(data.map(function(d) { return d.letter; }))
  .paddingInner(0.1);
```

Copy/paste the code above just beneath the data.sort code block, but before the last closing bracket.

This code is adding domains to our x and y scales. To our x scale we want a domain from 0 to the heighest frequency value. For our y scale we just want to map each letter to an index value and give each horizontal bar a small amount of space in between. <Find out what units are used for the scale padding.>

#### Append Our Axis

Get excited, this is the first step where we get to see something on the screen!

```javascript
svg.append("g")
    .attr("class", "y axis")
    .attr("transform", "translate(-3, 0)")
    .call(yAxis);

svg.append("g")
    .attr("class", "x axis")
    .attr("transform", "translate(0,-3)")
    .call(xAxis);
```

Copy/paste this code just below the y.domain code, but inside the closing bracket.

To the g or group element we appended to the body earlier we're going to append two more group elements. One will have the ingredients of a y-axis and the other the ingredients of an x axis, per our specifications.

Everything in these to code blocks you've been introduced to before expect the .call(). The .call() is a method used to invoke our generators. <speak to this in more depth>

#### Draw Some Rectangles!

It's getting really fun now. We see some stuff on our screen and we can imagine where our bars are going to be. All that's left is putting them there and styling.

```javascript
svg.selectAll(".bar")
    .data(data)
  .enter().append("rect")
    .attr("class", "bar")
    .attr("x", 0)
    .attr("height", y.bandwidth())
    .attr("y", function(d) { return y(d.letter); })
    .attr("width", function(d) { return x(d.frequency); });
```

If you have gotten this far, then you probably know what I'm going to tell you to do by now.

Copy/paste the code above just below the last block you copy/pasted, but still insted the second to last closing bracket.

This code selects all of the bars, binds the .bar selection to data, enters the data bound elements to the DOM and appends one rect for each .bar selection. The other lines of code class each selection as bar and set a few attributes such as x, y, height and width. Each of these attributes are required before you get to see bars on the screen. Forget to assign values to one of these attributes and you don't have a full bar.

#### Time to Pain With CSS

In the intial html code I passed off to you, there was an opening and closing style tag. I want you to take the code below and place it in between those two tags.

```css
p {
  margin: 0px 0px 0px 20px;
  font-family: 'Montserrat';
  font-size: 1.93em;
  font-weight: normal;
}

text {
  font-family: 'Montserrat';
  font-size: 14px;
  font-weight: normal;
}

.bar {
  fill:  #0072c8;
}

.bar:hover {
  fill: #968C83;
}

.y path, .y stroke, .y line {
  display: none;
}

.x path, .x stroke {
  display: none;
  shape-rendering: crispEdges;
}

.y text {
  font-family: 'Open Sans';
  font-size: 14px;
  text-anchor: middle;
}

.x text {
  font-family: 'Open Sans';
  font-size: 10px;
  text-anchor: middle;
}
```

Save and rerun your code to see your freshly styled D3 bar chart!

If you'd like understand more about how CSS works please visit <howylearn.com> for more details.

You did it!!!

### Enhancements

### License

MIT