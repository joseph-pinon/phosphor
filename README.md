<p align="center">
  <h1 align="center">Phosphor</h1>
</p>

<p align="center">
	Not just another J28.2 Formatter 
</p>

## Features
- Quickly generate messages into continuous line format for target platform.
- Automatic error and split line detection.
- Visualize exactly how your message will display in the cockpit - harvestable coords displayed.
- Configure and reuse your own message specifications.
- Each tab retains unique settings - name each tab for streamlined battle tracking.
- Choose how lines are prefixed and combined.
- Character count, and message count inform probability of message intercept.
- Lightweight, runs on any browser.

## How to Use
1. Open the phosphor.html in the web browser of your choice.
2. Double click tab to rename.
3. Setup:
   1. The form type changes the number of data entry regions and descriptions.
   2. Line combination changes the behavior of combining data regions.
   3. Platform informs character per line, line per page, coord harvestability rules and line break mechanics.
   4. Passage prefix controls the numbering used for each data region.

## Config
The actual platform restrictions and formats of standard messages are CUI or Secret and will not be maintained on this page. However, users on restricted networks can maintain their own repository of "form" types and platform capes/lims by directly altering the [JSON](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Scripting/JSON) fields in the html file.

Open "index.hmtl" in a text editor of your choice.

### Creating Forms
---
Search for "FORM_DATA"
```js
    const FORM_DATA = [
      {
        label: "Marshall",
        passages: [
          {label: "Name and ATO Day", type: "text"},
          {
            label: "Mission Status",
            type: "select",
            options: [
              {label: "Mission Successful", text: "Succ"},
              {label: "Mission Failure", text: "Fail"}
            ]
          },
          {label: "Tanker Status", type: "text"},
          {label: "Friendly Aircraft", type: "text"},
          {label: "Munitions Expended", type: "text"},
          {label: "Timing Targets", type: "text"},
          {label: "Test", type: "text"},
          {label: "Admin/Remarks", type: "text"}
        ]
      },
      {
        label: "DCA",
        passages: [
          {label: "Lorem ipsum dolor si", type: "text"},
          {label: "Lorem ipsum dolor si", type: "text"},
          {label: "Lorem ipsum dolor si", type: "text"},
          {label: "Lorem ipsum dolor si", type: "text"}
        ]
      }
    ];
```
- **label**: How the form type will display in the setup panel.
- **passages**: A list of all of the data forms "passages".
  - **label**: A description of what data the user should input into this passage.
  - **type**: The two options are "text" (Allow the user to type data freely) and "select" (Restrict the user to a set of prefragged options).
  - **options**: If the "select" type is chosen, supply a list of options.
    - **label**: The name of the option in the dropdown menu.
    - **text**: The text that will be formatted to the output message.


### Creating Platforms
---
Search for "PLATFORM_DATA". Below are the default "random" settings.
```js
    const PLATFORM_DATA = [
      {
        label: "F-16",
        charsPerLine: 40,
        screenLines: 12,
        supportsDoubleSlash: true,
        harvestableCoordinatePattern: /\d{2}[A-Z] [A-Z]{2}\d \d{3} \d{3} \d{3}/g
      },
      {
        label: "F-35",
        charsPerLine: 32,
        screenLines: 6,
        supportsDoubleSlash: false,
        harvestableCoordinatePattern: /\d{2}[A-Z] [A-Z]{2} \d{5} \d{5}/g
      },
      {
        label: "F-15",
        charsPerLine: 24,
        screenLines: 10,
        supportsDoubleSlash: true,
        harvestableCoordinatePattern: /\d{2}[A-Z] [A-Z]{2} \d{5} \d{5}/g
      },
      {
        label: "A-10",
        charsPerLine: 16,
        screenLines: 5,
        supportsDoubleSlash: true,
        harvestableCoordinatePattern: /\d{2}[A-Z] [A-Z]{2}\d \d{3} \d{3} \d{3}/g
      }
    ];
```
- **label**: Controls how the platform displays in the dropdown.
- **charsPerLine**: The number of characters the display in the cockpit can render on a single line.
- **screenLines**: The number of lines the display can render before the pilot has to scroll.
- **supportsDoubleSlash**: If the platform properly interprets "//" as a line break.
- **harvestableCoordinatePattern**: A [regex](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions/Cheatsheet) expression to determine whether patterns of coordinates will appear as "Harvestable".




