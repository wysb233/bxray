# replace扩展

#### 例子

~~~java

//@Reset desc描述 name名字 使用@Reset标记一个字段后这个字段的值可以被/replace设置
//@Replace key替换的key desc描述


//如 敌人在这里#radar.location -> 敌人在这里X :0 , Y:0 , Z:0
 @Reset(desc = "#x #y #z", name = "RadarLocation")
 private String radarlocation = "X :#x , Y:#y , Z:#z";

 /**
     * 
     * @param str 无具体作用
     * @return 返回要被替换的内容
     */
 @Replace(key = "#radar.location", desc = "雷声追踪最后一次追踪的位置")
 public String RadarLocation(String str) {
        int x = (int) ReplaceManager.radar.getX();
        int y = (int) ReplaceManager.radar.getY();
        int z = (int) ReplaceManager.radar.getZ();
        return mylocation.replace("#x", x + "").replace("#y", y + "").replace("#z", z + "");


}


~~~


#### ReplaceManager

~~~java

public String processAll(String str) {
        for (Replace replace : replacems.keySet()) {
            try {
                str = str.replace(replace.key(), (String) replacems.get(replace).invoke(Config.getReplaces(), str));
            } catch (IllegalAccessException e) {
                e.printStackTrace();
            } catch (InvocationTargetException e) {
                e.printStackTrace();
            }
       }
      return str;
}

~~~

