# Rule 4: UI Components and Design Catalog

When building the UI layer based on a specific design system, you MUST ensure that all components correctly implement the Material 3 XML themes and that they can be easily previewed and tested in both Light and Dark modes.

## 1. Design System Catalog Screen
Before or alongside building feature screens, you must create a "Design Catalog" screen (e.g., `DesignSystemActivity` or `DesignSystemFragment`). 
- **Purpose**: This screen acts as a gallery to showcase all the custom UI components defined by the design system in one scrollable view.
- **Theme Switcher**: This screen MUST contain a `Switch` or `Button` at the top to toggle between Light and Dark themes dynamically at runtime (using `AppCompatDelegate.setDefaultNightMode()`).

## 2. Using Customized UI Components
Always use the `com.google.android.material.*` views. Do not use legacy standard Android views. These Material views automatically adapt to the `themes.xml` (colors, typography, and shapes) you defined in Rule 3.

### Cards (`MaterialCardView`)
Cards must use `MaterialCardView` to properly apply corner rounding, elevation, and stroke colors from the theme.
```xml
<com.google.android.material.card.MaterialCardView
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    app:cardElevation="2dp"
    app:cardCornerRadius="?attr/shapeAppearanceMediumComponent"
    app:strokeColor="?attr/colorOutline"
    app:cardBackgroundColor="?attr/colorSurface">
    
    <!-- Card Content Here -->

</com.google.android.material.card.MaterialCardView>
```

### Switches (`SwitchMaterial`)
Always use `SwitchMaterial` for toggles. It automatically tints itself using `?attr/colorPrimary` and `?attr/colorSurface`.
```xml
<com.google.android.material.switchmaterial.SwitchMaterial
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Toggle Setting"
    android:textAppearance="?attr/textAppearanceBodyLarge"
    android:textColor="?attr/colorOnSurface" />
```

### Text Inputs (`TextInputLayout` + `TextInputEditText`)
For user input (EditTexts), always wrap `TextInputEditText` inside a `TextInputLayout`. This allows for Outlined or Filled styles that adapt to the Material 3 design system.
```xml
<!-- Outlined Style Text Input -->
<com.google.android.material.textfield.TextInputLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    style="@style/Widget.Material3.TextInputLayout.OutlinedBox"
    android:hint="Enter your name">

    <com.google.android.material.textfield.TextInputEditText
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textColor="?attr/colorOnSurface" />

</com.google.android.material.textfield.TextInputLayout>
```

### Buttons (`MaterialButton`)
Use `MaterialButton`. They adapt to `?attr/colorPrimary` by default. Use styles for Outlined or Text buttons.
```xml
<!-- Filled Button -->
<com.google.android.material.button.MaterialButton
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:text="Primary Action" />

<!-- Outlined Button -->
<com.google.android.material.button.MaterialButton
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    style="@style/Widget.Material3.Button.OutlinedButton"
    android:text="Secondary Action" />
```

## 3. Strict Adaptation Rule
- **No hardcoded customizations**: If a Card needs a red background, you do NOT hardcode `#FF0000`. You update the design system's `colors.xml` and `themes.xml` to define an `error` or `customCard` semantic color, and reference it via `?attr/...`. 
- **Testing**: Before finalizing UI code, the agent must ensure that switching the app to Dark Mode via the catalog's theme switcher seamlessly flips the colors of Cards, Switches, EditTexts, and Buttons without any unreadable text or invisible borders.
