### UI Field Types

#### Properties are supported by all field types

| property | var type | example | description |
|---------:|:--------:|:-------:|:------------|
| id | string | “theName” | the identifier of the field. This must be unique |
| type | string | “text” | type of field |
| title | string | “Enter name” | the text shown in the user interface left to the input field |
| defaultValue | string | “John Doe”, "#9B9B9B" | the value assigned to a field when a new instance of a widget is created |
| disabled | boolean | “true”, “false” | fields can be disabled by default. Set this to true to disable the field |
| hidden   | boolean | “true”, “false” | fields can be hidden in the user interface. Set this to true to hide the field |

#### Field types and their specific properties

| field type | properties | var type | example | description |
|-----------:|:----------:|:--------:|:-------:|:------------|
| label | [default properties] |  | read only html text |
| text | [default properties] |  | single line text input field |
| textarea | [default properties] |  | multi line text input field |
| | • rows | integer | “5” | number of rows |
| | • cols | integer | “15” | number of columns |
| font | [default properties]			font selector including font style
	hideUI
•	style
•	bold
•	italic
•	underline
•	alignment	
boolean boolean
boolean
boolean
boolean	
“true”, “false”
“true”, “false”
“true”, “false”
“true”, “false”
“true”, “false”	
hide all style options
hide bold option
hide italic option
hide unterline option
hide alignment option
| json | [default properties]			JSON input field with syntax highlighting
	•	width
•	height	integer
integer	“300”
“200”	width in pixel
height in pixel
| number | [default properties]			
	•	min
•	max
•	step

•	unit

•	format	double
double
double

string

string	“0.0”
“83.43”
“0.1”

“%”, “px”

“0.01”	minimum value allowed
maximum value allowed
step for value changes when using up and down arrows
show a unit string in the input field next to the number
number format, defines how many digits are shown
| color | [default properties]			color selector
| gradient | [default properties]			gradient selector to choose between color, linear od radial gradient
| image | [default properties]			image selector
| checkbox | [default properties]			on / off selector
| selection | [default properties]			drop down list of string values
	selections
•	id
•	title	array
string
string	
“default”
“Default Text”	array with strings the user can select
option id
option title
| button | [default properties]			push button
| composition | [default properties]			select a composition instance
				
