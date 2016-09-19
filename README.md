# Zero to Bar Chart with D3 v4

### Who is this for?

This is a walk through for those just getting started with the D3 library or those familiar with the library looking for an alternative to the standard Let's Make a Bar Chart Part [I](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=4&cad=rja&uact=8&ved=0ahUKEwjclImNmZzPAhVD3mMKHUKOCQkQjBAIJTAD&url=https%3A%2F%2Fbl.ocks.org%2Fmbostock%2F7322386&usg=AFQjCNHLhVkHcxaoCx1W3A8aCLs4oU2Hqg&sig2=ITg7T7CwsOUK1U4hlDIgWw&bvm=bv.133178914,d.cGc), [II](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjclImNmZzPAhVD3mMKHUKOCQkQjBAIJzAC&url=https%3A%2F%2Fbost.ocks.org%2Fmike%2Fbar%2F2%2F&usg=AFQjCNHn4eRIkc_-KCxfy5VuH9hhKwxnmA&sig2=-MwD9VXrlgZFNpErVXM4XA&bvm=bv.133178914,d.cGc) and [III](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&ved=0ahUKEwjclImNmZzPAhVD3mMKHUKOCQkQjBAIIzAB&url=https%3A%2F%2Fbost.ocks.org%2Fmike%2Fbar%2F3%2F&usg=AFQjCNFNoLbYperkYjMEOdv2W9sUMjBTRQ&sig2=FG2GzLGfpUgCJLRH-yf44g&bvm=bv.133178914,d.cGc). If you haven't see those yet, you may want to start there. Not because this walk through's more difficult, but rather because those tutorials are likely to give you an even more robust foundation of knowledge.

This aim of this tutorial is walk you through the create of a bar chart with v4 and little more.

### Who is this NOT for?

- Experts D3 developers
- Those comfortable feeling there own way around the documentation
- Practitioners looking for D3 development best practice

### How to use this

Before you get going open up your favorite text editor, browser and the console. I haven't tested this code on any other environments than the one I am currently working with. If you have a Mac and would like to mirror my tool set use [Sublime Text](https://www.sublimetext.com/3) and [Chrome](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=2&cad=rja&uact=8&sqi=2&ved=0ahUKEwijzfmCnJzPAhUhHGMKHQHmDt0QFggqMAE&url=https%3A%2F%2Fwww.google.com%2Fchrome%2Fbrowser%2Fdesktop%2F&usg=AFQjCNEnCNpcuwbjwWkR_ZzY4O_v0ORT9A&sig2=PvJ2rGXR-yg4A3IPq-4Icw&bvm=bv.133178914,d.cGc). Sublime Text and Chrome also work on PCs, but the console will be a bit different.

Feel free to experiment as we develop. Tweaking the code can help drive to concepts home and reveal potential gaps in understanding you wouldn't have realized otherwise. Once finished, you should do us all a favor and [create you own block](https://bost.ocks.org/mike/block/). Blocks are refernces all D3 developers use to learn and up there skills. By contributing to bl.ocks.or your adding ideas to a growing repository, making a portfolio for yourself and an easy refernce to past work you've done.

### Installation

Clone or download this repository to a directory you would like to work from by clicking the Clone or download button on the repos' landing page.

![Clone or download](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/clone-download.png)

This presents a few options.

![Clone or download options](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/clone-download-options.png)

I like to take the terminal route by copying the url and cloning the repo with terminal. You will want to approach this differently if you don't have [git](https://git-scm.com/downloads) installed and don't want spend the time right now setting it up. However, I will encourage to take some time getting familiar with git. It's an amazing tool. By far the most heavily utilized software engineered for open source contribution.

![Clone to desktop](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/clone-to-desktop.png)

For this example, I'll clone the repo onto my desktop.

![Cloned to desktop](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/cloned-to-desktop.png)

