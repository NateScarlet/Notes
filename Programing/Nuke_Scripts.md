Nuke.Scripts
	Tcl
		TCL自身命令
		Nuke内置命令
			expression nuke表达式
			python python代码
			node 节点
返回节点的内部名称
			input 节点d
返回节点的输入节点
			add_channel 通道名称
添加通道
			add_layer 图层名称 通道名称 ...
添加图层 最多8个通道
			layers
列出图层
			knob 调整名 数值
设置调整的数值
			sample 节点 通道 x y 宽度 高度
返回指定像素值
			basename 字符串
返回不带目录的文件名（有后缀）
		节点
			this
命令所在的节点
			input
命令的上一个节点
			parents
父节点（例如所在的组或者root）
			root
整个工程
			group
此节点代表的组
	python
		python自带模块
		nuke模块
			Functions
函数
				scriptName()
返回脚本名
				script_directory()
返回脚本所在目录
				pluginAddPath( 插件路径 )
添加插件目录
				tcl(TCL代码)
				expression(nuke表达式)
				界面
					ask("字符串")
询问
					message("字符串")
小弹窗
					display()
显示窗
					getInput()
文本输入窗口
					getColor()
弹出取色器
					getFilename()
弹出文件浏览器
					getClipName()
弹出序列浏览器
					getFramesAndViews
帧范围和视图选择器
					Panel()
返回面板对象
					面板对象
						show()
					menu
菜单
						menu("菜单名")
返回指定菜单
						菜单对象
							addMenu("菜单名")
添加子菜单
							addCommand("命令名", "命令内容", "快捷键")
添加命令
				Knob
调节
					Array_Knob("调节的名称", "调节的标签")
数值
					WH_Knob("调节的名称", "调节的标签")
滑动条
					Boolean_Knob("调节的名称", "调节的标签")
布尔
					调节对象
						setTooltip('工具提示的内容')
设置工具提示
				execute("节点名", 起始帧, 结束帧, 间隔)
render("节点名", 起始帧, 结束帧, 间隔)
执行输出节点
				executeMultiple((包含多个节点的变量名), ([起始帧, 结束帧, 间隔]))
执行多个输出节点
				undo()
撤销
				frame(帧编号)
跳到指定帧 如果不指定帧编号则返回当前帧
				delete()
删除节点
				center()
				zoom()
				redo()
重做
				Viewer
查看器
					activeViewe()
当前激活的查看器
					查看器对象
						frameControl(i)
播放控制
				FrameRange
帧范围
					FrameRange("帧范围")
单个帧范围
					FrameRanges("帧范围")
多个帧范围
					单个帧范围对象
						setFirst(整数)
设置第一帧
						setLast(整数)
设置最后一帧
						setIncrement(整数)
设置增量
						frist()
返回最后一帧
						last()
返回最后一帧
						increment()
返回增量
						frames()
返回帧数量
						getFrame(索引号)
返回指定索引号帧的帧数
						isInRange(帧号)
返回布尔值:指定帧是否在范围内
						minFrame()
返回其中最小的帧号
						maxFrame()
返回其中最大的帧号
						stepFrame()
返回两帧之间的间隔
					多个帧范围对象
						size()
返回其中帧范围的录像
						add()
添加其他的帧范围到其中
						minFrame()
返回所有帧范围中最小的帧号
						maxFrame()
返回所有帧范围中最大的帧号
						clear()
重置其中的帧范围
						compact()
规范帧范围的表达,移除所有拷贝
						toFrameList()
返回其中的所有帧
						getRange()
返回其中保存的帧范围
				scriptSave(文件名=无)
脚本保存
				scriptSaveAs(文件名=无,覆盖已有文件=-1)
脚本另存为
					参数
						覆盖已有文件
							0
不覆盖
							1
覆盖
							-1
询问用户
				env["属性名"]
返回指定环境属性
				selectAll()
选择所有节点
				toNode("节点名称")
返回指定节点名称的节点(python对象)
				selectedNodes()
