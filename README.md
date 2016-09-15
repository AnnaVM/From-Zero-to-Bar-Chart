# Zero to Bar Chart with D3 v4

### Who is this not for
- Experts D3 developers
- Those comfortable feeling there own way around the documentation
- Practitioners looking for D3 development best practice

### How to use this
Before you get going, you should have text editor in front of you, a browser open as well as the console open. We'll be using these tools to step through the tutorial. I **strongly** encourage you to branch out by adding your own styles.

After you have given this documentation a once over go back and add your own data.

I would love to see you [create you own blocks](https://bost.ocks.org/mike/block/) to reference later. Your blocks are also helpful for other just getting started.

### Why bar charts?

Our goal when visualizing data is to get a message across to the viewer as efficiently and accurately as possible. To do this we need to choose our encodings wisely. Not always, but very often, bar charts are a great choice.

![Preattentive Attributes](https://github.com/rcrocker13/From-Zero-to-Bar-Chart/blob/master/preattentive-attributes.png)  */
The fuzzy picture above displays server form attributes we can choose from when encoding data. I have put a box around length to draw your attention to the form of focus in the tutorial.

- They work
- There are basic
- Best practices are often over looked

### Work flow
1. Get the data
    * Categorical
    * Quantitative
2. Think about your messaging
3. Code
    1. Title
    2. Append your svg to the body
    3. Position a g element using the margin convention
    4. Declare scales and axis
    5. Bring in the data
    6. Sort the data to bring our insight to the viewers attention
    7. Set the domain
    8. Add bars

### Enhancements

### License

MIT