You should see this directory in your finder after cloning. If git clone doesn't work for you, you may need to enter sudo git clone. To save yourself from entering your password on every future git clone you'll want to set up [ssh-agent](http://stackoverflow.com/questions/10054318/how-to-provide-username-and-password-when-run-git-clone-gitremote-git), but this can be saved for later.

Now type cd from-zero-to-bar-chart in terminal to make that your active directory.

Once in that directory you can spin up simple server with Python. You do this be typing ptyhon -m SimpleHTTPServer in you terminal.

Open an incognito tab in your Chorme browser and type localhost:<and the active port> into the address bar.

![Spin up a Simple Server](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/spin-a-simple-server.png)

The finished product looks thusly :) Ready to walk through it step by step?

### Why bar charts?

Our goal when visualizing data is to get a message across to the viewer as efficiently and accurately as possible. To do this we need to choose our encodings wisely. Not always, but very often, bar charts are a great choice.

![Preattentive Attributes](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/preattentive-attributes.png)

The image above displays several attributes we can manipulate with our data. These preattentive attributes can be used to bring attention to important areas or accidentally misinform, if we aren't careful. The attributes you choose affect how your data is precieved. Duh, right? Well, not every encoding is created equally.

Length happens to be one of the best if not the best tool for comparing factors along one dimension. The simplest solution is sometimes the best solution.

### Work flow

1. Gather the data
2. Think about your messaging
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

---

#### Our Data

---

