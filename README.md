# Zero to Bar Chart with D3 v4

### Who this is for?

This is a walk through for those just getting started with the D3 library or those familiar with the library looking for an alternative to the standard Let's Make a Bar Chart Part [I](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=4&cad=rja&uact=8&ved=0ahUKEwjclImNmZzPAhVD3mMKHUKOCQkQjBAIJTAD&url=https%3A%2F%2Fbl.ocks.org%2Fmbostock%2F7322386&usg=AFQjCNHLhVkHcxaoCx1W3A8aCLs4oU2Hqg&sig2=ITg7T7CwsOUK1U4hlDIgWw&bvm=bv.133178914,d.cGc), [II](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjclImNmZzPAhVD3mMKHUKOCQkQjBAIJzAC&url=https%3A%2F%2Fbost.ocks.org%2Fmike%2Fbar%2F2%2F&usg=AFQjCNHn4eRIkc_-KCxfy5VuH9hhKwxnmA&sig2=-MwD9VXrlgZFNpErVXM4XA&bvm=bv.133178914,d.cGc) and [III](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwjclImNmZzPAhVD3mMKHUKOCQkQjBAIIzAB&url=https%3A%2F%2Fbost.ocks.org%2Fmike%2Fbar%2F3%2F&usg=AFQjCNFNoLbYperkYjMEOdv2W9sUMjBTRQ&sig2=FG2GzLGfpUgCJLRH-yf44g&bvm=bv.133178914,d.cGc). If you haven't see those guides yet, you may want to start there. Not because this walk through's more difficult, but rather because those tutorials are likely to give you an even more robust foundation of knowledge.

### Who this is NOT for?

- Experts D3 developers
- Practitioners looking for D3 development best practices

### How to use

Before you get going, open up your favorite text editor, browser and the console. Caution, I haven't tested this code on any environments other than my own. If you have a Mac and would like to mirror my environment use [Sublime Text](https://www.sublimetext.com/3) and [Chrome](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&sqi=2&ved=0ahUKEwijzfmCnJzPAhUhHGMKHQHmDt0QFggqMAE&url=https%3A%2F%2Fwww.google.com%2Fchrome%2Fbrowser%2Fdesktop%2F&usg=AFQjCNEnCNpcuwbjwWkR_ZzY4O_v0ORT9A&sig2=PvJ2rGXR-yg4A3IPq-4Icw&bvm=bv.133178914,d.cGc). Sublime Text and Chrome also work on PCs, but the console will be a bit different.

Feel free to experiment as we develop. Tweaking the code can help drive concepts home and reveal potential gaps in understanding that wouldn't have been realized otherwise. Once finished do us all a favor and [create you own block](https://bost.ocks.org/mike/block/).

Blocks are refernces D3 developers use to learn. By contributing to [Blocks](bl.ocks.org) your adding ideas to a growing repository, making a portfolio for yourself and an easy refernce to past work you've done.

### Installation

Clone or download this repository to a directory to work from by clicking "Clone or download" button on the repos' landing page.

![Clone or download](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/clone-download.png)

Clicking presents a few more options.

![Clone or download options](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/clone-download-options.png)

I like to copy the url and clone the repo from the terminal. You may need to take a different approach if you don't have [git](https://git-scm.com/downloads) installed and don't want to work through the setup right now.

![Clone to desktop](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/clone-to-desktop.png)

Once I see that I'm in my Desktop in the terminal I can git clone.

![Cloned to desktop](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/cloned-to-desktop.png)

Now you should see the directory in your finder after cloning. If git clone doesn't work for you, you may need to enter `sudo git clone`.

> To save yourself from entering your password on every future git clone you'll want to set up [ssh-agent](http://stackoverflow.com/questions/10054318/how-to-provide-username-and-password-when-run-git-clone-gitremote-git), but this can be saved for later.

Now type `cd from-zero-to-bar-chart` in terminal to make that your active directory.

Once in that directory you can spin up simple server with Python. You do this be typing `ptyhon -m SimpleHTTPServer 8000` in you terminal.

Open an incognito tab in your Chorme browser and type `localhost:8000` into the address bar.

![Spin up a Simple Server](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/spin-a-simple-server.png)

When we finish you'll end up with a chart that looks like the image above. At the momement be happy if you have a browser open with no errors showing up in your console.

![no-errors](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/no-errors.png)

You can navigate to developer tool by following the selections above in your own incognito window or press option + command + j on your keyboard.

![developer tool](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/developer-tools.png)

### Why build a bar chart?

Our goal when visualizing data is to get a message across to the viewer as efficiently and accurately as possible. To do this we need to choose our encodings wisely. Not always, but very often, **bar charts** are the best choice.

![Preattentive Attributes](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/preattentive-attributes.png)

