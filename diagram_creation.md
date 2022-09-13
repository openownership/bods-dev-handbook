# Creating SVG diagrams

BODS diagrams are created in Scalable Vector Graphic (SVG) format for ease of scaling and translation. SVGs use XML syntax. Text can therefore be stripped out and translated using standard tools. The following workflow guidance is provided so that diagrams within the BODS documentation can accommodate translated text.

## Suggested diagram creation workflow

- Use Google Draw to do a 1st draft of a diagram BUT do not include any text.

  This is recommended since Google Draw allows for easy layout, styling and connection of diagram elements. Examples of Google Draw versions of diagrams can be [seen here](https://drive.google.com/drive/folders/1R0r-Dx-PivOYmUPbE7MtKbHm-nrFAikB), though note that they have text in them.
  
- Export the diagram as an SVG file using File > Download.

- Open the SVG locally in [Inkscape >1.0](https://inkscape.org/).

  Since verion 1, Inkscape has [better SVG 2 support and text-handling](https://wiki.inkscape.org/wiki/index.php?title=Release_notes/1.0#Browser-compatible_flowed_text). 

- Go to Edit > Preferences > Text and ensure that 'Use SVG2 auto-flowed text' is checked.

  The [SVG 2 specification](https://www.w3.org/TR/2018/CR-SVG2-20181004/) contains support for text-wrapping, and Inkscape produces good SVG 2 output. However browsers still do not implement SVG 2 fully. So the guidance below contains workarounds.

- Use the 'Create and edit text objects' tool to click and add text to the diagram. (Do not click and drag to create a text area. If text needs to span multiple lines, use the Enter key to add line breaks manually.) 
  
- Make sure that the 'Text alignment' setting for the string is correctly set to left, centre, or right depending on which edge of the text should remain 'fixed' when the text is replaced by a (longer) translated string. 

  Looking at [this diagram](https://standard.openownership.org/es/0.3.0/schema/guidance/repr-beneficial-ownership.html#overview) in Spanish, the line labels should have been left aligned.

- Place the text and adjust diagram elements so that there is space for the text to be replaced by a longer, translated string.

  Looking at [this diagram](https://standard.openownership.org/es/0.3.0/schema/guidance/repr-state-owned-enterprises.html#scenario-4) in Spanish, a string has crept outside the middle grey statement box. Extra space should have been created in the grey box to accommodate longer strings.

- Save your edits and open the file in a browser (or two) to see how the layout looks.

  There appears to be a bug around Inkscape's aligment and SVG output. This can mean that the text shows up in odd places. Moving the text element in Inkscape away and then back to its original position, then re-saving, can correct things.
  
 - If you want to see how well your diagram will do at accommodating longer strings, open the SVG file in a text editor. Edit strings within the \<text\> elements, save and view in the browser of your choice.