返回所有选中的节点列表
				selectedNode()
返回选中的节点(单个,用户正在使用的那个)
				menu( 菜单名 )
返回菜单对象
				selectPattern()
弹出输入对话框, 选择符合输入的节点
				applyPreset(节点名, 预设名)
对当前节点应用预设
				applyUserPreset(节点名, 预设名, [节点])
对当前用户节点应用预设
				createNode("节点名"[,调节名 = 调节的数值, ...])
nodes.节点名()
创建节点
				thisNode()
脚本所在的节点
				numvalue( 调整名, default=无限)
获取调整值(仅数字)
				value()
获取调整值
				Layer()
				Callback
					autolabel()
nuke默认的界面显示函数
			Classes
类
				Knob
调整
					实例方法
						Class()
返回类名称
						__init__(...)
初始化
						__new__(T, S, ...)
类型为T 子类型为S的新对象
						clearAnimated()
清除动画
				Node
节点
					Node["调整名"]
Node调整对象
						value()
返回调整的值
						setAnimated()
设置为带动画的
						setValue("值"[, time = 关键帧时间])
设置值
						animations()
返回动画曲线
						copyAnimations(动画曲线)
从指定动画曲线复制
					实例方法
						Class()
返回节点的类
						__getitem__(x, y)
						__len__(x)
						__new__(T, S, ...)
						__reduce_ex__(...)
						__repr__(x)
						__str__(x)
						addKnob(调节)
添加调节
						allKonbs()
返回所有调整的列表
						autoplace()
自动放置节点,避免重叠
						bbox()
返回节点的边界盒 x, y, w, h 列表
						canSetInput(i, 节点)
是否节点能否被连接至第i个输入
						channels()
返回此节点输出通道的字符串列表
						clones()
返回克隆的数量
						connectInput(i, 节点)

						knobDefault("控制名", "默认值")
设置调节默认值
						numKnobs()
getNumKnobs()
返回调节数量
						knob('调节名')
返回调节
						knobs()
返回所有调节
						name()
返回节点名
						showInfo()

						clones()
克隆数量
						shown()

						showControlPanel()
显示控制面板
						channels()
返回拥有的通道
						metadata(["条目名称", 时间, 视图])
返回元数据中的值
						setName(“名称”, uncollide=True, updateExpressions=False)
设置名称
							参数
								uncollide
解决命名冲突
								updateExpressions 
更新其他节点中的表达式
						showControlPanel()
打开控制面板
						selectOnly()
单个选择
						loadToolset(filename=None, overwrite=-1)
读取工具集
				MenuItem
菜单内容
					实例方法
						setShortcut
					Menu
菜单
						实例方法
							findItem
							addMenu
							name()
				Nodes
各种节点
					例如nuke.nodes.Read
可以后接各种节点名来建立新节点
						例如nuke.nodes.Read(file="filepath\filename.ext")
后面的括号内可以设置创建时的属性
					实例方法
						__new__(T, S, ...)
建立新T子类型S类型的对象
			变量
				EXE_PATH
nuke程序所在路径
				子主题 2
		nukescripts模块
			replaceHashes(字符串)
替换#号
	nuke表达式
		[TCL表达式]
			value 值
			lrange 列表 起始索引 结束索引
切片
			lindex 列表 索引号
索引
			split 字符串 分隔符
分隔
		[python {python表达式}]
		函数
			随机
				random (可选x, 可选y, 可选z)
伪随机[0,1] 随机种子xyz
			通用
				x ()
frame ()
返回当前帧编号
				y (帧编号)
动画曲线在指定帧的值
				true ()
永远返回1
				false ()
永远返回0
				max (x, y, ...)
最大值
				min (x, y, ...)
最小值
				pi ()
圆周率π
				fmod (x, y)
取余
				rint (x)
四舍五入
				int (x)
trunc (x)
舍去小数点后数字
				step (a, x)
x是否不小于a
			颜色
				from_byte (颜色组件)
