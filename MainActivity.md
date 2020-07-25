## MainActivity.java

    package com.example.notepad;

    import androidx.appcompat.app.AlertDialog;
    import androidx.appcompat.app.AppCompatActivity;
    import android.app.DatePickerDialog;
    import android.app.TimePickerDialog;
    import android.content.Context;
    import android.content.DialogInterface;
    import android.os.Bundle;
    import android.view.KeyEvent;
    import android.view.LayoutInflater; 
    import android.view.View;
    import android.widget.AdapterView;
    import android.widget.Button;
    import android.widget.DatePicker;
    import android.widget.EditText;
    import android.widget.ImageView;
    import android.widget.LinearLayout;
    import android.widget.ListView;
    import android.widget.TextView;
    import android.widget.TimePicker;   
    import android.widget.Toast;
    import java.util.ArrayList;
    import java.util.Calendar;
    import java.util.List;

### public class MainActivity extends AppCompatActivity {

    //定义了三个成员变量
    
        private List<PictureItem> pictureItemList = new ArrayList<>();    //用于存储每个Item独立的数据

        private String time;    //时间选择器选择的时间

        private String date;    //日期选择器选择的日期

#### BrushData方法

        public void BrushData(EditText editText, String string, PictureItemAdapter adapter) {
        //数据更新方法，参数1是EditText输入的内容，参数2是选择的时间，参数3是PictureItemAdapter类
     
            PictureItem initData = new PictureItem(editText.getText().toString(), string, R.drawable.pic_1, null);
            //创建一个新的PictureItem类型的实例initData，里面含有三个参数，第一个是EditText输入的内容，第二个是时间日期，第三个是图片，第四个是后面涉及的“具体内容”
            
            pictureItemList.add(initData);    //PictureItem类型的列表增加这个实例作为新的元素
            
            adapter.notifyDataSetChanged();    //adapter更新
            
            editText.setText("");    //EditText内容更新为空
        }


#### 重写OnCreate方法，活动的初始化操作
        @Override
        protected void onCreate(final Bundle savedInstanceState) {
        
            super.onCreate(savedInstanceState); 
            setContentView(R.layout.activity_main);

            final PictureItemAdapter adapter = new PictureItemAdapter(MainActivity.this, R.layout.pic_item, pictureItemList);

            //获取对UI组件的引用
            final ListView listView = (ListView) findViewById(R.id.list_view);
            final EditText editText = (EditText) findViewById(R.id.edit_text)；
            Button button = (Button) findViewById(R.id.button);

            //将ArrayAdapter绑定到ListView
            listView.setAdapter(adapter);    //把列表的Item和pictureItemList列表的每一个元素绑定

#### Enter按键监听(指的是手机虚拟键盘的Enter键)
/*      //监听myEditText的Enter键，注释掉了的原因是Enter键用来换行了，新增加了Button“添加”按钮来实现该功能
        editText.setOnKeyListener(new View.OnKeyListener(){
            
            @Override            
            public boolean onKey(View view, int keyCode, KeyEvent keyEvent){            
                if(keyEvent.getAction()==keyEvent.ACTION_DOWN){            
                    if((keyCode == keyEvent.KEYCODE_DPAD_CENTER) || (keyCode == keyEvent.KEYCODE_ENTER)){
                        PictureItem initData = new PictureItem(editText.getText().toString() R.drawable.pic_1);
                        pictureItemList.add(initData);
                        adapter.notifyDataSetChanged();
                        editText.setText("");
                        return true;
                    }
                }
                return false;
            }
        });*/
#### “添加”按钮监听，每次点击新建一个Item项
        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Calendar calendar = Calendar.getInstance();
                //日期选择器
                DatePickerDialog datePickerDialog = new DatePickerDialog(MainActivity.this, new DatePickerDialog.OnDateSetListener() {
                    @Override
                    public void onDateSet(DatePicker view, int year, int month, int dayOfMonth) {
                        date = year + "年" + (month + 1) + "月" + dayOfMonth + "日";
                        String string = date + time + "您有新的日程安排";
                        Toast.makeText(MainActivity.this, string, Toast.LENGTH_SHORT).show();
                        BrushData(editText, (date + "\n" + time), adapter);
                    }
                }, calendar.get(Calendar.YEAR), calendar.get(Calendar.MONTH), calendar.get(Calendar.DAY_OF_MONTH));
                datePickerDialog.show();

                //时间选择器
                TimePickerDialog timePickerDialog = new TimePickerDialog(MainActivity.this, new TimePickerDialog.OnTimeSetListener() {
                    @Override
                    public void onTimeSet(TimePicker timePicker, int hourOfDay, int minute) {
                        time = hourOfDay + "时" + minute + "分";
                    }
                }, calendar.get(Calendar.HOUR_OF_DAY), calendar.get(Calendar.MINUTE), true);
                timePickerDialog.show();
            }
        });

