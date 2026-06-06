# Rule 3: Material Design 3 (Material You) XML Theme Rules

When generating UI code, you MUST implement and adhere to **Material Design 3 (M3)** standards using the classic Android XML View system. The app must support both Light and Dark themes natively.

## 1. Complete Theme Configuration
A complete XML design system requires defining core XML resource files:
1. **Colors**: `res/values/colors.xml`
2. **Light Theme**: `res/values/themes.xml`
3. **Dark Theme**: `res/values-night/themes.xml`
4. **Typography**: `res/values/styles.xml` (or defined in `themes.xml`)
5. **Shapes**: `res/values/shape.xml`

## 2. XML Theme Implementation
Whenever generating a new app or feature, you must structure the XML theme as follows:

### Colors (`res/values/colors.xml`)
Define all the core color primitives used across both light and dark themes.
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- Light Primitives -->
    <color name="md_theme_light_primary">#6750A4</color>
    <color name="md_theme_light_onPrimary">#FFFFFF</color>
    <color name="md_theme_light_primaryContainer">#EADDFF</color>
    <color name="md_theme_light_onPrimaryContainer">#21005D</color>
    <color name="md_theme_light_background">#FFFBFE</color>
    <color name="md_theme_light_onBackground">#1C1B1F</color>

    <!-- Dark Primitives -->
    <color name="md_theme_dark_primary">#D0BCFF</color>
    <color name="md_theme_dark_onPrimary">#381E72</color>
    <color name="md_theme_dark_primaryContainer">#4F378B</color>
    <color name="md_theme_dark_onPrimaryContainer">#EADDFF</color>
    <color name="md_theme_dark_background">#1C1B1F</color>
    <color name="md_theme_dark_onBackground">#E6E1E5</color>
</resources>
```

### Light Theme (`res/values/themes.xml`)
Map the Light primitives to the Material 3 theme attributes.
```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme. -->
    <style name="Theme.MyApp" parent="Theme.Material3.Light.NoActionBar">
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/md_theme_light_primary</item>
        <item name="colorOnPrimary">@color/md_theme_light_onPrimary</item>
        <item name="colorPrimaryContainer">@color/md_theme_light_primaryContainer</item>
        <item name="colorOnPrimaryContainer">@color/md_theme_light_onPrimaryContainer</item>
        
        <!-- Background colors -->
        <item name="android:colorBackground">@color/md_theme_light_background</item>
        <item name="colorOnBackground">@color/md_theme_light_onBackground</item>
        <item name="colorSurface">@color/md_theme_light_background</item>
        <item name="colorOnSurface">@color/md_theme_light_onBackground</item>

        <!-- Typography -->
        <item name="textAppearanceTitleLarge">@style/TextAppearance.MyApp.TitleLarge</item>
        
        <!-- Shapes -->
        <item name="shapeAppearanceSmallComponent">@style/ShapeAppearance.MyApp.SmallComponent</item>
    </style>
</resources>
```

### Dark Theme (`res/values-night/themes.xml`)
Map the Dark primitives to the Material 3 theme attributes.
```xml
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- Base application theme for Dark Mode. -->
    <style name="Theme.MyApp" parent="Theme.Material3.Dark.NoActionBar">
        <!-- Primary brand color. -->
        <item name="colorPrimary">@color/md_theme_dark_primary</item>
        <item name="colorOnPrimary">@color/md_theme_dark_onPrimary</item>
        <item name="colorPrimaryContainer">@color/md_theme_dark_primaryContainer</item>
        <item name="colorOnPrimaryContainer">@color/md_theme_dark_onPrimaryContainer</item>
        
        <!-- Background colors -->
        <item name="android:colorBackground">@color/md_theme_dark_background</item>
        <item name="colorOnBackground">@color/md_theme_dark_onBackground</item>
        <item name="colorSurface">@color/md_theme_dark_background</item>
        <item name="colorOnSurface">@color/md_theme_dark_onBackground</item>
    </style>
</resources>
```

### Typography and Shapes (`res/values/styles.xml`)
Define standard text appearances and corner rounding.
```xml
<resources>
    <!-- Typography -->
    <style name="TextAppearance.MyApp.TitleLarge" parent="TextAppearance.Material3.TitleLarge">
        <item name="android:textSize">22sp</item>
        <item name="android:textStyle">normal</item>
    </style>

    <!-- Shapes -->
    <style name="ShapeAppearance.MyApp.SmallComponent" parent="ShapeAppearance.Material3.SmallComponent">
        <item name="cornerFamily">rounded</item>
        <item name="cornerSize">8dp</item>
    </style>
</resources>
```

## 3. Usage Rules
- **NEVER hardcode colors** in layouts (e.g., `android:textColor="#000000"`). Always reference theme attributes like `?attr/colorOnSurface` or `?attr/colorPrimary`.
- **NEVER hardcode text sizes** in layouts. Always reference standard text appearances like `?attr/textAppearanceBodyMedium`.
- Always use `com.google.android.material.*` components instead of standard Android widgets (e.g., use `MaterialButton` instead of `Button`, `MaterialTextView` instead of `TextView`).
