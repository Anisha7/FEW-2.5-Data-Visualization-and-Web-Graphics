
# FEW 2.5 - D3 Intro

<!-- Put a link to the slides so that students can find them -->

➡️ [**Slides**](https://make-school-courses.github.io/FEW-2.5-Data-Visualization-and-Web-Graphics/Slides/Lesson-9.html ':ignore')

<!-- > -->

## Minute-by-Minute

| **Elapsed** | **Time**  | **Activity**              |
| ----------- | --------- | ------------------------- |
| 0:00        | 0:05      | Overview and Learning Outcomese                |
| 0:05        | 0:05      | D3 Intro                  |
| 0:10        | 0:10      | Explore D3       |
| 0:20        | 0:30      | Getting Started                     |
| 0:50        | 0:10      | Loading Data      |
| 1:00        | 0:30      | SVG      |
| 1:30        | 0:10      | BREAK      |
| 1:40        | 1:00      | Lab      |
| 2:40        | 0:05      | Wrap up review objectives |
| TOTAL       | 2:45      | -                         |


<!-- > -->

## Overview

D3 is a library that has been around for a long time. It's more of a toolkit for making visualizations with JavaScript. It's the first namer that comes when conversation turns to making data visualizations with JS.

## Why you should know this

It's the tool that wrote the book on data visualization with JS. You can do just about anything with D3. It has huge flexibility and deep toolset. It also has a steep learning curve.

<!-- > -->

## Learning Objectives

- Identify use cases for D3
- Define data used by D3
- Create simple visualizations with D3

<!-- > -->

## D3

D3 - Data Driven Documents describes itself as:

> D3.js is a JavaScript library for manipulating documents based on data. D3 helps you bring data to life using HTML, SVG, and CSS. D3’s emphasis on web standards gives you the full capabilities of modern browsers without tying yourself to a proprietary framework, combining powerful visualization components and a data-driven approach to DOM manipulation.

What does it do? Data visualization! You could say D3 wrote the book on data visualization with JavaScript.

<!-- > -->

## How does it work?

D3 does so much it's hard to answer that. It draws things from data. It binds to data, meaning it will update when the data changes. It handles animation and interactions. It can load data and manipulate the DOM.

D3 is more of a toolbox with tools that are focussed on drawing things on the screen from a datasets.

<!-- > -->

## Explore D3.

Go to the [D3 hompage](https://d3js.org), and take a look at the examples on the D3 home and [examples pages](https://github.com/d3/d3/wiki/Gallery).

**Find an example that you think is interesting to show to the group and answer the question: _why is this interesting?_**

D3 is complex. With that complexity comes a lot of flexibility. Expect a steep learning curve!

<!-- > -->

## Getting started

Link to the library from the CDN:

`<script src="https://d3js.org/d3.v5.min.js"></script>`

You can find this link on the [D3 hompage](https://d3js.org)

Select an element to work with. You will be adding or modifying elements within this one. Here we are selecting the body:

```JS
d3.select('body')
```

<!-- v -->

Next select the elements you want to modify or create. In this case we are selecting divs. It doesn't matter that there no existing divs.

```JS
d3.select('body')
	.selectAll('div')
```

<!-- v -->

Next add some data. Data can be an array containing any type of data. Each element of the array will be processed. For this example I've used an array of numbers.

```JS
d3.select('body')
	.selectAll('div')
	.data([5,6,2,8,4,9,1])
```

<!-- v -->

Next call `enter()`. Calling this method tells D3 to add new elements if they don't exist.  

```JS
d3.select('body')
	.selectAll('div')
	.data([5,6,2,8,4,9,1])
	.enter()
```

<!-- v -->

Use `append()` to tell D3 what type of element to append.

```JS
d3.select('body')
	.selectAll('div')
	.data([5,6,2,8,4,9,1])
	.enter()
	.append('div')
```

<!-- v -->

Set the text of each new node. This method takes a function which receives one of the data values and should return the text to display in the node.

```JS
d3.select('body')
	.selectAll('div')
	.data([5,6,2,8,4,9,1])
	.enter()
	.append('div')
	.text((d) => d)
```

<!-- v -->

The `style()` method takes two parameters. First is the style attribute to set, and second is either a function or a primitive value.

```JS
d3.select('body')
	.selectAll('div')
	.data([5,6,2,8,4,9,1])
	.enter()
	.append('div')
	.text((d) => d)
	// When the second parameter is a primitive value, the value is returned.
	// Look at: padding, background-color, and margin.
	.style('padding', '1em')
	.style('background-color', 'red')
	.style('margin', '1px')
	// When the second parameter is a function, the function receives
	// a data value and returns a value.
	// See the width. Here the value is normalized and returned as a %.
	.style('width', (d) => `${d / 10 * 100}%`)
```

<!-- > -->

## Loading Data

D3 has its own data loaders built in. D3 works with: JSON, CSV, and a few other data types. Read more [here](https://github.com/d3/d3/blob/master/API.md#fetches-d3-fetch).

See the loading data example below. Notice this uses a Promise:

Load a JSON Object:

```JS
d3.json('metal.json')
		.then(json => console.log(json))
```

Load a CSV object.

```JS
// CSV
	d3.csv('metal_bands_2017.csv')
		.then(csv => console.log(csv))
```

<!-- > -->

## SVG

The earlier example used HTML, created HTML elements, and set CSS styles on those elements. D3 is also happy to work with SVG.

SVG and HTML are closely related. Imagine HTML as a language for sharing and displaying text documents, and SVG as a language for sharing and displaying graphical images. Both languages share the same parent language.  

<!-- v -->

Remember these SVG tags to get started:

- rect - Rectangle
- circle - Circle
- ellipse - Elipse
- g - Group
- line - Line
- path - Path
- polygon - Polygon
- and [many more...](https://developer.mozilla.org/en-US/docs/Web/SVG/Element)

Take a look at the list of SVG tags what do you see there?

<!-- v -->

### Activity

**Pair up and explore a section of the SVG tag list.**

<!-- v -->

### Making SVG happen

D3 writes SVG for us!

SVG tags have different names and many new and different attributes!

Try it for yourself with these challenges:

- Make an svg tag
	- `<svg id="svg" width="500" height="500"></svg>`
- Make an array of objects
	- Give each object three properties, each assigned a random value.

<!-- v -->

Select the SVG element by its id name and give it a CSS style.

```JS
d3.select('#svg')
	.style('border', '1px solid')
```

<!-- v -->

Select all of the `rect`s. None exist yet. Add data. Then call enter to start creating elements from the dataset.

```JS
d3.select('#svg')
	.style('border', '1px solid')
	.selectAll('rect')
	.data(data)
	.enter()
```

<!-- v -->

Set attributes on SVG rect. Below we've set the height and width to the value at the `c` key in the data, and used transform to move the rect `x` and `y` position based on the values at keys `a` and `b`.

```JS
d3.select('#svg')
	.style('border', '1px solid')
	.selectAll('rect')
	.data(data)
	.enter()
	.append('rect')
	.attr('height', (d) => d.c * 50)
	.attr('width', (d) => d.c * 50)
	.attr('transform', (d, i) => `translate(${500 / 50 * i}, ${500 - d.a * 500})`)
```

<!-- v -->

### Activity

Answer the following questions:

- What happened in the examples above?
- How would you incorporate data from another source?
- How would you modify the appearance?

<!-- > -->

<!-- .slide: data-background="#087CB8" -->
## [**10m**] BREAK

<!-- > -->

## Lab

Choose an example or tutorial from the D3 site and recreate that example with your own dataset.

**Stretch Challenge:** Recreate a second example. The goal here is to get familiar with D3 to use later in your projects

<!-- > -->

## After class

- Continue working on your [Final Visualization 3](Assignments/Data-Visualization-3.md), due 3/4 9:30am
