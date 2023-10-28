开发中我们可能需要对List集合进行手动分页，使用list的subList方法可以方便实现分页
```java
//subList手动分页，page为第几页，rows为每页个数
public static List<T> subList(List<T> list, int page, int rows) throws Exception{
    List<T> listSort  = new ArrayList<>();
    int size=list.size();
    int pageStart=page==1?0:(page-1)*rows;//截取的开始位置
    int pageEnd=size<page*rows?size:page*rows;//截取的结束位置
    if(size>pageStart){
        listSort =list.subList(pageStart, pageEnd);
    }
    //总页数
    int totalPage=list.size()/rows;
    return listSort;
}

```
