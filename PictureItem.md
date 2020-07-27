## PictureItem.java
    package com.example.notepad;
    
### PictureItem类，内含4个成员变量，对应PictureItemAdapter.java中的4个控件
    public class PictureItem {
        private String name;
        private String timeClock;
        private int imageId;
        private String concreteContext;
### 初始化
        public PictureItem(String name, String timeClock, int imageId, String concreteContext) {
            this.name = name;
            this.timeClock = timeClock;
            this.imageId = imageId;
            this.concreteContext = concreteContext;
        }
### get和set方法
        public String getName() {
            return name;
        }

        public String getTimeClock() {
            return timeClock;
        }

        public int getImageId() {
            return imageId;
        }

        public String getConcreteContext() {
            return concreteContext;
        }

        public void setName(String name) {
            this.name = name;
        }

        public void setTimeClock(String timeClock) {
            this.timeClock = timeClock;
        }

        public void setImageId(int imageId) {
            this.imageId = imageId;
        }

        public void setConcreteContext(String concreteContext) {
            this.concreteContext = concreteContext;
        }

    }
