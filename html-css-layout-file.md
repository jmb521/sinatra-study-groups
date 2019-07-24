# Sinatra 2. HTML & CSS in Sinatra (How to Use the Layout File)
**Title**: HTML & CSS in Sinatra (How to Use the Layout File)
**Description**: Come and learn how to use the layout file in Sinatra, we go over HTML and CSS concepts along the way.

## Table of Contents
1. Layout File & era
2. HTML
3. CSS

## BONUS
- Explain how a hard-refresh works `cmd + shift+ r`

## Layout File & erb
### erb Syntax
```
<% @im_hidden %>
<%= @im_visible %>
```

### yield
`<%= yield %>`

### Using Fonts
`<link href=“https://fonts.googleapis.com/css?family=Josefin+Sans|Press+Start+2P&display=swap” rel=“stylesheet”>`


## HTML
### HTML Fundamentals
- Tags: img, input, label, p, div

### Dev Tools
- Inspect

### Accessibility
- Semantic elements


## CSS
### CSS Fundamentals
[image:E2B04992-68DF-45D4-803E-C9C1FF6CA89E-13846-0000182405137FA2/css-syntax.png]
- ID vs Class Selectors

### Media Queries
- Min and Max Width
	- `@media only screen and (max-width: 600px)  {…}`
	- ^ says if [device width] is less than or equal to 600px
	- `@media only screen and (min-width: 600px)  {…}`
	- ^ says if [device width] is greater than or equal to 600px

### CSS Grid & Flexbox

### Accessibility
- `:focus`