from_sRGB (颜色组件)
sRGB 转 线性
				to_byte (颜色组件)
to_sRGB (颜色组件)
线性 转 sRGB
				from_rec709 (颜色组件)
rec709 转 线性
				to_rec709 (颜色组件)
线性 转 rec709
			数学
				abs (x)
绝对值
				fabs(x)
浮点数绝对值
				ceil (x)
向上取整
				floor()
向下取整
				clamp (x, 最小值, 最大值)
固定到范围[最小值,最大值]
				clamp (x)
固定到范围[0,1]
				degrees (x)
弧度转角度
				radians (x)
角度转弧度
				exp (x)
自然数e的x次方
				exponent (x)
logb (x)
以2为底x的对数向下取整再加一
				hypot (x, y)
直角边x,y求斜边
				ldexp (x, 指数)
x*2^指数
				log (x)
x的自然对数
				log10 (x)
以10为底x的对数
				pow (x, y)
x的y次方
				pow2 (x)
x的2次方
				mix (a, b, x)
lerp (a, b, x)
f(0)=a,f(1)=b,返回f(x)的值
				smoothstep (a, b, x)
平滑步进 [0,1]的立方插值(平坦)
				sqrt (x)
非负数平方根
			噪波
				mantissa (x)
标准化分数(返回[0.5,1)的值)
				fBm (x, y, z, 周期, 幅度, 增益)
分形布朗运动
				noise (x, 可选y, 可选z)
柏林噪波(范围[-1,1],整数返回0)
				turbulence (x, y, z, 周期, 幅度, 增益)
同fBm除了使用noise()的绝对值
			三角函数
				sin (x)
正弦
				cos (x)
余弦
				tan (x)
正切
				asin (x)
反正弦
				acos (x)
反余弦
				atan (x)
反正切
				atan2 (x,y)
2值反正切(求2向量夹角)
				sinh (x)
双曲正弦
				cosh (x)
双曲余弦
				tanh (x)
双曲正切
			曲线.integrate(第一帧,最后一帧)
积分
Tcl
	TCL自身命令
	Nuke内置命令
		expression nuke表达式
		python python代码
		node 节点
返回节点的内部名称
		input 节点
返回节点的输入节点
		add_channel 通道名称
添加通道
		add_layer 图层名称 通道名称 ...
添加图层 最多8个通道
		layers
列出图层
		knob 调整名 数值
设置调整的数值
		sample 节点 通道 x y 宽度 高度
返回指定像素值
		basename 字符串
返回不带目录的文件名（有后缀）
	节点
		this
命令所在的节点
		input
命令的上一个节点
		parents
父节点（例如所在的组或者root）
		root
整个工程
		group
此节点代表的组
python
	python自带模块
	nuke模块
		Functions
函数
			scriptName()
返回脚本名
			script_directory()
返回脚本所在目录
			pluginAddPath( 插件路径 )
添加插件目录
			tcl(TCL代码)
			expression(nuke表达式)
			界面
				ask("字符串")
询问
				message("字符串")
小弹窗
				display()
显示窗
				getInput()
文本输入窗口
				getColor()
弹出取色器
				getFilename()
弹出文件浏览器
				getClipName()
弹出序列浏览器
				getFramesAndViews
帧范围和视图选择器
				Panel()
返回面板对象
				面板对象
					show()
				menu
菜单
					menu("菜单名")
返回指定菜单
					菜单对象
						addMenu("菜单名")
添加子菜单
						addCommand("命令名", "命令内容", "快捷键")
添加命令
			Knob
调节
				Array_Knob("调节的名称", "调节的标签")
数值
				WH_Knob("调节的名称", "调节的标签")
滑动条
				Boolean_Knob("调节的名称", "调节的标签")
布尔
				调节对象
					setTooltip('工具提示的内容')
设置工具提示
			execute("节点名", 起始帧, 结束帧, 间隔)