The image above displays several attributes we can manipulate with our data in D3. These preattentive attributes draw our attention to important areas or, if we aren't careful, accidentally the wrong information.

The attributes you choose affect how your data is precieved. Duh, right? Well, not every encoding is created equally. Length happens to be one of the best if not the best tool for comparing factors along a single measure. The simplest solution is sometimes the best.

### Work flow

1. [Gather the Data](#our-data)
2. [Think About Your Messaging](#think-about-your-massaging)
3. [Put up a Skeleton](#put-up-a-skeleton)
4. [Title](#title)
5. [Create Space for Your Chart](#create-space-for-your-chart)
6. [Create Scales and Axis](#create-scales-and-axis)
7. [Bring in the Data](#bring-in-the-data)
8. [Set the Domain](#set-the-domain)
9. [Draw the Axis](#draw-the-axis)
10. [Render Rectangles](#render-rectangles)
11. [Apply Styles](#apply-styles)

# Our Data

The csv can be accessed [here](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/data.csv). You should also be able to reference data.csv from your current working directory. If you're familar with [Let's Make a Bar Chart](https://bost.ocks.org/mike/bar/) then you'll recall manually input data used and a .tsv. To make things more familiar I converted the .tsv used in that guide into a .csv.

To make a bar chart our data needs two ingredients. Your data needs [both](http://regentsprep.org/regents/math/algebra/ad1/qualquant.htm) a qualitative and quantitative dimension. By this I mean you need a column with [categories](https://en.wikipedia.org/wiki/Categorical_variable) and a column with values. Idealy the data will be rolled up to one row per category. Those familar with SQL can think about this as a [GROUP BY](http://www.w3schools.com/sql/sql_groupby.asp) clause. JS practitioners may think of this one-to-one structure as a JSON [key-value pair](http://stackoverflow.com/questions/3715644/key-value-pairs-using-json).

Notice our data only has one row per letter...

![data-csv](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/data-csv.png)

[(back to Work Flow)](#work-flow)

---

# Think About Your Messaging

We have a choice to make between respecting the implicit order of the letters in the alphabet (see [ordinal data](https://en.wikipedia.org/wiki/Ordinal_data)) or sorting them by how often their used. For the sake of argument, I'm going to side with the choice of sorting. Sorting relieves a huge amount of work for those reading our chart. Even though our chart's relatively simple unsorted bars are much harder to reason. Sorting brings those letters most frequently used to readers attention immediately.

[(back to Work Flow)](#work-flow)

---

# Put up a Skeleton

For those who don't know, D3 stands for Data Driven Documents. The documents we're driving with data live in the DOM. So, the first thing to do is to put up the scaffolding.

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

> You may want to use this code as a boiler plate for future D3 development projects.

If there was already code in your index.html file, go ahead and delete it all. Then copy/paste the code above into the page.

![empty](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/empty-dom.png)

This gets you started with a blank HTML page.

[(back to Work Flow)](#work-flow)

---

# Title

Every chart has a role to play. How do we know what this chart does? One way is by giving your chart a clear title. We'll do this with a simple p tag.

```html
<p>Relative frequencices of the letters of the English language</p>
```

Place the p tag in between your opening and closing body tags.

![chart title](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/chart-title.png)

Now you should see an unformatted title awaiting a chart.

[(back to Work Flow)](#work-flow)

---

# Create Space for Your Chart

Now that we know what our chart is meant to do we need space to tell our story. For that we need to place an svg element on the screen with a g inside. You can read more about the convention we're using [here](https://bl.ocks.org/mbostock/3019563).

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

Copy/paste the code above inside your script tags.

![svg and g inserted](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/svg-g-inserted.png)

We have declared varibles used to set the size of our chart. We appended an svg to our body and g element to the svg.

The 960x500 demensions are used in [Blocks](bl.ocks.org). To be more supportive of the community, it's nice to build charts easily ported over. Feel free to change the dimensions for the sake of experimentation or for you own reasons.

Don't worry about the transform attribute for now. We will get into more later on. For now just know the translate argument takes a string in the form of (x, y) between the parenthesis.

[(back to Work Flow)](#work-flow)

---

# Create Scales and Axis

Some say scales are the most important features of the D3 library. In the context of a bar chart, we will use them to convert data into to pixels. This translations helps us create nicely size rectangles, but the scales can be applied to much more interesting applications.

```javascript
var x = d3.scaleLinear()
      .range([0, width]);

var y = d3.scaleBand()
    .range([height, 0]);
```

Place this code inside the script tags, just underneath the last block you copy/pasted.

The code above declares an x.range(screen space) from 0 to width. The x-axis is the axis we'll spread our horizontal bars across. And since frequency is a [continuous number](http://stattrek.com/statistics/dictionary.aspx?definition=Continuous%20variable) we want to use a [linear scale](https://github.com/d3/d3-scale/blob/master/README.md#scaleLinear).

The y-axis is a bit different. What we want is a discrete row for each letter. When building a bar chart our rows are referred to as [bands](https://github.com/d3/d3-scale/blob/master/README.md#scaleBand). If we were plotting circles we would be using [scalePoint](https://github.com/d3/d3-scale/blob/master/README.md#scalePoint).

Now let's declare those axis generators.

```javascript
var xAxis = d3.axisTop(x)
    .ticks(10, "%");

var yAxis = d3.axisLeft(y);
```

You can place this just below the last code block you copy/pasted.

Axis generators in D3 do a lot of work. They create paths, tick, text and lines for us to format further.

For our xAxis we chose axisTop to position our text above the line. The x argument we feed in is the scale created earlier. With a fractional measure we want to format the text over the ticks as percentages with a precision to the tenths place.

The only specification we pass to our y-axis is to show the text on the left and to use the y scale created earlier.

Nothing will change visually before we call the scales.

[(back to Work Flow)](#work-flow)

---

# Bring in the Data

```javascript
d3.csvParse("data.csv", function(error, data) {
  if (error) throw error;

  data.forEach(function(d) {
    return d.frequency = +d.frequency;
  });

  data.sort(function(a, b) {
    return a.frequency - b.frequency;
  });
});
```

Insert this code just below the last block you copy/pasted.

Here we use a helpful feature of the D3 API to parse csv data. D3 also has parsers for .tsv, .json and .dsv which as custom delimeted value.

Once the data is read we need to do a bit more processing. Be defual csv files store all your data as strings. This can be a problem for calculations, like the width of our bars. Thankfully, the data set is small, so a simple loop over each value will convert them from a string to a number.

With or frequency data converted to a number we can also sort our bars. The rows of our data wouldn't sort correctly if we hadn't converted the strings to numbers before sorting.

> Remember, the reason we sort our bars is to bring the most important information to our viewers attention as quickly as possible.

[(back to Work Flow)](#work-flow)

---

# Set the Domain

How do we specify were the ends of our bars should land?

![input-domain](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/input-domain.png)

D3 scales to the rescue! Earlier when we delcared a range for each scale we were defining the physical limitations such as width and height. Now that we have data we can complete our scales by adding domains.

```javascript
x.domain([0, d3.max(data, function(d) { return d.frequency; })]);

y.domain(data.map(function(d) { return d.letter; }))
  .paddingInner(0.1);
```

Copy/paste the code above just beneath the data.sort code block, but before the last closing bracket of the function reading in your data.

This adds domains to our x and y scales. To our x scale we want a domain from 0 to the heighest frequency value. For our y scale we just want to map each letter to an index value and give each row a bit of space in between. The paddingInner defines what percent of each row should be left for spacing in between the bars.

[(back to Work Flow)](#work-flow)

---

# Draw the Axis

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

Copy/paste this code just below the y.domain code, but inside the closing bracket of the function reading in data.

![add axis](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/add-axis.png)

We just appended two more g elements to the intial g element positioned inside the svg. Could that sound any more abstract?

One of the g elements will have the ingredients of a y-axis and the other the ingredients of an x axis, per our specifications.

Everything in these code blocks you've been introduced to before except the .call(). The .call() is a method used to invoke our generators. The [.call](https://github.com/d3/d3-selection/blob/master/README.md#selection_call) is a consice way for us to call the axis functions created earlier while keeping them bound to our selections.

[(back to Work Flow)](#work-flow)

---

# Render Rectangles

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

If you have gotten this far, then you probably know what I'm going to tell you to do next.

Copy/paste the code above just below the last block you copy/pasted, but inside the the closing braket of the function that read in the data.

![draw rectangles](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/draw-rectangles.png)

This code selects all of the bars, binds the .bar selection to data, enters the data bound elements to the DOM and appends one rect for each .bar selection. The other lines of code class each selection as `.bar` and set a few attributes such as x, y, height and width. Each of these attributes are required before you get to see bars on the screen. Forget to assign values to one of these attributes and you won't have any bars to show.

[(back to Work Flow)](#work-flow)

---

# Apply Styles

In the intial html code there was an opening and closing style tag inside the head tag. I want you to take the code below and place it in between those two style tags.

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

```html
<link href="https://fonts.googleapis.com/css?family=Montserrat|Open+Sans:300" rel="stylesheet">
```

For good measure place the line of code above in between line 3 and 4 of your index.html document.

![Congratulations](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/images/you-did-it.png)

If you'd like understand more about how CSS works visit [Getting to Know CSS](http://learn.shayhowe.com/html-css/getting-to-know-css/).

Congratulations, you did it!

[(back to Work Flow)](#work-flow)