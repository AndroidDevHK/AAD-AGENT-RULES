# Rule 2: Dialog Handling Rules

When generating or implementing dialogs in Android, you MUST strictly adhere to the following rules to ensure consistency, reusability, and proper UI scaling.

## 1. Separate Class and Layout
Every new dialog must be completely decoupled from the Activity or Fragment that calls it.
- **Separate Class**: Create a dedicated Kotlin/Java class for each dialog. Do not handle dialog UI logic directly inside an Activity or Fragment.
- **Separate Layout**: Create a dedicated XML layout file (e.g., `dialog_custom_name.xml`) specifically for the dialog. Do not reuse existing layouts unless specifically designed as a shared dialog layout.

## 2. Use `Dialog` Object
- You must use the base `android.app.Dialog` class to create and handle the dialog.
- **Do NOT use** `AlertDialog.Builder` or other builder patterns for custom dialogs, as they restrict layout flexibility and custom behavior. 

## 3. Specific Sizing and Margins
All dialogs must adhere to a strict width and margin policy to ensure they look consistent across different screen sizes.
- **Width**: The dialog window width must be set to `match_parent`.
- **Horizontal Margin**: The dialog must have exactly `20dp` of horizontal margin (left and right) from the edges of the screen.

## 4. View Binding
- You must use **View Binding** to inflate the layout and interact with its views.
- Avoid using `findViewById` entirely.

### Example Implementation Guide:
To achieve the `match_parent` width, `20dp` margins, and use View Binding with the `Dialog` object:

```kotlin
val dialog = Dialog(context)
dialog.requestWindowFeature(Window.FEATURE_NO_TITLE)

// Inflate layout using View Binding
val binding = DialogYourCustomLayoutBinding.inflate(LayoutInflater.from(context))
dialog.setContentView(binding.root)

// Ensure background is transparent to allow margins to show
dialog.window?.setBackgroundDrawableResource(android.R.color.transparent)

// Set width to match_parent and apply 20dp margin
val window = dialog.window
if (window != null) {
    val layoutParams = WindowManager.LayoutParams()
    layoutParams.copyFrom(window.attributes)
    layoutParams.width = WindowManager.LayoutParams.MATCH_PARENT
    layoutParams.height = WindowManager.LayoutParams.WRAP_CONTENT
    window.attributes = layoutParams
    
    // Apply 20dp padding/margin on the root view of your dialog_your_custom_layout.xml
    // OR set inset drawable as background.
}

// Access views via binding
// binding.titleTextView.text = "Hello!"
// binding.confirmButton.setOnClickListener { dialog.dismiss() }

dialog.show()
```
*(Note: To perfectly implement the 20dp margin, the root view of the dialog's XML layout should handle the `20dp` margin/padding, or an inset drawable should be applied to the window background.)*
