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



