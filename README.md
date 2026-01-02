# Extended Inputs

**More input fieldviews for Saltcorn**

## Summary

**What it adds:** Two enhanced slider FieldViews (`enhanced_slider_integer` and `enhanced_slider_float`) that combine a range slider with a numeric input field.

**Primary Use Case:** Provides a dual-input control for numeric fields, allowing users to either drag a slider or manually type a value, with optional prefix/postfix labels (e.g., currency symbols, units, percentages).


## Plugin Configuration

This plugin has **no global configuration settings**. All configuration is done at the field level when you add the FieldView to a specific field in your table.


## How to Use

### Step 1: Create or Edit a Table Field

1. Navigate to **Table → [Your Table]**. 
2. Add a new field or edit an existing field with type **Integer** or **Float**. 

### Step 2: Assign the FieldView

1. Open or create an **Edit** view.
2. In the field configuration, locate the **Field View** dropdown.
3. Select one of: 
   - **`enhanced_slider_integer`** (for Integer fields)
   - **`enhanced_slider_float`** (for Float fields)

### Step 3: Configure the Enhanced Slider

After selecting the FieldView, you'll see additional configuration options:

| Setting Name | Data Type | Required | Description |
|--------------|-----------|----------|-------------|
| **Min** | Integer/Float | Yes (if not set at field level) | Minimum value for the slider and input |
| **Max** | Integer/Float | Yes (if not set at field level) | Maximum value for the slider and input |
| **Entry width (px)** | Integer | No | Width of the numeric input box in pixels (default is browser default) |
| **Prefix** | String | No | Text displayed before values (e.g., `$`, `€`) |
| **Postfix** | String | No | Text displayed after values (e.g., `%`, `kg`, `m²`) |

**Important Notes:**
- If your field already has `min` and `max` attributes defined at the field level, those will be used automatically.
- If `min` and `max` are **not** defined at the field level, you **must** configure them in the FieldView settings or the slider will not render correctly. 

### Step 4: Use in Forms and Edit Views

The control displays: 
- **Left label:** Prefix + Minimum value + Postfix
- **Slider:** Interactive range input
- **Right label:** Prefix + Maximum value + Postfix
- **Numeric input:** Manual entry field with prefix/postfix


## Technical Constraints & Hidden Logic

### Synchronization Behavior
- When the **slider** is moved, the **numeric input** updates in real-time. 
- When the **numeric input** is changed, the **slider** position updates immediately.
- The `onchange` event fires only when the slider movement is complete (not during dragging).

### Hardcoded Step Value
- The numeric input uses `step:  "1"` for both Integer and Float variants.
- This means Float fields may not allow fractional input increments via keyboard arrows (though manual decimal entry is allowed).

### JavaScript Dependencies
- The plugin loads `custom.js` which relies on **jQuery** (`$` function).
- The synchronization functions (`enhsli_range` and `enhsli_number`) use jQuery DOM traversal (`.next()`, `.prev()`).

### Localization
- Min/max labels use `toLocaleString()` for number formatting (e.g., `1,000` vs `1000` depending on locale).
- Prefix/postfix are plain text and not localized.

### Custom Event Handling
- If the field has an `onChange` attribute, it will be **appended** to the built-in synchronization logic (not replaced).


## Example Use Cases

### Currency Input
- **Field Type:** Float
- **FieldView:** `enhanced_slider_float`
- **Config:**
  - Min: `0`
  - Max: `10000`
  - Prefix: `$`
  - Entry width: `100`

### Percentage Slider
- **Field Type:** Integer
- **FieldView:** `enhanced_slider_integer`
- **Config:**
  - Min:  `0`
  - Max: `100`
  - Postfix: `%`
  - Entry width: `60`

### Weight Input
- **Field Type:** Float
- **FieldView:** `enhanced_slider_float`
- **Config:**
  - Min: `0`
  - Max: `500`
  - Postfix: `kg`
  - Entry width: `80`


## License
[MIT](./LICENSE)
