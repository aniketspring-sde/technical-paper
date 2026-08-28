
#### HTML (HyperText Markup Language) is used to define the structure and content of a web page. It provides elements such as headings, paragraphs, links, images, forms, tables, and sections.

#### CSS (Cascading Style Sheets) is used to control the presentation and layout of HTML elements. It defines properties such as colors, fonts, spacing, positioning, alignment, responsiveness, and animations.

## Box Model
- The CSS box model is a container that used to structure the elements in a webpage so the element can be displayed visually good. It consists of four essential components content, padding, border, and margin, as shown in the following diagram.
   - Content: This is the innermost part of the box and refers to the actual content of an element, such as text, images, or other media. You can set its size using the properties such as inline size and block-size, also known as width and height.
   - Padding: Represents the space between the content and the element's border. It can be applied separately to each side of the element (top, right, bottom, and left). The size of this box is set using padding and other related properties.
   - Border: Defines a line or boundary around the padding and content of an element. The size, style and color of this box is set using border and other related properties.
   - Margin: Represents the space outside the border of an element. Like padding, margins can also be set separately for each side and are typically used to create space between elements on a webpage. The size of this box is set using margin and other related properties.

     <img width="642" height="302" alt="image" src="https://github.com/user-attachments/assets/e4c389cd-dcc8-4c29-b717-6d27e1af250a" />

## Inline versus Block Elements.
- Block Elements
A block element normally starts on a new line and occupies the available horizontal space.
  - example: div, p, h1, section
  - Characteristics:

      - Starts on a new line.
      - Normally takes the available width.
      - width and height can be applied.
      - Margin and padding affect surrounding layout.
- Inline Elements
Inline elements normally remain within the same line as surrounding content.
 - example: span, a
 - Characteristics:

      - Does not normally start a new line.
      - width and height do not behave like they do on block boxes.
      - Horizontal margin and padding affect surrounding inline content.
## Positioning: Relative/Absolute
- position: relative keeps the element in the normal document layout flow. Adjusting its coordinates shifts it relative to its own original position, leaving an empty placeholder gap where it used to be.
- position: absolute rips the element completely out of the normal layout flow. Other elements behave as if it does not exist. It anchors itself relative to its closest parent container that has a defined position.

## Common CSS structural classes
- Structural classes are used to organize the layout of a webpage.
  
| Class        | Purpose                 |
| ------------ | ----------------------- |
| `.container` | Main content wrapper    |
| `.header`    | Header section          |
| `.navbar`    | Navigation area         |
| `.main`      | Main content            |
| `.content`   | Primary content         |
| `.sidebar`   | Secondary content       |
| `.section`   | Logical content section |
| `.footer`    | Footer                  |
| `.row`       | Horizontal layout       |
| `.column`    | Vertical/content column |

## Common CSS syling classes

## CSS Specificity
- CSS specificity is an algorithm that determines which style declaration is ultimately applied to an element.
If two or more CSS rules point to the same element, the declaration with the highest specificity will "win", and that style will be applied to the HTML element.
 - Specificity Hierarchy
   1. Inline styles
      
   2. ID selectors  
      
   3. Class/attribute / pseudo-class selectors         
         
   4. Element/ pseudo-element selectors
## CSS Responsive Queries
- Media queries in CSS are used to apply different CSS styles based on the screen size, resolution, and other characteristics of the user device. Media queries uses @media rule to include a extra block of CSS properties when a certain conditions are met. Media queries can also be used to style printable version of page separately.
   - Syntax      
@media not|only mediatype and (media feature) and (media feature) {     
    CSS-Code;    
- Here, media-type can be things like screen, print, speech, etc., and media-feature can be characteristics such as width, height, aspect ratio, orientation, and more.

## Flexbox
- Flexbox is a layout model for arranging items (horizontally or vertically) within a container, in a flexible and responsive way.
- CSS Flexbox is used for a one-dimensional layout, with rows OR columns.
- A flexbox always consists of:
   - A Flex Container - The parent (container) element, where the display property is set to flex or inline-flex
   - One or more Flex Items - The direct children of the flex container automatically becomes flex items
  #### CSS Flex Container Properties
      
      The flex container element can have the following properties:
      
          display - Must be set to flex or inline-flex
          flex-direction - Sets the display-direction of flex items
          flex-wrap - Specifies whether the flex items should wrap or not
          flex-flow - Shorthand property for flex-direction and flex-wrap
          justify-content - Aligns the flex items when they do not use all available space on the main-axis (horizontally)
          align-items - Aligns the flex items when they do not use all available space on the cross-axis (vertically)
          align-content - Aligns the flex lines when there is extra space in the cross axis and flex items wrap
   
  #### CSS flex-direction Property

      The flex-direction property specifies the display-direction of flex items in the flex container.
      
      This property can have one of the following values:
      
          row (default)
          column
          row-reverse
          column-reverse
  #### CSS flex-wrap Property

      The flex-wrap property specifies whether the flex items should wrap or not, if there is not enough room for them on one flex line.
      
      This property can have one of the following values:
      
          nowrap (default)
          wrap
          wrap-reverse
  #### CSS justify-content Property

      The justify-content property aligns the flex items along the main-axis (horizontally).
      
      This property can have one of the following values:
      
          center
          flex-start (default)
          flex-end
          space-around
          space-between
          space-evenly
  #### CSS align-items Property

      The align-items property aligns the flex items vertically (on the cross-axis).
      
      This property can have one of the following values:
      
          normal (default)
          stretch
          center
          flex-start
          flex-end
          baseline






## Common header meta tags
- The <meta> tag defines metadata about an HTML document. Metadata is data (information) about data.
- <meta> tags always go inside the <head> element, and are typically used to specify character set, page description, keywords, author of the document, and viewport settings.
- Metadata will not be displayed on the page, but is machine parsable.
- Metadata is used by browsers (how to display content or reload page), search engines (keywords), and other web services.
   - meta tags:
      - `<meta name="description" content="A description of the page">`
      - Use this tag to provide a short description of the page. In some situations, this description is used in the snippet shown in search results
      - `<meta name="viewport" content="...">`
      - This tag tells the browser how to render a page on a mobile device. Presence of this tag indicates to Google that the page is mobile friendly. Read more about how to configure the viewport meta tag.
      - `<meta name="rating" content="adult">, <meta name="rating" content="RTA-5042-1996-1400-1577-RTA">`
      - Labels a page as containing sexually-explicit adult content, to signal that it be filtered by SafeSearch results. Learn more about labeling SafeSearch pages.

      
### References:
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position
- https://www.w3schools.com/css/css_specificity.asp
- https://www.tutorialspoint.com/css/css_media_queries.html
- https://developers.google.com/search/docs/crawling-indexing/special-tags
