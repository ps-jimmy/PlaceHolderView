#**PlaceHolderView**
![](https://github.com/janishar/janishar.github.io/blob/master/images/logo-phv.png)

######Simple, Easy and Superfast dynamic view creation with Awesome animations prebuilt!

##Few Implementations
![](https://github.com/janishar/janishar.github.io/blob/master/gifs/vid_tinder.gif)![](https://github.com/janishar/janishar.github.io/blob/master/gifs/feed_vid.gif)![](https://github.com/janishar/janishar.github.io/blob/master/gifs/vid_slides.gif)

![](https://github.com/janishar/janishar.github.io/blob/master/gifs/vid_fade.gif)![](https://github.com/janishar/janishar.github.io/blob/master/gifs/vid_drawer.gif)  

##STEP 1: Define a PlaceHolderView inside XML layout
```java
//PlaceHolderView to wrap around the recycler view in XML
<com.mindorks.placeholderview.PlaceHolderView
        android:id="@+id/galleryView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>

```
##STEP 2: Create item views XML, example: gallery_item_big.xml
```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:padding="10dp">
    <android.support.v7.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:cardCornerRadius="6dp"
        app:cardElevation="6dp">
        <ImageView
            android:id="@+id/imageView"
            android:layout_width="match_parent"
            android:layout_height="250dp"
            android:scaleType="centerCrop"
            android:src="@android:color/holo_orange_dark"/>
    </android.support.v7.widget.CardView>
</LinearLayout>
```
##STEP 3: Create item class to bind and define view operations
```java
@Animate(Animation.ENTER_LEFT_DESC)
@NonReusable
@Layout(R.layout.gallery_item_big)
public class ImageTypeBig {

    @View(R.id.imageView)
    private ImageView imageView;

    private String mUlr;
    private Context mContext;
    private PlaceHolderView mPlaceHolderView;

    public ImageTypeBig(Context context, PlaceHolderView placeHolderView, String ulr) {
        mContext = context;
        mPlaceHolderView = placeHolderView;
        mUlr = ulr;
    }

    @Resolve
    private void onResolved() {
        Glide.with(mContext).load(mUlr).into(imageView);
    }

    @LongClick(R.id.imageView)
    private void onLongClick(){
        mPlaceHolderView.removeView(this);
    }

}
```

##STEP 4 : Add views to the PlaceHolderView
```java
 
 PlaceHolderView mGalleryView = (PlaceHolderView)findViewById(R.id.galleryView);

// (Optional): If customisation is Required then use Builder with the PlaceHolderView
// placeHolderView.getBuilder()
//      .setHasFixedSize(false)
//      .setItemViewCacheSize(10)
//      .setLayoutManager(new GridLayoutManager(this, 3));

  mGalleryView
        .addView(new ImageTypeBig(this.getApplicationContext(), mGalleryView, url1));
        .addView(new ImageTypeBig(this.getApplicationContext(), mGalleryView, url2));
        .addView(new ImageTypeBig(this.getApplicationContext(), mGalleryView, url3));
        .addView(new ImageTypeBig(this.getApplicationContext(), mGalleryView, url4));
```
##*That's All! Cheers!* :beer:

##Classes OverView

#PlaceHolderView
1. getBuilder(): Get builder for the PlaceHolderView to modify the default properties
2. setLayoutManager(layoutManager): Add custom layout manager
3. addView(): Add views to the PlaceHolderView
4. removeView(): Removes the existing view
5. SmoothLinearLayoutManager: This class is bundled with the library, and should be used for those view which has dynamic heavy contents. It reduces the screen flikering on bind

##Annotations
1. @Layout: Bind the XML layout with the class.
2. @View: Bind the variable with the view defined in the above layout.
3. @Click: Bind the OnClickListener to a view.
4. @LongClick: Bind the long click listerner to a view.
5. @Resolve: Any operation being performed on the view reference defined by @View should be annotated with this.
6. @Animate(Animation.ENTER_LEFT_DESC): Sets the defined animations in the Animation class on this item view.
7. @NonReusable: Releases the view reference along with all the attached references in the view object. This view object should not be used again in the addView().

#ExpandablePlaceHolderView
####This class is build upon the PlaceHolderView and implements all the features of ExpandableListView but with much power and lot easier

##Annotations(ExpandablePlaceHolderView)
1. @Parent: Defines the class to be used as the parent in the expandable list.
2. @SingleTop: Makes only one parent remain in expanded state.
3. @Collapse: Bind a method of the parent class to listen to the collapse event.
4. @Expand: Bind a method of the parent class to listen to the Expand event.
5. @ParentPosition: Bind an int variable to update with relative position among parents.
6. @ChildPosition: Bind an int variable to update with relative position among children of a parent.
7. @Toggle: Bind a view to be used as a trigger for expanding or collapsing a parent view. If not provided then the parent view becomes a toggle by default.

##There is no adapter configuration required

#SwipePlaceHolderView
####This class is bundled with view that can create beautiful card stacks like Tinder, LinkdIn and Card Games. This class provides methods to customize the behavior of the stack, gesture inputs and animations.

##SwipeDecor
####This class contains view behaviour settings and animation controls for SwipePlaceHolderView.

##Builder(SwipePlaceHolderView)
####The stack structure and type configurations are done using builder class

##Annotations(SwipePlaceHolderView)
1. @SwipeIn: It binds a method and calls it when a view is swiped in/accepted
2. @SwipeOut: It binds a method and calls it when a view is swiped out/rejected.
3. @SwipeCancelState: It binds a method and calls it when a card is put back in the stack/canceled.
4. @SwipeInState: It binds a method and pings it till a card is moving in the direction of swiping in/accepted
5. @SwipeOutState: It binds a method and pings it till a card is moving in the direction of swiping out/rejected

######The Full Documentation is in the process of writing. For any query post it in the discussion or janishar.ali@gmail.com

#Gradle
```java
dependencies {
    compile 'com.mindorks:placeholderview:0.1.0'
}
```
#Dependency: It depends on the RecyclerView
```java
    com.android.support:recyclerview-v7:23.+
```

###If this library helps you in anyway, show your love :heart: by putting a :star: on this project :v:

#Examples
[Android Navigation Drawer](https://medium.com/@janishar.ali/navigation-drawer-android-example-8dfe38c66f59#.vmlw4zb00)

[Android Beginner Image Gallery](https://medium.com/@janishar.ali/android-beginner-image-gallery-example-da73a596f4d5#.p42z8w83o)

[Android Advance Image Gallery](https://medium.com/@janishar.ali/android-advance-image-gallery-example-3ec6ddf85ed9#.6n8ouof9k)

[Android Expandable News Feed](https://medium.com/@janishar.ali/android-expandable-news-feed-example-4b4544e1fe7e#.3n9k18x2s)

[Android Tinder Swipe](https://medium.com/@janishar.ali/android-tinder-swipe-view-example-3eca9b0d4794#.413dgor3o)

#License

```
   Copyright (C) 2016 Janishar Ali Anwar

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License

```
