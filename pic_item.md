## pic_item.xml
    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:orientation="horizontal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <ImageView
            android:id="@+id/image_view"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center_vertical"
        />

        <TextView
            android:id="@+id/text_view"
            android:layout_width="210dp"
            android:layout_height="wrap_content"
            android:layout_gravity="center_vertical"
            />

        <TextView
            android:id="@+id/text_view2"
            android:layout_width="110dp"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:text="22:50"
            />

        <TextView
            android:id="@+id/text_view3"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:visibility="gone"
            />

    </LinearLayout>
