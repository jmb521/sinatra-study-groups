#Flexbox


## background
Flexbox was created to provide a better layout and distribute space within a design, without having to know the size beforehand. A flex container expands items to fill available free spaces or shrinks to prevent overflow. 
Flexbox is better intended for small scale layouts, while grid is recommended for larger scale layouts. 

##container (parent)
###
.container {
    display: flex;
}
 or 
 .container {
     display: inline-flex;
 }

 this enables flex for all the children of the container. 

 ### flex-direction
 .container {
     flex-direction: row;
     flex-direction: row-reverse;
     flex-direction: column;
     flex-direction: column-reverse;
 }

 ### flex-wrap
 .container {
     flex-wrap: nowrap; #keeps all flex items on one line
     flex-wrap: wrap; #flex items wrap onto multiple lines
     flex-wrap: wrap-reverse; #goes bottom to top wrapping multiple lines
 }

 ### flex-flow
 .container {
     flex-flow: row nowrap <<--- default value
 }

 is short hand for flex-direction and flex-wrap

 ### justify-content
 .container {
     justify-content: flex-start; <-- default. Items are pushed toward the start line (left side)
     justify-content: flex-end; #items are pushed toward the end line (right side)
     justify-content: center; - items centered along the line
     justify-content: space-between; - items evenly distributed between start and end lines.
     justify-content: space-around; - items evenly distributed in the line with equal space around them. 
 }

 ### align-items 
 .container {
     align-items: stretch; 
     align-items: flex-start;
     align-items: flex-end;
     align-items: center;
     align-items: baseline; - lines content up with where the text falls.

 }

 ### align-content
 .container {
     align-content: flex-start;
     align-content: flex-end;
     align-content: center;
     align-content: space-between;
     align-content: space-around;
     align-content: stretch; -lines stretch to take up remaining space
 }


 ## properties for flex items (children)

 ### order
 by default they are in source order. You can change what order they appear in by specifying an integer value
 .item {
     order: 3; - default value is 0
 }

 ### flex-grow
 this allows an item to grow to fit the space if it needs to. Takes an integer value
 .item {
     flex-grow: 2;
 }

 ### flex-shrink
 allows an item to shrink if necessary
 .item {
     flex-shrink: 3; - default is 1 must be a positive integer. 
 }

 ### flex-basis
 defines the default size of an item before the remaining space is distributed. Can be a length value (5em/px/% or keyword (auto))

 .item {
     flex-basis: 4px;
     flex-basis: auto; (extra space distributed based on flex-grow)
 }

 ### flex 
 shorthand for flex-grow, flex-shrink, and flex-basis
 .item {
     flex: none;
     flex: [0, 1] (flex-grow and flex-shrink)
     flex: auto - flex:basis
 }

 ### align-self 

 allows the default alignment to be overridden for flex items

 .item {
     align-self: auto;
     align-self: flex-start;
     align-self: flex-end;
     align-self: center;
     align-self: baseline; 
     align-self: stretch;
 }