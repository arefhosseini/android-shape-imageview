# Shape Image View (Compatible with AndroidX)
[![](https://jitpack.io/v/arefhosseini/android-shape-imageview.svg)](https://jitpack.io/#arefhosseini/android-shape-imageview)
[![](https://jitci.com/gh/arefhosseini/android-shape-imageview/svg)](https://jitci.com/gh/arefhosseini/android-shape-imageview)

## How to use

<b>Step 1.</b> Add JitPack repository in your root build.gradle at the end of repositories:

```groovy
allprojects {
	repositories {
		...
		maven { url 'https://jitpack.io' }
	}
}
```

<b>Step 2.</b> Add the dependency:

```groovy
dependencies {
    implementation 'com.github.arefhosseini:android-shape-imageview:1.0.3'
}
```
###Shader Based ImageView's
####BubbleImageView
![Android Bubble ImageView](images/small-bubble.png)
```XML
<com.github.siyamed.shapeimageview.BubbleImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:src="@drawable/neo"
    app:siArrowPosition="right"
    app:siSquare="true"/>
```

Attributes:
* `siTriangleHeight` the height of the bubble pointer in dp
* `siArrowPosition` where to point the arrow, currently `left|right`
* `siSquare` set width and height to the minimum of the given values `true|false`

####RoundedImageView
![Android Rounded Rectangle ImageView](images/small-rounded.png)
```XML
<com.github.siyamed.shapeimageview.RoundedImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:src="@drawable/neo"
    app:siRadius="6dp"
    app:siBorderWidth="6dp"
    app:siBorderColor="@color/darkgray"
    app:siSquare="true"/>
```

Attributes:
* `siBorderColor` border color
* `siBorderWidth` border width in dp
* `siBorderAlpha` alpha value of the border between 0.0-1.0
* `siRadius` corner radius in dp
* `siSquare` set width and height to the minimum of the given values `true|false`

####CircularImageView
![Android Circular ImageView](images/small-circle.png)
```XML
<com.github.siyamed.shapeimageview.CircularImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:src="@drawable/neo"
    app:siBorderWidth="6dp"
    app:siBorderColor="@color/darkgray"/>
```

Attributes:
* `siBorderColor` border color
* `siBorderWidth` border width in dp
* `siBorderAlpha` alpha value of the border between 0.0-1.0

####ShapeImageView
This view has the capability to process a provided SVG file (for a limited set of SVG elements), build a 
[Path][Path] object and draw it on the shader. The library includes SVG files defining a set of basic shapes and 
ShapeImageView subclasses using those files. You can use whatever SVG you want to have a wonderful 
and creatively shaped images in your application. The included SVG files are under [library/src/main/res/raw][svg_location]


| DiamondImageView                                       | PentagonImageView                                        | HexagonImageView                                         |
| ------------------------------------------------------ | -------------------------------------------------------- | -------------------------------------------------------- |
| ![Android Diamond ImageView](images/small-diamond.png) | ![Android Pentagon ImageView](images/small-pentagon.png) | ![Android Hexagon ImageView](images/small-hexagon.png)   |


| OctogonImageView                                       | StarImageView                                            | HeartImageView                                       |
| ------------------------------------------------------ | -------------------------------------------------------- | ---------------------------------------------------- |
| ![Android Octogon ImageView](images/small-octogon.png) | ![Android Start ImageView](images/small-star.png)        | ![Android Heart ImageView](images/small-heart.png)   |


```XML
<com.github.siyamed.shapeimageview.{ClassName}
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_margin="8dp"
    android:src="@drawable/neo"
    app:siBorderWidth="8dp"
    app:siBorderColor="@color/darkgray"/>
```

Attributes:
* `siBorderColor` border color
* `siBorderWidth` border width in dp
* `siBorderAlpha` alpha value of the border between 0.0-1.0
* `siStrokeCap` border stroke cap type `butt|round|square`
* `siStrokeJoin` border stroke join type `bevel|miter|round`
* `siSquare` set width and height to the minimum of the given values `true|false`
* `siShape` a reference to an SVG. This is used by ShapeImageView, not the subclasses of it.


SVG elements that are supported are: [rectangle][svg_rectangle], [circle][svg_circle], 
[ellipse][svg_ellipse], [polygon][svg_polygon], [path][svg_path], [group][svg_group]. [Transformations][svg_transformations] on those elements are also supported. 

The system converts an SVG file into a Path. For each element including the parent element `<svg>` a new Path is created, and all the children Path's are [added][Path.addPath] to their parent path. 

###Bitmap Mask Based ImageViews 

This view uses extra bitmaps for bitmap masks. Therefore it would be good to use them for very custom shapes, 
possibly not in a recycling view. 

* With [mask bitmap](sample/src/main/res/drawable/star.png): 

![Android Star Shape ImageView ](images/small-mask-star.png)
```XML
<com.github.siyamed.shapeimageview.mask.PorterShapeImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:siShape="@drawable/star"
    android:src="@drawable/neo"
    app:siSquare="true"/>
```

* With [shape XML](sample/src/main/res/drawable/shape_rounded_rectangle.xml):

![Android Star Shape ImageView ](images/small-xmlshape-rounded.png)

```XML
<com.github.siyamed.shapeimageview.mask.PorterShapeImageView
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:siShape="@drawable/shape_rounded_rectangle"
    android:src="@drawable/neo"
    app:siSquare="true"/>
```

rounded rectangle shape definition in XML: 

```XML
<shape android:shape="rectangle" xmlns:android="http://schemas.android.com/apk/res/android">
    <corners
        android:topLeftRadius="18dp"
        android:topRightRadius="18dp"
        android:bottomLeftRadius="18dp"
        android:bottomRightRadius="18dp" />
    <solid android:color="@color/black" />
</shape>
```

Attributes:
* `siShape` the bitmap mask shape, either a shape drawable or a bitmap
* `siSquare` set width and height to the minimum of the given values `true|false`

This method reads a shape file (either bitmap or an android shape xml), creates a bitmap object using this shape, and finally combines the bitmap of the real image to be shown and the mast bitmap using xfermode. 

## Sample

See/execute the [sample](sample) for a demonstration of the components.

## Proguard

```
-dontwarn android.support.v7.**
-keep class android.support.v7.** { ; }
-keep interface android.support.v7.* { ; }
-keepattributes *Annotation,Signature
-dontwarn com.github.siyamed.**
-keep class com.github.siyamed.shapeimageview.**{ *; }
```
