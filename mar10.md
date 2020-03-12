# Grid & Flexbox

Grid elements only apply to the first child; you cannot use it for a bunch of nested elements and you cannot use it on itself.

To turn grid on: `display: grid`.

Grid *can* be displayed as rows, but we typically want to use columns.

Padding: how do I move the space between the content and the border (which is sometimes invisible); how is my content inside of the box?
- If I set my content within a container of a defined 500px, padding is setting how it will be placed within that space.
- A line of text may only take up 10px, so you may want to set where it will
- be within that 500px container.

Margin: how much does the element push the things around it

## When to Use Grid Over Flexbox 

Grid is generally for 2D layouts. You *can* do that with flexbox, but grid gives you more control over the specifics of the 2D layout. Everything you do in grid, you can do in flexbox.

## CSS Clean File Tips

CSS variables should go at the top of the file.

Universal element selectors for selecting font family, etc, should go below that.

Remember: Things that come later override whatever was before that. So put all of the generic stuff above.

Try to group things that are related to each other.