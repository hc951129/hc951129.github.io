## PictureItemAdapter.java
    package com.example.notepad;
    import android.content.Context;
    import android.view.LayoutInflater;
    import android.view.View;
    import android.view.ViewGroup;
    import android.widget.ArrayAdapter;
    import android.widget.ImageView;
    import android.widget.TextView;

    import java.util.List;

    import androidx.annotation.NonNull;
    import androidx.annotation.Nullable;
    
### 这种继承方法用来实现ListView的功能很有帮助   
### public class PictureItemAdapter extends ArrayAdapter {

    private int resourceId;

### PictureItemAdapter构造方法
    public PictureItemAdapter(@NonNull Context context, int textViewResourceId, @NonNull List objects) {
        super(context, textViewResourceId, objects);
        resourceId = textViewResourceId;
    }

### 重写 getView方法，因为每个Item需要4个参数，分别是可选框(imageView)，输入的内容(textView)，选择的时间日期(textView2),长按后的具体内容(textView3)
    @Override
    public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
        PictureItem pictureItem = (PictureItem) getItem(position);
        View view = LayoutInflater.from(getContext()).inflate(resourceId,parent,false);
        ImageView imageView = (ImageView) view.findViewById(R.id.image_view);
        TextView textView = (TextView)view.findViewById(R.id.text_view);
        TextView textView2 = (TextView)view.findViewById(R.id.text_view2);
        TextView textView3 = (TextView)view.findViewById(R.id.text_view3);
        imageView.setImageResource(pictureItem.getImageId());
        textView.setText(pictureItem.getName());
        textView2.setText(pictureItem.getTimeClock());
        textView3.setText(pictureItem.getConcreteContext());
        return view;
    }
}