render("节点名", 起始帧, 结束帧, 间隔)
执行输出节点
			executeMultiple((包含多个节点的变量名), ([起始帧, 结束帧, 间隔]))
执行多个输出节点
			undo()
撤销
			frame(帧编号)
跳到指定帧 如果不指定帧编号则返回当前帧
			delete()
删除节点
			center()
			zoom()
			redo()
重做
			Viewer
查看器
				activeViewe()
当前激活的查看器
				查看器对象
					frameControl(i)
播放控制
			FrameRange
帧范围
				FrameRange("帧范围")
单个帧范围
				FrameRanges("帧范围")
多个帧范围
				单个帧范围对象
					setFirst(整数)
设置第一帧
					setLast(整数)
设置最后一帧
					setIncrement(整数)
设置增量
					frist()
返回最后一帧
					last()
返回最后一帧
					increment()
返回增量
					frames()
返回帧数量
					getFrame(索引号)
返回指定索引号帧的帧数
					isInRange(帧号)
返回布尔值:指定帧是否在范围内
					minFrame()
返回其中最小的帧号
					maxFrame()
返回其中最大的帧号
					stepFrame()
返回两帧之间的间隔
				多个帧范围对象
					size()
返回其中帧范围的录像
					add()
添加其他的帧范围到其中
					minFrame()
返回所有帧范围中最小的帧号
					maxFrame()
返回所有帧范围中最大的帧号
					clear()
重置其中的帧范围
					compact()
规范帧范围的表达,移除所有拷贝
					toFrameList()
返回其中的所有帧
					getRange()
返回其中保存的帧范围
			scriptSave(文件名=无)
脚本保存
			scriptSaveAs(文件名=无,覆盖已有文件=-1)
脚本另存为
				参数
					覆盖已有文件
						0
不覆盖
						1
覆盖
						-1
询问用户
			env["属性名"]
返回指定环境属性
			selectAll()
选择所有节点
			toNode("节点名称")
返回指定节点名称的节点(python对象)
			selectedNodes()
返回所有选中的节点列表
			selectedNode()
返回选中的节点(单个,用户正在使用的那个)
			menu( 菜单名 )
返回菜单对象
			selectPattern()
弹出输入对话框, 选择符合输入的节点
			applyPreset(节点名, 预设名)
对当前节点应用预设
			applyUserPreset(节点名, 预设名, [节点])
对当前用户节点应用预设
			createNode("节点名"[,调节名 = 调节的数值, ...])
nodes.节点名()
创建节点
			thisNode()
脚本所在的节点
			numvalue( 调整名, default=无限)
获取调整值(仅数字)
			value()
获取调整值
			Layer()
			Callback
				autolabel()
nuke默认的界面显示函数
		Classes
类
			Knob
调整
				实例方法
					Class()
返回类名称
					__init__(...)
初始化
					__new__(T, S, ...)
类型为T 子类型为S的新对象
					clearAnimated()
清除动画
			Node
节点
				Node["调整名"]
Node调整对象
					value()
返回调整的值
					setAnimated()
设置为带动画的
					setValue("值"[, time = 关键帧时间])
设置值
					animations()
返回动画曲线
					copyAnimations(动画曲线)
从指定动画曲线复制
				实例方法
					Class()
返回节点的类
					__getitem__(x, y)
					__len__(x)
					__new__(T, S, ...)
					__reduce_ex__(...)
					__repr__(x)
					__str__(x)
					addKnob(调节)
添加调节
					allKonbs()
返回所有调整的列表
					autoplace()
自动放置节点,避免重叠
					bbox()
返回节点的边界盒 x, y, w, h 列表
					canSetInput(i, 节点)
是否节点能否被连接至第i个输入
					channels()
返回此节点输出通道的字符串列表
					clones()
返回克隆的数量
					connectInput(i, 节点)

					knobDefault("控制名", "默认值")
设置调节默认值
					numKnobs()
getNumKnobs()
返回调节数量
					knob('调节名')
返回调节
					knobs()
返回所有调节
					name()
