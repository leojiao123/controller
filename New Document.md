![](http://wx4.sinaimg.cn/mw690/71085e2bly1fmxekr259wg20dn0pbqm1.gif)

1:  h5 controller demo示例
	 	
	  点击按钮获取后台数据进行 html 模态框的弹出,这里连接的为本机tomcat 所搭建服务器
	  用浏览器承载html内容，支持 汇贷客中  h5 与 原生的所有交互
	
	  返回的数据模型如下
			
		第一种 html 的对话框数据模型
	
		public String grant_type; 
			// 弹出对话框的类型（共有3种）1：html 类型的对话框
   	 
		public boolean status;  
			// 是否可关闭(点击对话框外部空白处对话框消失)
   		
		public String href; 
			//  html 对话框所展示内容的链接
    	
		public Object action; 
			// 所携带的action (该action 为2级controller，
			   与本层controller结构完全一致，
			   提供给h5处理该action的 方法可以实现数据的嵌套，
			   1级controller 弹出后续controller 时使用 )
				
		public Boolean showDragView; 
			// 是否显示右下角的可拖拽按钮
    	
		public Boolean canDrag; 
			// 右下角的可拖拽按钮是否可以拖动
    	
		public String dragImageUrl; 
			// 拖拽按钮的图片地址
    	
		public double widthRate;  
			// 整个对话框的宽度（包括关闭按钮）
			   数值单位从 0 - 1  1为设备屏幕宽度
			   本地默认值默认为0.8

		public double widthHeightRate;    	
			// 宽高比例  
			   该html 的高度由宽度计算而来
 			   计算方式为宽度*widthHeightRate
			   (android  端可以实现高度自适应 ，返回0的话为高度自动适应 ，ios 端支持与否暂不确定)

		public double bacRate;  
			// 背景的透明度   
			   从 0-1 黑色的背景透明度
               0为全透明  1 为全黑
		
		public double delayTime; 
			// 延时弹出对话框，单位秒
		

		## 该图中所用的数据如下 ##

		{
		    "bacRate": 0.6,  // 透明度0.6
		    "canDrag": true, //有下角图标可拖动 
		    "dragImageUrl": "http://192.168.8.244:8080/drag.jpg",   // 可拖动按钮的图片源
		    "grant_type": "dialog_h5",  // 声明该 模态框的类型为h5
		    "href": "http://192.168.8.244:8080/test.html",  // 该h5所链接的地址
		    "showDragView": true,  // 右下角的可拖动按钮是否可见
		    "status": true,  // 点击空白处是否可关闭
		    "widthHeightRate": 0, // 宽高比例
		    "widthRate": 0.9,		// 宽度所占屏幕比例
			"delayTime": 0.0  // 不做延时 
		}	
		
		 该h5类型对话框存在的弊端为加载完成之前会有 一段加载时间，就算把所有的h5资源缓存到本地也会有
			一段加载时间，该时间为浏览器下载资源时间+浏览器渲染html的时间

		
![](http://wx3.sinaimg.cn/mw690/71085e2bly1fmxekwhodkg20d80nn7bx.gif)




2:  img controller demo示例

	点击按钮获取后台数据进行 单张图片模态框的弹出（与上一版的imgcontroller改变不大） 
	第一次弹出会有加载图片的过程，可以选择图片加载完成后再弹出对话框，这样会增加整体弹出的时间
	
	数据模型如下
	
	public CloseBtnStatusBean btn_close; 
		// 关闭按钮配置

    public String grant_type;  
		// 弹出模型类型

    public boolean status;  
		// 点击空白处是否可关闭对话框

    public String picture_url; 
		// 图片地址

    public Object action; 
		// 所携带的action (该action 为2级controller，
			   与本层controller结构完全一致，
			   提供给h5处理该action的 方法可以实现数据的嵌套，
			   1级controller 弹出后续controller 时使用 )

   	public Boolean showDragView; 
			// 是否显示右下角的可拖拽按钮
    	
	public Boolean canDrag; 
		// 右下角的可拖拽按钮是否可以拖动
	
	public String dragImageUrl; 
		// 拖拽按钮的图片地址
	
	public double widthRate;  
		// 整个对话框的宽度（包括关闭按钮）
		   数值单位从 0 - 1  1为设备屏幕宽度
		   本地默认值默认为0.8

	public double widthHeightRate;    	
		// 宽高比例  
		   该html 的高度由宽度计算而来
			   计算方式为宽度*widthHeightRate
		   (android  端可以实现高度自适应 ，返回0的话为高度自动适应 ，ios 端支持与否暂不确定)

	public double bacRate;  
		// 背景的透明度   
		   从 0-1 黑色的背景透明度
           0为全透明  1 为全黑
	
	public double delayTime; 
		// 延时弹出对话框，单位秒

    public static class CloseBtnStatusBean {
        public boolean status; // 是否关闭按钮 true 显示 false 不显示
        public String location; // 关闭按钮的位置
    }
		
	public double delayTime; 
			// 延时弹出对话框，单位秒

	## 该图中所用的数据如下 ##

		{
		    "action": "",  // 下级controller 无
		    "bacRate": 0.6, // 背景透明度 0.6 
		    "btn_close": {
		        "location": "top-right", // 关闭按钮位置右上角
		        "status": true  // 关闭按钮可用
		    },
		    "canDrag": true,  //右下角小图标可拖拽 
		    "dragImageUrl": "http://192.168.8.244:8080/drag.jpg", // 右下角小图标地址
		    "grant_type": "dialog_picture",  // 声明模态框类型为img类型
		    "picture_url": "https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=837922046,2961098478&fm=27&gp=0.jpg", // 图片地址
		    "showDragView": true, //  屏幕右下角显示小图标
		    "status": true, // 点击空白处是否可关闭对话框
		    "widthHeightRate": 0, // 宽高比为0 代表高度自适应
		    "widthRate": 0.9  // 整体宽度为屏幕宽度的0.9  (包含关闭按钮) 
		}

	