The csv can be accessed [here](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/data.csv). Data.csv should also be in your current working directory. If you're familar with [Let's Make a Bar Chart](https://bost.ocks.org/mike/bar/) then you'll know they use a combination of manually input data and a .tsv. To make things a bit more familiar I converted the same .tsv into a .csv.

In order to make a bar chart with D3 your data needs two ingredients. Your data needs [both](http://regentsprep.org/regents/math/algebra/ad1/qualquant.htm) a qualitative and quantitative dimension. By this I mean you need a column with [categories](https://en.wikipedia.org/wiki/Categorical_variable) and a column with values. Idealy the data will be rolled up to one row per category. Those familar with SQL will think about this as a [GROUP BY](http://www.w3schools.com/sql/sql_groupby.asp) clause. JS practitioners may think of this one-to-one structure as a key-value pair.

Notice our data only has one row per letter...

![data-csv](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/data-csv.png)

#### What Message Do We Want to Communicate

---

The choice we have to make is between respecting the order of the letters in the alphabet (see [ordinal data](https://en.wikipedia.org/wiki/Ordinal_data)) or sort them by the measure defining the length of our bars. I would make the argument for sorting. I think sorting relieves a huge amount of work. Those reading our chart have plenty to make sense of already. Why not sort so the letters most frequently used pop out immediately?

To leave the letters unsorted does tell the story of where along the alphabet the most letters used lie, but that isn't the message here. We could also encode the vowels with a different hue so they stand out. At the end of the day, the success of our chart depends how effectively we communicate the important messages.

#### Bare Bones DOM

For those who don't know, D3 stands for Data Driven Documents. The documents we're driving with data live in the DOM. The first thing you want to as you start to code involves putting up some scaffolding.

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

Empty out the index.html file, if it isn't already, and copy/paste the code above into the page.

![empty](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/empty-dom.png)

#### Title

---

Every chart has a role to play. How do we know what this chart is meant to do? One way is by giving your chart a clear title. We'll do this with a simple p tag.

```html
<p>Relative frequencices of the letters of the English language</p>
```

Place the p tag inside your body tag just before the empty script tags.

![chart title](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/chart-title.png)

#### Append Your svg and g to the Screen

Now that we know what our chart's meant to do we need space to tell our story. For that we need to place an svg element on the screen with a smaller g placed inside. You can read more about this convention [here](https://bl.ocks.org/mbostock/3019563).

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

![svg and g inserted](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/svg-g-inserted.png)

Here we declare varibles used to set the size of our chart. We append an svg to our body and g element to the svg. Again, why we append a g element to our svg makes more sense in the [Margin Convention](https://bl.ocks.org/mbostock/3019563) documentation.

Note that 960x500 are demensions rendered inside bl.ocks.org. Feel free to change the size. Personally, I'm trying to get into the habit of creating bl.ock friendly charts. So, that's why we choose those dimensions here.

Don't worry about the transform attribute for now. We will get into more later on. For now just know the translate argument takes a string in the form of (x, y) between the parenthesis.

#### Create Scales and Axis

---

Some say scales are the most features of the D3 library. In this context, we will use them to convert data into to pixels, but they can be used for much much more.

Think of scales as a function translating data space into screen space. If that still doesn't resonate think about metric conversions. Those from the states who travel to other countries quickly realize distance is measured differently. Someone used to gauging distance in miles would feed kilometers into a converter and get miles to get a read out in miles. D3 scales take in our data and return a number that fits our our screen.

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

Axis generators in D3 do a lot of work. They create text labels, tick marks and zero lines. Whether you want to see all those elements is your call, but D3 give them to you by default.

For our xAxis we chose axisTop so our text shows up above the line. The x argument we feed in is the scale created earlier. Since our measure is a percentage we can format the ticks as such with precision to the tenths place.

The only specification we state in our y-axis is that we want the text to show on the left and to use the y scale created earlier.

Nothing changing visually, because we haven't called the scales.

#### We're Ready for the Data

---

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

Here we use a helpful feature of the D3 API to parse data in a csv format.

Once the data is read in we need to do a bit more processing. Csv files store all your data as strings. This can be a probably when you need to calculate the width of bars. Thankfully, this data set is small, so a simple loop over each frequency value can convert them from a string to a number.

With or frequency data converted to a number we can also sort our bars. Remember, the reason we sort our bars is to bring the most important information to our viewers attention as quickly as possible.

You still won't see anything different aesthetically.

#### Declare the Limits of Our Data

---

![input-domain](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/input-domain.png)

How do we specify were the ends of our bars should land?

D3 scales to the rescue! Earlier when we delcare a range for each scale we were defining the physical limitations such as width and height. Now that we have data we can finish out our scales with domains.

```javascript
x.domain([0, d3.max(data, function(d) { return d.frequency; })]);

y.domain(data.map(function(d) { return d.letter; }))
  .paddingInner(0.1);
```

Copy/paste the code above just beneath the data.sort code block, but before the last closing bracket.

This code is adding domains to our x and y scales. To our x scale we want a domain from 0 to the heighest frequency value. For our y scale we just want to map each letter to an index value and give each row a bit of space in between. The paddingInner defines what percent of each row should be left for spacing in between the bars.

#### Append Our Axis

---

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

![add axis](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/add-axis.png)

We just append to more g element to the intial g element positioned inside the svg. Could that sound any more abstract? One of the g elements will have the ingredients of a y-axis and the other the ingredients of an x axis, per our specifications.

Everything in these code blocks you've been introduced to before except the .call(). The .call() is a method used to invoke our generators. The [.call](https://github.com/d3/d3-selection/blob/master/README.md#selection_call) is a consice way for us to call the axis functions created early while keeping them bound to our selection.

#### Draw Some Rectangles!

---

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

![draw rectangles](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/draw-rectangles.png)

This code selects all of the bars, binds the .bar selection to data, enters the data bound elements to the DOM and appends one rect for each .bar selection. The other lines of code class each selection as bar and set a few attributes such as x, y, height and width. Each of these attributes are required before you get to see bars on the screen. Forget to assign values to one of these attributes and you won't have any bars to show.

#### Time to Pain With CSS

---

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

```html
<link href="https://fonts.googleapis.com/css?family=Montserrat|Open+Sans:300" rel="stylesheet">
```

For good measure place the line of code above in between line 3 and 4 of your index.html document.

![Congratulations](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/you-did-it.png)

If you'd like understand more about how CSS works please visit <howylearn.com> for more details.

## You did it!!!

### Enhancements

### License

MIT