返回节点名
					showInfo()

					clones()
克隆数量
					shown()

					showControlPanel()
显示控制面板
					channels()
返回拥有的通道
					metadata(["条目名称", 时间, 视图])
返回元数据中的值
					setName(“名称”, uncollide=True, updateExpressions=False)
设置名称
						参数
							uncollide
解决命名冲突
							updateExpressions 
更新其他节点中的表达式
					showControlPanel()
打开控制面板
					selectOnly()
单个选择
					loadToolset(filename=None, overwrite=-1)
读取工具集
			MenuItem
菜单内容
				实例方法
					setShortcut
				Menu
菜单
					实例方法
						findItem
						addMenu
						name()
			Nodes
各种节点
				例如nuke.nodes.Read
可以后接各种节点名来建立新节点
					例如nuke.nodes.Read(file="filepath\filename.ext")
后面的括号内可以设置创建时的属性
				实例方法
					__new__(T, S, ...)
建立新T子类型S类型的对象
		变量
			EXE_PATH
nuke程序所在路径
			子主题 2
	nukescripts模块
		replaceHashes(字符串)
替换#号
nuke表达式
	[TCL表达式]
		value 值
		lrange 列表 起始索引 结束索引
切片
		lindex 列表 索引号
索引
		split 字符串 分隔符
分隔
	[python {python表达式}]
	函数
		随机
			random (可选x, 可选y, 可选z)
伪随机[0,1] 随机种子xyz
		通用
			x ()
frame ()
返回当前帧编号
			y (帧编号)
动画曲线在指定帧的值
			true ()
永远返回1
			false ()
永远返回0
			max (x, y, ...)
最大值
			min (x, y, ...)
最小值
			pi ()
圆周率π
			fmod (x, y)
取余
			rint (x)
四舍五入
			int (x)
trunc (x)
舍去小数点后数字
			step (a, x)
x是否不小于a
		颜色
			from_byte (颜色组件)
from_sRGB (颜色组件)
sRGB 转 线性
			to_byte (颜色组件)
to_sRGB (颜色组件)
线性 转 sRGB
			from_rec709 (颜色组件)
rec709 转 线性
			to_rec709 (颜色组件)
线性 转 rec709
		数学
			abs (x)
绝对值
			fabs(x)
浮点数绝对值
			ceil (x)
向上取整
			floor()
向下取整
			clamp (x, 最小值, 最大值)
固定到范围[最小值,最大值]
			clamp (x)
固定到范围[0,1]
			degrees (x)
弧度转角度
			radians (x)
角度转弧度
			exp (x)
自然数e的x次方
			exponent (x)
logb (x)
以2为底x的对数向下取整再加一
			hypot (x, y)
直角边x,y求斜边
			ldexp (x, 指数)
x*2^指数
			log (x)
x的自然对数
			log10 (x)
以10为底x的对数
			pow (x, y)
x的y次方
			pow2 (x)
x的2次方
			mix (a, b, x)
lerp (a, b, x)
f(0)=a,f(1)=b,返回f(x)的值
			smoothstep (a, b, x)
平滑步进 [0,1]的立方插值(平坦)
			sqrt (x)
非负数平方根
		噪波
			mantissa (x)
标准化分数(返回[0.5,1)的值)
			fBm (x, y, z, 周期, 幅度, 增益)
分形布朗运动
			noise (x, 可选y, 可选z)
柏林噪波(范围[-1,1],整数返回0)
			turbulence (x, y, z, 周期, 幅度, 增益)
同fBm除了使用noise()的绝对值
		三角函数
			sin (x)
正弦
			cos (x)
余弦
			tan (x)
正切
			asin (x)
反正弦
			acos (x)
反余弦
			atan (x)
反正切
			atan2 (x,y)
2值反正切(求2向量夹角)
			sinh (x)
双曲正弦
			cosh (x)
双曲余弦
			tanh (x)
双曲正切
		曲线.integrate(第一帧,最后一帧)
积分