## 第一步、Android studio新项目的导入
下载一个gradle，下载链接：[https://gradle.org/](https://gradle.org/)
下载成功后得到一个压缩包如图：
![](https://img-blog.csdnimg.cn/20201006140954834.png#pic_center)
在Android Studio中找到目录gradle-wrapper下的配置文件，修改其中的distributionUrl，修改为压缩包所在目录，如图：
![](https://img-blog.csdnimg.cn/20201006141227272.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70#pic_center)  
然后修改setter-gradle路径和缓存路径：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020112023045251.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70#pic_center)
把原来可以运行的程序的这两个文件拷贝过来：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201120230354812.png#pic_center)  
  
  
## 第二步、读懂包结构  
![](https://img-blog.csdnimg.cn/20201217130701699.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70)  
NoteEditor类：实现了编辑类便签内容的功能和与UI的接口。  
NotePad类：提供服务器和客户端的协议、列名、URI。  
NotePadProvider类：笔记本的创建、更新、保存等功能都在这里。  
NotesList类：应该是实现了笔记本在应用中的表层面，用到了标题，用到了id等信息。  
NotesLiveFolder类：得到用户做了什么活动，在主页中相应用户的操作。  
TitleEditor类：标题的修改类。

![](https://img-blog.csdnimg.cn/20201217133129463.png)  
这三个app_notes是头部图标，比如如图所示：  
![](https://img-blog.csdnimg.cn/2020121713323688.png)  
新建按钮图标的图片是这两张图ic_menu_compose：  
![](https://img-blog.csdnimg.cn/20201217133326482.png)   
删除按钮图标的图片是这两张图ic_menu_delete：  
![](https://img-blog.csdnimg.cn/20201217133445720.png)  
新建按钮图标的图片是这两张图ic_menu_edit(但是好像并没有在程序中体现)：  
![](https://img-blog.csdnimg.cn/20201217133653819.png)  
返回按钮图标的图片是这两张图ic_menu_revert(但是好像并没有在程序中体现)：  
![](https://img-blog.csdnimg.cn/20201217133751224.png)  
保存按钮图标的图片是这两张图ic_menu_save(返回功能体现在保存里了)：  
![](https://img-blog.csdnimg.cn/20201217133903403.png)  
笔记本文件图标的图片是这两张图ic_folder_notes但是好像并没有在程序中体现)：  
![](https://img-blog.csdnimg.cn/20201217134057481.png)  
接下来是layout包：    
![](https://img-blog.csdnimg.cn/2020121713442956.png)  
它们分别对应内容编辑界面：   
![](https://img-blog.csdnimg.cn/20201217134505441.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70)  
列表界面：  
![](https://img-blog.csdnimg.cn/20201217134603608.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70)  
标题编辑界面：  
![](https://img-blog.csdnimg.cn/20201217134645582.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70)  
menu包：  
![](https://img-blog.csdnimg.cn/20201217135006640.png)  
编辑器选项菜单：  
![](https://img-blog.csdnimg.cn/20201217135139491.png)

列表长按菜单：  
![](https://img-blog.csdnimg.cn/20201217135154750.png)  
列表选项菜单：  
![](https://img-blog.csdnimg.cn/20201217135221409.png)  
标签名字：  
![](https://img-blog.csdnimg.cn/20201217135301372.png)  
## 第三步、在笔记本列表中添加时间戳  
第一步、找到NotesList中的添加视图的语句  
![](https://img-blog.csdnimg.cn/20201217202905459.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70)  
前面我们学过，SimpleCursoraAdapter是用来创建ListView的方法之一，这里可以看到dataColumns和viewIDs，分别是数据和视图id。
那么我们第一步：  
在视图中添加一个文本框：  
在原有的基础上添加一个垂直的线性布局，和一个文本视图，如图所示：  
![](https://img-blog.csdnimg.cn/20201217204856786.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70)  
将上上图中的java代码行的语句里添加成如图所示：  
![](https://img-blog.csdnimg.cn/20201217225937913.png)  
由于代码是别人的，这个逻辑写出来出错如图：  
![](https://img-blog.csdnimg.cn/20201217230132416.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70)  
查了别人的逻辑之后，在Notelist类中的字符串数组中添加语句如图：  
![](https://img-blog.csdnimg.cn/2020121723030579.png)
  


我们现在得到的运行结果是这样的：  
![](https://img-blog.csdnimg.cn/20201217205126334.png)  
有一串数字，对应的是修改时间，你修改一下标签它就会改变。那么这个值在哪里？它又怎么改写成时间格式呢？  

我们第一个思路是在NotesList类里面直接修改  

```xml
NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE
```
的值，将时间赋给它，但是不行，传入如图  
![](https://img-blog.csdnimg.cn/20201217230531747.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70)  
这个构造方法的时候类型错误，尝试修改前面的数组直接加入时间，也不行，于是还是参考别人的逻辑，在编辑保存返回值的时候再改变
```xml
NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE
```
的值，即在NoteEditor中做如下修改：  

```java
ContentValues values = new ContentValues();
SimpleDateFormat sf = new SimpleDateFormat("yy/MM/dd HH:mm:ss");
values.put(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE,sf.format(new Date()));
```
于是时间戳功能得以实现（成果如图）：  
![](https://img-blog.csdnimg.cn/20201217231326377.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70)  
## 第四步、在笔记本中添加搜索框  
1.先添加一个搜索框视图：  
![](https://img-blog.csdnimg.cn/20201217233545545.png)  
2.编辑搜索框格式：  

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <!--垂直布局，listView用来显示自动搜索的内容-->
    <SearchView
        android:id="@+id/search2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:queryHint="请输入搜索内容"
        >
    </SearchView>
    <ListView
        android:paddingLeft="10dp"
        android:paddingRight="10dp"
        android:id="@android:id/list"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:drawSelectorOnTop="false" />
    <TextView
        android:paddingLeft="10dp"
        android:paddingRight="10dp"
        android:id="@android:id/empty"
        android:gravity="center"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:text="无搜索结果" />
</LinearLayout>

```
3.添加布局文件到Notelist类的初始方法里：  
![](https://img-blog.csdnimg.cn/2020121723423930.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70)    
4.在Notelist类中添加一个搜索框监听器，方法是用别人的，理解即可，代码如下：  

```java
public void SearchView(final SimpleCursorAdapter adapter) {
        SearchView searchView = findViewById(R.id.search);
        searchView.setSubmitButtonEnabled(true);
        searchView.setOnQueryTextListener(new SearchView.OnQueryTextListener() {
            // 单击搜索按钮时激发该方法
            @Override
            public boolean onQueryTextSubmit(String query) {
                return false;
            }
            // 用户输入字符时激发该方法
            @Override
            public boolean onQueryTextChange(String s) {
                Cursor newCursor;

                if (!s.equals("")) {
                    String selection = NotePad.Notes.COLUMN_NAME_TITLE + " GLOB '*" + s + "*'";
                    newCursor = getContentResolver().query(
                            getIntent().getData(),
                            PROJECTION,
                            selection,
                            null,
                            NotePad.Notes.DEFAULT_SORT_ORDER
                    );
                } else {
                    newCursor = getContentResolver().query(
                            getIntent().getData(),
                            PROJECTION,
                            null,
                            null,
                            NotePad.Notes.DEFAULT_SORT_ORDER
                    );
                }
                adapter.swapCursor(newCursor); // 视图将同步更新！
                return true;
            }
        });
    }
```
注意，写完这个方法后还要在初始化方法中onCreate中加入语句：  

```java
SearchView(adapter);
```
它的意思是，初始化的同时传入SimpleCursorAdapter对象，初始化查询监听器。  
在没实现以上功能之前，单击这个图标：  
![](https://img-blog.csdnimg.cn/20201218010659216.png)  
它会出现：  
![](https://img-blog.csdnimg.cn/2020121801072159.png)  
但是输入内容没用。
实现功能之后，输入内容它会自动显示如图所示：  
![](https://img-blog.csdnimg.cn/20201218010811607.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0ltcGVybWFuZW50,size_16,color_FFFFFF,t_70)  




  

  












  