3:  link controller demo  
	返回的数据类型为
	{
		    "grant_type": "h5",  // 直接跳转 html 
		    "href": "" // 跳转的链接 
		    "delayTime": 0.0 //  延时跳转时间
	}

4： 附 我的界面item 服务端control 示例
![](http://192.168.8.244:8080/menutest.png)

该图中所有数据为后台返回数据
以第一个菜单的数据为例
		
		{
			"leftIconUrl": "http://192.168.8.244:8080/item1.png",  // 最左侧图片的地址
			"leftIconHeight": 25, // 左侧图片高度，宽度为自适应 单位为dp 对像素的换算在不同分辨率的设备上换算不同,在该机上为50px
			"rightIconUrl": "http://192.168.8.244:8080/right_arrow.png",  // 最右侧的箭头图片地址
			"rightIconHeight": 20, // 右侧的图片高度
			"itemHeight": 60, // 整个条目的高度
			"itemMarginTop": 10, // 整个条目距离上面的间距 可以看做不同条目间的间距 
			"itemMarginBottom": 0,  // 整个条目距离下面条目的间距 
			"paddingLeft": 15, //  左侧内容的内间距，即最左侧图标距离最左边的距离
			"paddingTop": 0, // 上间距，可以不进行设置 ，直接用itemHeight 进行条目高度的控制
			"paddingRight": 15, // 最右侧图标距离最右边的间距
			"paddingBottom": 0, // 下间距,可以不进行设置 ，直接用itemHeight 进行条目高度的控制
			"spacingIconWithText": 10, // 左侧图标距离中间文字的间距
			"itemText": "测试", // 文字标题
			"action": "action1", // action 即点击进行的 操作，可以对当前我的界面所有的条目进行列举，用不同字符串控制
			"isLink": "true", // 是否是超链接
			"linkUrl": "https://www.pgyer.com/zhmftest", // 是超链接的话的地址 , 是超链接直接进行跳转，不需要新增action 
			"linkNeedUserId": false // 是否需要在超链接后面 追加userId ,需要追加的话会同步追加 fromSource 
		}

		上面的数据模型列举了几乎所有的可配置选项，视需求而定，简化的配置可以如下(所有的间距由app默认配置)
		{
			"leftIconUrl": "http://192.168.8.244:8080/item1.png",  // 最左侧图片的地址
			"rightIconUrl": "http://192.168.8.244:8080/right_arrow.png",  // 最右侧的箭头图片地址
			"itemText": "测试", // 文字标题
			"action": "action1", // action 即点击进行的 操作，可以对当前我的界面所有的条目进行列举，用不同字符串控制
			"isLink": "true", // 是否是超链接
			"linkUrl": "https://www.pgyer.com/zhmftest", // 是超链接的话的地址 , 是超链接直接进行跳转，不需要新增action 
			"linkNeedUserId": false, // 是否需要在超链接后面 追加userId ,需要追加的话会同步追加 fromSource 
			"isMarginTop": true  // 是否距离上个条目有间距
		}



	

		