#### 监听Item项的点击事件
、、、markdown
        //监听listView的Item的点击键
        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> adapterView, View view, int i, long l) {
                ImageView imageView = (ImageView) view.findViewById(R.id.image_view);
                if (pictureItemList.get(i).getImageId() == R.drawable.pic_1) {
                    imageView.setImageResource(R.drawable.pic_2);
                    pictureItemList.get(i).setImageId(R.drawable.pic_2);
                } else if (pictureItemList.get(i).getImageId() == R.drawable.pic_2) {
                    imageView.setImageResource(R.drawable.pic_1);
                    pictureItemList.get(i).setImageId(R.drawable.pic_1);
                }
            }
        });

#### 监听Item项的长按事件
        //监听listView的Item的长按键
        listView.setOnItemLongClickListener(new AdapterView.OnItemLongClickListener() {
            @Override
            public boolean onItemLongClick(AdapterView<?> adapterView, final View view, final int i, long l) {
                final AlertDialog.Builder dialog = new AlertDialog.Builder(MainActivity.this);
                dialog.setTitle("提示!");
                dialog.setMessage("请选择您要做出的改变：");
                LayoutInflater inflater = (LayoutInflater) MainActivity.this.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
                LinearLayout layout = (LinearLayout) inflater.inflate(R.layout.dialog_view, null);
                dialog.setView(layout);
                final EditText editText1 = (EditText) layout.findViewById(R.id.edit_text1);
                final EditText editText2 = (EditText) layout.findViewById(R.id.edit_text2);
                final EditText editText3 = (EditText) layout.findViewById(R.id.edit_text3);
                editText1.setText(pictureItemList.get(i).getName());
                editText2.setText(pictureItemList.get(i).getTimeClock());
                editText3.setText(pictureItemList.get(i).getConcreteContext());
                dialog.setCancelable(false);
                dialog.setNegativeButton("删除", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int which) {
                        pictureItemList.remove(i);
                        adapter.notifyDataSetChanged();
                    }
                });
              //在dialog界面点击修改键弹出新的dialog界面，后来功能简化到同一个dialog界面中
              //dialog.setNeutralButton("修改", new DialogInterface.OnClickListener() {
              //    @Override
              //     public void onClick(DialogInterface dialogInterface, int which) {
              //        final AlertDialog.Builder builder = new AlertDialog.Builder(MainActivity.this);
              //        LayoutInflater inflater = (LayoutInflater)MainActivity.this.getSystemService(Context.LAYOUT_INFLATER_SERVICE);
              //        LinearLayout layout = (LinearLayout)inflater.inflate(R.layout.dialog_view,null);
              //        builder.setView(layout);
              //        final EditText editText1 = (EditText)layout.findViewById(R.id.edit_text1);
              //        final EditText editText2 = (EditText)layout.findViewById(R.id.edit_text2);
              //        editText1.setText(pictureItemList.get(i).getName());
              //        editText2.setText(pictureItemList.get(i).getTimeClock());
              //        builder.setPositiveButton("确定", new DialogInterface.OnClickListener() {
              //            @Override
              //            public void onClick(DialogInterface dialogInterface, int which2) {
              //                pictureItemList.get(i).setName(editText1.getText().toString());
              //                pictureItemList.get(i).setTimeClock(editText2.getText().toString());
              //                adapter.notifyDataSetChanged();
              //            }
              //        });
              //        builder.setNegativeButton("取消", new DialogInterface.OnClickListener() {
              //            @Override
              //            public void onClick(DialogInterface dialogInterface, int i) {
              //                return;
              //            }
              //        });
              //        builder.show();
              //    }
              //});
              dialog.setPositiveButton("确认", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialogInterface, int which) {
                        pictureItemList.get(i).setName(editText1.getText().toString());
                        pictureItemList.get(i).setTimeClock(editText2.getText().toString());
                        pictureItemList.get(i).setConcreteContext(editText3.getText().toString());
                        adapter.notifyDataSetChanged();
                    }
                });
              dialog.setNeutralButton("取消", new DialogInterface.OnClickListener() {
                  @Override
                  public void onClick(DialogInterface dialogInterface, int i) {
                  }
              });
              dialog.show();
              return false;
          }
      });
    }
}

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/hc951129/hc951129.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
