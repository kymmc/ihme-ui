![travis badge](https://travis-ci.org/ihmeuw/ihme-ui.svg) [![codecov.io](https://codecov.io/github/ihmeuw/ihme-ui/coverage.svg?branch=master)](https://codecov.io/github/ihmeuw/ihme-ui?branch=master)

# [IHME-UI](https://github.com/ihmeuw/ihme-ui)

ihme-ui is a collection of JavaScript and React-based visualization tools and user interface elements developed by the [Institute of Health Metrics and Evaluation](http://healthdata.org). These elements are used in IHME's [visualizations of global health metrics](http://www.healthdata.org/results/data-visualizations).

This document provides installation instructions, an overview of the elements, their APIs, and examples of their use.

* [Installation](#installation)
* [API Reference](#api)
  * [axis](#axis)
  * [axis-chart](#axis-chart)
  * [button](#button)
  * [choropleth-legend](#choropleth-legend)
  * [group](#group)
    * [options](#options)
  * [html-label](#html-label)
  * [reponse-container](#response-container)
  * [shape](#shape)
    * [area](#area)
    * [line](#line)
    * [multi-line](#multi-line)
    * [scatter](#scatter)
    * [symbol](#symbol)
  * [slider](#slider)
  * [spinner](#spinner)
  * [svg-text](#svg-text)
* [Test Utilities](#test-utilities)
  * [Data Generator](#data-generator)
* [Code Quality](#code-quality)

###### WORK IN PROGRESS: Not stable until v1.0.0

---

## Installation

Requirements:

* Node: ≥ v5.1.1

To install ihme-ui tools and all dependencies:

```sh
npm install -S ihme-ui
```
To install demo files:

```sh
npm run demo
```

## API

### <a id="axis"></a>axis

Chart axes with customizable scales and ticks.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`position` | no | object | where to position ticks relative to axis line; will match an AXIS_TYPE (default: bottom)<br /><br />one of: top, right, bottom, left
`scale` | yes | object | appropriate scale for object
`style` | no | object | style object to apply to element
`ticks` | no | number | [number of axis ticks use](https://github.com/d3/d3-axis#axis_ticks)
`tickFormat` | no | object | [format of axis ticks ticks](https://github.com/d3/d3-axis#axis_tickFormat)
`tickPadding` | no | number | [padding of axis ticks](https://github.com/d3/d3-axis#axis_tickPadding) (default: 3px)
`tickSize` | no | number | [size of both inner and outer tick lines](https://github.com/d3/d3-axis#axis_tickSize) (default: 6)
`tickSizeInner` | no | number | [size of inner tick lines](https://github.com/d3/d3-axis#axis_tickSizeInner) (default: 6)
`tickSizeOuter` | no | number | [size of outer tick lines](https://github.com/d3/d3-axis#axis_tickSizeOuter) (default: 6)
`tickValues` | no | object | [user-specified tick values](https://github.com/d3/d3-axis#axis_tickValues) (default: automatic)
`translate` | no | object | push axis in x or y direction

### axis-chart

Chart with customizable width, height, scales, and padding.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`children` | no | object | React element or elements<br /><br />one of type: arrayOf(PropTypes.node), node
`className` | no | string, object | class names to appended to the element
`height` | no | number | pixel height of line chart
`padding`| no | number | padding around the chart contents (default: top:20 right:20 bottom:30 left:50)
`width` | no | number | pixel width of line chart
`xDomain` | no | object | [min, max] for xScale (i.e., the domain of the data)
`xScaleType`| no | object | type of x scale<br /><br />pne of: band, linear, ordinal, point
`yDomain` | no | object | [min, max] yScale (i.e., the range of the data)
`yScaleType` | no | object | type of y scale<br /><br />one of: band, linear, ordinal, point

### button

Button with customizable id, name, class name, icon, animation, and click handler.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`className` | no | string, object | array of classes to add to button<br /><br />one of type: string, object, array
`clickHandler` | no | object | function to be executed on click
`disabled` | no | boolean | boolean value to set button as disabled
`icon` | no | string | path to image to render within button tag
`id` | no | string | id value for button
`name` | no | string | name of button
`showSpinner` | no | boolean | boolean value to display spinner
`text` | no | string | text to render within button tag
`theme` | no | string | color scheme of component (see button.css)

### choropleth-legend

Choropleth map legend with customizable color steps, color scale, data, appearance, and interaction handlers.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`colorSteps` | yes | object | array of color steps, e.g. ['#fff', '#ccc', '\#000', ...]
`colorScale` | yes | object | function that accepts data as a parameter and returns color
`data` | yes | object | array of datum objects
`domain` | yes | object | [min, max] for xScale; xScale positions <circles> and provides axis
`keyField` | yes | string | uniquely identifying property of datum, e.g., location_id
`margins` | no | object | margins to subtract from width and height
`onClick` | no | object | onClick function for DensityPlot circles
`onMouseOver` | no | object | onMouseOver function for DensityPlot circles
`onSliderMove` | no | object | callback function to attach to slider handles
`rangeExtent` | yes | object | array of [min, max] for slider in data space
`valueField` | yes | string | property of datum object that holds value
`unit` | no | string | unit of data; axis label
`width` | yes | number | width of element in pixels
`x1` | no | number | x-axis coord (as percentage) of the start of the gradient (e.g., 0)
`x2` | no | number | x-axis coord (as percentage) of the end of the gradient (e.g., 100)
`zoom` | no | number | float value used for implementing "zooming"; any element that needs to become larger in "presentation mode" should respond to this scale factor.<br /><br />Guide: <br />zoom: 0 -> smallest possible<br />zoom: 0.5 -> half of normal size<br />zoom: 1 -> normal<br />zoom: 2 -> twice normal size

### group

Button set with `selectable` property and customizable class names and interaction handlers.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`children` | yes | object |  React element or elements<br /><br />one of type: arrayOf(PropTypes.node), node
`className` | no | string, object | one of type: string, object, array
`clickHandler` | no | object | clickHandler function with following signature: function({ value })
`disabledItems` | no | number, string, object | one of type: arrayOf(number), arrayOf(string), number, string
`hoverHandler` | no | object |
`selectedItems` | no | number, string, object | one of type: arrayOf(number), arrayOf(string), number, string
`theme` | no | string | color scheme of component (one of: 'dark', 'light', 'common')

#### options

Options for the group element, wrapped by group.

Property | Required | Type(s) | Description
        --- | :---: | :---: - | ---
`className` | no | string, object | one of type: string, object, array
`clickHandler` | no | object |
`disabled` | no | boolean | boolean value to apply disabled class styling
`hoverHandler` | no | object |
`icon` | no | string | path to image to render within label tag
`selected` | no | boolean | boolean value to apply selected class styling
`text` | no | string | text to render within label tag
`type` | no | string, number, object | react element to be wrapped by this option (default: Button)

### html-label

HTML element label with customizable class name, icon, text, appearance, and interaction handlers.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`children` | no | object |  React element or elements<br /><br />one of type: arrayOf(PropTypes.node), node
`className` | no | string, object | one of type: string, object, array
`clickHandler` | no | object | function with following signature: function({ value })
`hoverHandler` | no | object | function with following signature: function({ value })
`htmlFor` | no | string | ID of a labelable form-related element
`icon` | no |string | path to image to render within label tag
`text` | no | string | text to render within label tag
`theme` | no | string | color scheme of component; see html-label.css

### MultiSelect and SingleSelect

Select boxes built on top of [IHME-React-Select](https://github.com/ihmeuw/ihme-react-select). At minimum, the following props should be declared.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`labelKey` | yes | string | key on option objects holding label (e.g., `location_name`)
`valueKey` | yes | string | key on option objects holding value (e.g., `location_id`)
`onChange` | yes | func | function to be executed on change in value
`options` | yes | array | array of option objects
`value` | yes | array or object | list of options or single option currently selected
`hierarchical` | no | boolean | whether or not to display options hierarchically; if `true`, option objects need a `level` key

#### Example

```jsx
import { SingleSelect, MultiSelect } from 'ihme-ui/ui';

<SingleSelect
    labelKey="name"
    valueKey="name"
    onChange={ function (selection <Object>) {...} }
    options={ [{location_name: 'Albany', location_id: 1 }, ...] }
    value={{ location_name: 'Denver', location_id: 2 }}
/>

<MultiSelect
    labelKey="name"
    valueKey="name"
    onChange={ function (selections <Array>) {...} }
    options={ [{location_name: 'Albany', location_id: 1 }, ...] }
    value={[{ location_name: 'Denver', location_id: 2 }, ...]}
/>
```


### responsive-container

Responsive HTML container with customizable resize callback function and responsiveness to height and width. A simple wrapper for [react-virtualized](https://github.com/bvaughn/react-virtualized).

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`children` | yes | object | React element or elements<br /><br />one of type: arrayOf(PropTypes.node), node
`disableHeight` | no | boolean | boolean value to disable dynamic :height property
`disableWidth` | no | boolean | boolean value to disable dynamic :width property
`onResize` | no | object | Callback function to be invoked on resize ({height, width})

### shape

Selection of useful shapes and data displays, suitable for use within an ihme-ui chart.

#### area

Area element with customizable appearance, data, data accessors, and interaction handlers.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`clickHandler` | no | object | (default: noop)
`color` | no | string | (default: steelblue)
`data` | yes | object | array of objects, e.g. [ {}, {}, {} ]
`dataAccessors` | yes | object | (default: { x: 'x', y0: 'y0', y1: 'y1' })
`hoverHandler` | no | object | (default: noop)
`scales` | yes | object | [scales from d3Scale](https://github.com/d3/d3/wiki/Quantitative-Scales)
`strokeWidth` | no | string | (default: 2.5)

#### line

Line element with customizable appearance, data, data accessors, and interaction handlers.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`clickHandler` | no | object | (default: noop)
`data` | yes | object | array of objects e.g. [ {}, {}, {} ]
`dataAccessors` | yes | object | (default: { x: 'x', y: 'y' })
`fill` | no | string | (default: none)
`hoverHandler` | no | object | (default: noop)
`scales` |yes | object | [scales from d3Scale](https://github.com/d3/d3/wiki/Quantitative-Scales)
`stroke` | no | string | (default: steelblue)
`strokeWidth` | no | string | (default: 2.5)

#### multi-line

Multi-line element with customizable appearance, data, data accessors, and interaction handlers.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`clickHandler` | no | object |
`colorScale` | no | object | function that accepts keyfield, and returns stroke color for line
`data` | no | object | array of objects e.g. [ {location: 'USA',values: []}, {location: 'Canada', values: []}
`dataAccessors` | yes | object | key names containing x, y data<br />x -> accessor for xscale<br />y -> accessor for yscale (when there's one, e.g. <Line />)<br />y0 -> accessor for yscale (when there're two; e.g., lower bound)<br />y1 -> accessor for yscale (when there're two; e.g., upper bound)
`dataField` | no | string | key that holds values to be represented by individual lines
`hoverHandler` | no | object |
`keyField` | no | string | key that uniquely identifies dataset within array of datasets
`scales` | no | object | [scales from d3Scale](https://github.com/d3/d3/wiki/Quantitative-Scales)
`showLine` | no | boolean | whether or not to draw lines (e.g., mean estimate lines)
`showUncertainty` | no | boolean | whether or not to draw uncertainty areas for lines

#### scatter

Scatterplot element with customizable appearance, data, data accessors, and interaction handlers.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`onClick` | no | object | partially applied function that takes in datum and returns function
`color` | no | string | (default: steelblue)
`colorScale` | no | object | function that accepts keyfield, and returns color for each symbol, overrides color above
`data` | yes | object | array of objects e.g. [ {}, {}, {} ]
`dataAccessors` | yes | object | key names containing x, y data
`onHover` | no | object | partially applied function that takes in datum and returns function
`scales` | yes | object | [scales from d3Scale](https://github.com/d3/d3/wiki/Quantitative-Scales)
`size` | no | number |
`symbolType` | no | string | key name for value of symbol (default: circle)

#### multi-scatter

Scatterplot element with customizable appearance, data, data accessors, and interaction handlers.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`colorScale` | no | object | function that accepts keyfield, and returns stroke color for line
`data` | no | object | array of objects e.g. [ {location: 'USA',values: []}, {location: 'Canada', values: []}
`dataAccessors` | yes | object | key names containing x, y data
`dataField` | no | string | key name for values representing individual lines
`keyField` | no | string | key name for topic of data
`onClick` | no | object | partially applied function that takes in datum and returns function
`onHover` | no | object | partially applied function that takes in datum and returns function
`scales` | yes | object | [scales from d3Scale](https://github.com/d3/d3/wiki/Quantitative-Scales)
`size` | no | number |
`symbolField` | no | string | key name for value of symbol
`symbolScale` | no | object | function to transform symbol value to a shape

#### symbol

Symbol element with customizable appearance, data, and interaction handlers.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`clickHandler` | no | object | partially applied fn that takes in datum and returns fn (default: noop)
`color` | no | string | (default:steelblue)
`data` | no | object | Datum for the click and hover handlers.
`hoverHandler` | no | object | partially applied fn that takes in datum and returns fn (default: noop)
`position` | no | object | (default: x: 0, y: 0)
`size` | no | number | area in square pixels (default: 64)
`strokeWidth` | no | number | (default: 1)
`type` | no | object | will match a [SYMBOL_TYPE](https://github.com/d3/d3/wiki/SVG-Shapes#symbol_type) (default: circle)<br /><br />one of: 'circle', 'square', 'triangle', 'cross', 'diamond', 'star', 'wye'

### slider

Single- or multi-input-value selector on a track with customizable appearance and interaction handlers.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`fill` | no | bool | boolean value to include fill in the track to indicate value (default: false)
`fillColor` | no | string | style for the fill color (default: '#ccc')
`height` | no | number | height of element in pixels (default: 24)
`labelFunc` | no | object | function applied to the selected value prior to rendering.<br /><br />Parameters: value - selected value<br />returns: 'string'<br />default: \_.identity
`onChange` | yes | object | callback function when value is changed.<br /><br />Parameters:<br />value: object with keys ['min'] and 'max'<br />key: key of most recent value change
`minValue` | yes | number | minimum slider value
`maxValue` | yes | number | maximum slider value
`step` | no | number | step between slider values (default: 1)
`value` | yes | number, object | initial selected value. If number, a single slider handle will be rendered. If object with keys 'min' and 'max', two slider handles will be rendered.<br /><br />one of type: number, array, shape
`width` | no | number | width of element in pixels (default: 200)

### spinner

Animated indicator (e.g., for loading) with customizable size.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`className` | no | string, object | one of type: string, object, array
`inline` | no | bool | display spinner inline with other elements (e.g., in a button)
`size` | no | string | one of: 'small', 'medium', 'large'

### svg-text

SVG element label with customizable anchor, position, and value.

Property | Required | Type(s) | Description
        --- | :---: | :---: | ---
`anchor` | yes | string | one of: 'start', 'middle', 'end']
`dx` | no | number |
`dy` | no | number |
`fill` | no | string | (default: black)
`value` | no | string, number | one of type: string, number
`x` | yes | number |
`y` | no | number |

---

## Test Utilities

### Data Generator

Data Generator creates fake data for testing purposes.

#### API Description

Data Generator takes an object with four properties.

`primaryKeys` is an array of objects that have a `name` property that is a string, and a `values` property that is an array. The data generator will create unique composite keys based on the values arrays.

`valueKeys` is an array of objects that have a `name` property that is a string, a `range` property that is an array of two numbers, and an `uncertainty` property that is a boolean. Value keys are iterated so that their values are within the range specified. If `uncertainty` is true, data generator will produce additional keys of the form `(name)_ub` and `(name)_lb` to represent upper and lower bound uncertainties.

`year` is a number that represents a starting year for a series of years iterated by length. The output key is `year_id`.

`length` is a number for which each unique composite key gets a new value key. If there are many composite keys, each key receives `length` number of data points.
```javascript
const config = {
  primaryKeys: [
    {name: 'A', values: [1, 2]},
    {name: 'B', values: [1, 2, 3]}
  ],
  valueKeys: [
    {name: 'value', range: [100, 200], uncertainty: false}
  ],
  year: 2000,
  length: 2
}
//outputs
[
  {A: 1, B: 1, value: v_1, year_id: 2000},
  {A: 1, B: 1, value: v_2, year_id: 2001},
  {A: 1, B: 2, value: v_1, year_id: 2000},
  {A: 1, B: 2, value: v_2, year_id: 2001},
  {A: 1, B: 3, value: v_1, year_id: 2000},
  {A: 1, B: 3, value: v_2, year_id: 2001},
  {A: 2, B: 1, value: v_1, year_id: 2000},
  {A: 2, B: 1, value: v_2, year_id: 2001},
  {A: 2, B: 2, value: v_1, year_id: 2000},
  {A: 2, B: 2, value: v_2, year_id: 2001},
  {A: 2, B: 3, value: v_1, year_id: 2000},
  {A: 2, B: 3, value: v_2, year_id: 2001}
]
```

Data generator also outputs a unique `id` key for each row of data.

#### Example

```javascript
const config = {
  primaryKeys: [
    {name: 'key_1', values: ['v_11', 'v_21', ..., 'v_m1']},
    {name: 'key_2', values: ['v_12', 'v_22', ..., 'v_m2']},
    ...
    {name: 'key_n', values: ['v_1n', 'v_2n', ..., 'v_mn']}
  ],
  valueKeys: [
    {name: 'value_1', range: [lower_1, upper_1], uncertainty: true},
    {name: 'value_2', range: [lower_2, upper_2], uncertainty: false},
    ...
    {name: 'value_k', range: [lower_k, upper_k], uncertainty: false}
  ],
  year: 2000,
  length: 10
}
dataGenerator(config);
```

## Code Quality
- eslint enforces AirBnB rules: https://github.com/airbnb/javascript
