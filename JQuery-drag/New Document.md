#这是基于jQuery的一个拖拽插件

					引用文件
					<script src="jquery.js"></script>
					<script src="jQuery-drag.js"></script>

###使用方式

   	<style>
        .item_content ul  {
            list-style:none;
        }
        .item_content ul li {
            width:200px;
            height:20px;
            margin:10px;
        }
    
    	// 由于插件内容是根据item.content类名来获取需要拖拽的元素的,所以这个类名必须是定位流
        .item_content {
            width:740px;
            height:460px;
            margin:0 auto;
            position: relative;
        }
        .item_content .item {
            width:200px;
            height:20px;
            line-height:20px;
            text-align:center;
            cursor:pointer;
            background:#ccc;
        }
    </style>
    
    </head>
    <body>
    <div >
    // 结构层次必须是这样
    <div class="item_content">
        <ul>
            <li>A 
    // li里面可以不写任何东西,但是必须放div.而且div的类名为item
                <div class="item">
                    1
                </div>
            </li>
            <li>B
                <div class="item">
                    2
                </div>
            </li>
            <li>C
                <div class="item">
                    3
                </div>
            </li>
            <li>D
                <div class="item">
                    4
                </div>
            </li>
            <li>E
                <div class="item">
                    5
                </div>
            </li>
            <li>F
                <div class="item">
                    6
                </div>
            </li>
        </ul>
    </div>
    </div>
    
    				<script src="jquery.js"></script>
    				<script src="jQuery-drag.js"></script>



拿到拖拽数组的起始index.和放置的index.可用于拖拽事件完成之后,完成数组的交换

```
// 这是拖拽插件内部的拖拽方法代码
this.drag = function() { // 拖拽
    var oldPosition = new Position() ;
    var oldPointer = new Pointer() ;
    var myTime;
    var isDrag = false ;
    var currentItem = null ;

    $(this).mousedown(function(e) {
        console.log(e.target);
        if(!indexObj.canDrag){
            return
        }

        e.preventDefault() ;
        scrollMove =  parent.scrollTop();
        
        // 在下面这行代码中,通过$(this).attr("index) 可以拿到拖拽起始的index
        indexObj.start = $(this).attr("index")
        oldPosition.left = $(this).position().left ;
        oldPosition.top =  $(this).position().top ;
        oldPointer.x = e.clientX ;
        oldPointer.y = e.clientY ;
        isDrag = true ;

        currentItem = this ;

    }) ;
    $(document).mousemove(function(e) {
        if(!isDrag) return false ;
        var currentPointer = new Pointer(e.clientX, e.clientY) ;
        isMove = true;
        clearInterval(myTime);
        $(currentItem).css({
            "opacity" : "0.8",
            "z-index" :1
        }) ;

        if(currentPointer.y < parent.offset().top ){
            clearInterval(myTime);
            myTime = setInterval(function () {
                        parent.scrollTop(scrollMove -= 2);
                    },10)

        }
        else if(currentPointer.y > (parent.offset().top + parent.height())  ){
            clearInterval(myTime);
            myTime = setInterval(function () {
                parent.scrollTop(scrollMove += 2);
            },10)

        }
        var left = currentPointer.x - oldPointer.x + oldPosition.left ;
        var top = currentPointer.y - oldPointer.y + oldPosition.top + parent.scrollTop()  ;

        $(currentItem).css({
            left : left,
            top : top
        }) ;
        currentItem.pointer = currentPointer ;
        // 开始交换位置

        currentItem.collisionCheck() ;


    }) ;
    $(document).mouseup(function() {
        if(!isDrag) return false ;
        isDrag = false ;
        clearInterval(myTime);
        // 在这里拿到拖拽完成之后的index. 可以自定义变量,或者对象进行保存,
        indexObj.end = $(currentItem).attr("index");
        currentItem.move(function() {
            $(this).css({
                "opacity" : "1",
                "z-index" : 0
            }) ;
        }) ;
        isMove = false;
    }) ;

}
```