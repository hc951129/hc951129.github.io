## activity_main,xml
    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:orientation="vertical"
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <ImageView
            android:id="@+id/image_view2"
            android:layout_width="wrap_content"
            android:layout_height="200dp"
            android:layout_gravity="center_vertical"
            android:src="@drawable/pic_0"
            />
        <RelativeLayout
            android:orientation="horizontal"
            android:layout_width="match_parent"
            android:layout_height="wrap_content">
            <EditText
                android:id="@+id/edit_text"
                android:layout_width="match_parent"
                android:layout_height="50dp"
                android:hint="@string/addItemHint"
                android:contentDescription="@string/addItemContentDescription"
                />
            <Button
                android:id="@+id/button"
                android:layout_width="60dp"
                android:layout_height="40dp"
                android:layout_alignParentRight="true"
                android:gravity="center"
                android:text="@string/sendmessage"
                android:onClick="onclick"
                tools:ignore="OnClick" />
        </RelativeLayout>>

        <ListView
            android:id="@+id/list_view"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            />

    </LinearLayout>
