```
- 关于Lua脚本 - 

脚本控制，脚本文件（*。Anm，* .Obj，*。Scn，* .Cam），
脚本可用于文本脚本控制字符
您可以使用Lua语言。此外，一些变量和功能已经扩展。


 - 变量 - 

    目标对象的信息放在以下变量中。

    obj.ox：参考坐标的相对坐标X.
    obj.oy：Y相对于参考坐标
    obj.oz：参考坐标的相对坐标Z.
    obj.rx：X轴旋转角度（360.0处旋转一次）
    obj.ry：Y轴旋转角度（一次旋转360.0）
    obj.rz：Z轴旋转角度（360.0旋转一圈）
    obj.cx：中心的相对坐标X.
    obj.cy：中心的相对坐标Y.
    obj.cz：中心的相对坐标Z.
    obj.zoom：放大率（1.0 =相等放大率）
    obj.alpha：不透明度（0.0到1.0 / 0.0 =透明度/ 1.0 =不透明）
    obj.aspect：宽高比（-1.0到1.0 /加/横向减少/减去垂直减少）
    obj.x：显示参考坐标X（ReadOnly）
    obj.y：显示参考坐标Y（ReadOnly）
    obj.z：显示参考坐标Z（ReadOnly）
    obj.w：图像大小W（ReadOnly）
    obj.h：图像大小H（ReadOnly）
    obj.screen_w：屏幕尺寸W（ReadOnly）
    obj.screen_h：屏幕尺寸H（ReadOnly）
    obj.framerate：帧率（ReadOnly）
    obj.frame：基于对象的当前帧号（ReadOnly）
    obj.time：基于对象的当前时间（秒）（ReadOnly）
    obj.totalframe：对象的总帧数（ReadOnly）
    obj.totaltime：对象的总时间（秒）（ReadOnly）
    obj.layer：放置对象的层（ReadOnly）
    obj.index：多个对象的数量（ReadOnly）※对于单个对象
    obj.num：多个对象的数量（1 =单个对象/ 0 =未定义）（ReadOnly）*对于单个对象
    obj.track0：跟踪栏0值（ReadOnly）*仅在脚本文件中可用
    obj.track1：跟踪栏1值（ReadOnly）*仅在脚本文件中可用
    obj.track2：跟踪栏2值（ReadOnly）*仅在脚本文件中可用
    obj.track3：跟踪栏3值（ReadOnly）*仅在脚本文件中可用
    obj.check0：复选框值（ReadOnly）*仅在脚本文件中可用


    - 注意事项 - 

    ○请使用obj.time而不是obj.frame来支持运动模糊。
    ○由于像素系统的功能对整个物体进行点处理，因此不适合实际使用。
    ○转义SJIS 2字节字符0x5c后执行脚本。
    ○脚本控制，文本对象中脚本的Unicode字符转换为Unicode标记（＆＃????;）。
    ○可以处理的脚本的最大大小约为32 KB。如果不止于此，请使用dofile（）等。
    ○如果从脚本调用脚本可能效果不佳。


    - 功能 - 

    添加了以下功能。

    ○obj.mes（文字）
    在文本对象中添加指定的文本。
    它只能在文本对象的文本中使用。
    ※你可以省略obj。并且只使用mes（）。
    text：指定要显示的文本。
    示例：obj.mes（“插入并显示此字符”）

    ○obj.effect（[name，param1，value1，param2，value2，...]）
    执行指定的过滤效果。只能使用媒体对象。
    在不带参数的情况下调用时，执行脚本后的过滤器效果。
    name：指定效果的名称。
    param1：指定效果参数的名称。
    value1：指定效果参数的值。
    您可以根据需要指定param？和value？的多个组合。
    ※param，轨道栏以外的设置值，复选框
    它是通过导出目​​标文件等输出的名称和值。
    ※请参阅输出中的名称，如名称更改的轨迹栏的导出。
    *在位移图的形状规格中将“type”设置为0，将“name”设置为“* tempbuffer”
    如果指定，则将tempbuffer读取为形状。
    示例：obj.effect（“色调校正”，“亮度”，150，“色调”，180）

    ○obj.draw（[ox，oy，zoom，alpha，rx，ry，rz]）
    绘制当前对象。只能使用媒体对象。
    通常在没有做任何事情的情况下最后绘制，但是使用obj.draw（）
    您可以多次绘制对象。
    ※如果使用obj.draw（），则不会执行脚本后的过滤效果。
    ※您可以通过调用没有参数的obj.effect（）来预先在脚本之后执行过滤效果。
    ox：相对坐标X.
    oy：相对坐标Y.
    oz：相对坐标Z.
    zoom：放大倍率（1.0 =相等放大倍率）
    alpha：不透明度（0.0 =透明度/ 1.0 =不透明度）
    rx：X轴旋转角度（360.0处旋转一次）
    ry：Y轴旋转角度（360.0旋转一圈）
    rz：Z轴旋转角度（360.0旋转一圈）
    示例：obj.draw（2,10,0）

    ○obj.drawpoly（x0，y0，z0，x1，x1，y1，z1，x2，y2，z2，x3，y3，z3 [，u0，v0，u1，v1，u2，v2，u3，v3，alpha]）
    使用任意矩形绘制当前对象的任何部分。只能使用媒体对象。
    ※除内角为180度以下的所有平面外，未正确绘制。
    ※顶点0到3顺时针转动的表面是表面。
    ※如果使用obj.drawpoly（），则不会执行脚本后的过滤效果。
    x0，y0，z0：正方形的顶点0的坐标
    x1，y1，z1：正方形的顶点1的坐标
    x2，y2，z2：正方形的顶点2的坐标
    x3，y3，z3：正方形的顶点3的坐标
    u0，v0：与顶点0对应的对象图像的坐标
    u1，v1：与顶点1对应的对象图像的坐标
    u2，v2：与顶点2对应的对象图像的坐标
    u3，v3：与顶点3对应的对象图像的坐标
    示例：obj.drawpoly（-50，-50,0,50，-50,0,50,50,50，-50,50,0,0,0，obj.w，0，obj.w，obj。 h，0，obj.h）

    ○obj.load（[type]，...）
    加载当前对象的图像。
    如果省略type，将自动确定。
    ※已经读取的图像将被丢弃。

    动画电影文件
    obj.load（“movie”，file [，time，flag]）
    从视频文件加载指定时间的图像。
    file：电影文件名
    time：要显示的图像的时间（秒）（默认为对象的当前时间）
    flag：0 =没有alpha / 1 = alpha
    返回值：视频总时间（秒）
    示例：obj.load（“movie”，“c：\\ test.avi”）
    ◇图像文件
    obj.load（“image”，file）
    加载图像文件。
    file：图像文件名
    示例：obj.load（“image”，“c：\\ test.bmp”）
    ◇文字
    obj.load（“text”，text [，speed，time]）
    阅读文字
    您可以使用颜色，大小和字体控制字符。
    您可以通过设置速度和时间来更改显示的字符数。
    ※不能用于文本对象。
    text：要阅读的文字
    speed：time参数的一秒钟内显示的字符数
    time：速度参数的经过时间
    示例：obj.load（“text”，“此字符将作为图像加载”）
    ◇图
    加载形状。
    obj.load（“figure”，name [，color，size，line]）
    名称：形状名称
    颜色：颜色（0x000000到0xffffff）
    尺寸：形状大小
    line：线宽的形状
    示例：obj.load（“figure”，“circle”，0xffffff，100）
    フレーム帧缓冲区
    从帧缓冲区读取。
    load（“framebuffer”[，x，y，w，h]）
    x，y，w，h：从帧缓冲区获取的范围（默认为全部）
    仮想虚拟缓冲区
    从虚拟缓冲区读取。
    ※可以使用obj.copybuffer（）和obj.setoption（）创建虚拟缓冲区。
    load（“tempbuffer”[，x，y，w，h]）
    x，y，w，h：从虚拟缓冲区获取的范围（默认为全部）
    オブジェクト图层上的对象
    在指定图层上加载对象。
    obj.load（“layer”，no [，effect]）
    no：图层编号（1到）
    效果：执行附加效果（true = enable / false <default> = not）
    直前上一个对象
    加载上一个对象。
    obj.load（“之前”）;
    它只能在加载自定义对象中的其他对象之前使用。

    ○obj.setfont（name，size [，type，col1，col2]）
    指定obj.load（）文本中使用的字体。
    ※您需要指定脚本的每次调用。
    名称：字体名称
    大小：字体大小
    类型：字符装饰（0到4）
    0 =正常字符/ 1 =阴影字符/ 2 =阴影字符（薄）
    3 =边框字母/ 4 =边框字母（薄）
    col1：字符颜色（0x000000到0xffffff）
    col2：阴影和边缘的颜色（0x000000-0xffffff）

    ○obj.rand（st_num，ed_num [，seed，frame]）
    生成随机数。与普通随机数不同，在同一时间范围内
    生成随机数，以便始终显示相同的值。
    ※你可以省略obj。并且只使用rand（）。
    st_num：随机数的最小值
    ed_num：随机数的最大值
    种子：随机数种子（默认是每个对象的不同随机数）
    指定正值会导致每个对象的随机数不同，即使物种相同
    如果物种相同，则负值会导致所有对象具有相同的随机性）
    frame：帧号（默认为当前帧）
    示例：obj.rand（10,20）

○obj.setoption（名称，值）
为当前对象设置各种选项。
※您需要指定脚本的每次调用。
name：选项名称
值：选项值

◇不要显示背面
obj.setoption（“剔除”，值）
值：0 =显示/ 1 =隐藏

向く指向相机的方向
obj.setoption（“billboard”，value）
值：0 =不进行/ 1 =仅在水平方向/ 2 =仅在垂直方向/ 3 =对向

対象阴影的对象
obj.setoption（“shadow”，value）
值：0 =不适用/ 1 =适用

◇抗锯齿
obj.setoption（“antialias”，value）
值：0 =不/ 1 =做

合成复合模式
obj.setoption（“blend”，value [，option]）
值：0 =正常/ 1 =加法/ 2 =减法/ 3 =乘法/ 4 =屏幕
5 =叠加/ 6 =比较（亮）/ 7 =比较（暗）/ 8 =亮度/ 9 =色差
以下是专用于虚拟缓冲区的合成模式。
“alpha_add”=颜色信息是加权平均值，并添加了alpha值
“alpha_max”=颜色信息是加权平均值，alpha值更大
“alpha_sub”=从alpha值中减去颜色信息，而不做任何事情
“alpha_add2”=叠加颜色信息并添加alpha值
选项：“强制”=强制规范模式
仅当原始合成模式正常时才反映用于绘制到帧缓冲区的合成模式。
指定“强制”选项以反映原件不正常的情况。

将绘图目标更改为虚拟缓冲区
obj.setoption（“drawtarget”，“tempbuffer”[，w，h]）
w，h：虚拟缓冲区的大小（默认不初始化）
如果绘图目标是虚拟缓冲区，则使用obj.draw（）和obj.drawpoly（）进行绘制
它是为虚拟缓冲区完成的。在这种情况下，对象具有
不反映坐标等设置，并按原样绘制参数的坐标。
指定大小会以透明颜色初始化虚拟缓冲区。
虚拟缓冲区由所有对象共享。

◇将绘图目标更改为帧缓冲区
obj.setoption（“drawtarget”，“framebuffer”）
将obj.draw（）和obj.drawpoly（）的绘图目标设置为帧缓冲区。
不通过draw（）等对帧缓冲区进行绘制时
完成脚本后自动完成而不用setoption（）更改它
它将绘制到帧缓冲区。

変更改脚本中帧缓冲区中绘图的状态
obj.setoption（“draw_state”，flag）
flag：true = draw / false =未绘制

フォーカス物体对焦框模式
obj.setoption（“focus_mode”，value）
value：“fixed_size”=设置固定大小的帧

◇设置摄像机参数
设置各种摄像机参数。
相机处于编辑模式时不会反映出来。
※只能使用相机效果，脚本（相机控制）
obj.setoption（“camera_param”，cam）
cam：相机参数（表格）
.x：相机坐标X.
.y：相机坐标Y.
.z：相机坐标Z.
.tx：摄像机的目标坐标X.
.ty：摄像机的目标坐标Y.
.tz：相机的目标坐标Z.
.rz：相机倾斜
.ux：摄像机的向上方向单位矢量X.
.uy：摄像机的向上方向单位矢量Y.
.uz：摄像机的上方向单位矢量Z.
.d：相机到屏幕的距离（焦距）
示例：cam = obj.getoption（“camera_param”）;

○obj.getoption（名称，...）
获取当前对象的各种选项。
name：选项名称

移动轨迹栏的移动模式
obj.getoption（“track_mode”，value）
值：跟踪条形码
返回值：0 =无/ 1 =直线/ 2 =曲线/ 3 =瞬时/ 4 =中点
5 =移动量/ 6 =随机/ 7 =加速/减速/ 8 =重复
数对象的段数
obj.getoption（“section_num”）
返回值：间隔数（中点数+ 1）

◇获取脚本名称
obj.getoption（“script_name”[，value] [，skip]）
value：滤镜效果的顶部和底部的相对位置（0表示我/减号/向上/加号表示底部）
skip：跳过禁用的滤镜效果（true =启用/ false <默认> =不）
返回值：脚本名称（如果目标不是脚本，则为空）
示例：如果obj.getoption（“script_name”）== obj.getoption（“script_name”， -  1）则
※您无法获取默认包含的脚本名称

调べる检查GUI的显示状态
obj.getoption（“gui”）
返回值：true =显示/ false =隐藏
※视频输出期间将被隐藏。

◇获取摄像机控制状态
obj.getoption（“camera_mode”）
返回值：0 =不受摄像机控制/ 0以外=由摄像机控制

◇获取摄像头参数
obj.getoption（“camera_param”）
返回值：摄像机参数（表格）
※表格的内容与obj.setoption（“camera_param”）相同。
示例：cam = obj.getoption（“camera_param”）;

调べる检查各个对象是否有效
obj.getoption（“multi_object”）
返回值：true =有效/ false =无效

○obj.getvalue（目标[，时间，部分]）
获取当前对象的设置。
target：设置类型
0 =轨迹栏0的值
1 =轨迹栏1的值
2 =轨迹栏2的值
3 =轨迹栏3的值
“x”=参考坐标X.
“y”=参考坐标Y.
“z”=参考坐标Z.
“rx”=参考X轴旋转角度
“ry”=标准Y轴旋转角度
“rz”=参考Z轴旋转角度
“缩放”=标准放大率（100 =相等放大率）※请注意，这与obj.zoom（1.0 =等倍）不同
“alpha”=标准不透明度（0.0到1.0 / 0.0 =透明/ 1.0 =不透明）
“aspect”=标准纵横比（-1.0到1.0 /加=水平减少/负垂直减少）
“时间”=基于对象的时间
“layer7.x”=第7层对象的参考坐标X.
※您可以在图层[图层编号]中获取另一图层的对象的值。[设置类型]
“scenechange”=场景变化时的显示比例（0.0到1.0）只有场景变化可用
※请参考场景变更脚本的例子
time：获取时间点值的时间（秒）（默认为当前时间）
section：作为时间参考的节号（默认为起点）
0 =起点/ 1 =第一中点/ 2 =第二中点/ -1 =终点
※不反映目标对象的时间控制。

○obj.setanchor（name，num [，option，..]）
显示锚点。
调用此功能时显示定位点的设置
当锚移动时反映变量。
每次通话最多可调用此功能8次。
如果更改了呼叫顺序或号码，则可能无法正确反映。
name：指定存储--dialog中指定的坐标的变量名称。 ※指定变量名称作为字符串
指定“track”时，将引用从--track0指定的轨迹栏的起点和终点中点的值。
※如果直接指定表变量名，则只显示没有锚显示或移动的行。
num：指定锚点数。您可以为所有锚点指定最多16个。
如果name =“track”，请指定0。锚点的数量是起点和终点中点的数量。
选项：可以列出各种选项。
“line”=用一条线连接锚点。
“loop”=用一条线连接锚点。
“star”=分别将锚点与对象的中心连接。
“arm”=将锚点连接到对象的中心。
“color”=更改上述选项的线条颜色。为后续参数指定颜色（0x000000到0xffffff）。
“inout”=显示上述选项行显示为IN和OUT侧。 （锚的数量将是一半）
“xyz”=用3D坐标控制锚点。 ※默认为2D坐标
※使用相机控制+阴影时，预览中的阴影可能会略微偏移。
返回值：获取的锚点数
示例：obj.setanchor（“pos”，3）
n = obj.setanchor（“track”，0，“line”）

○obj.getaudio（buf，文件，类型，大小）
从音频文件中获取音频数据。
获取相对于对象时间的位置数据。
buf：指定表以接收数据。
※如果指定nil，则表格将返回第3个返回值。
file：音频文件名（如果指定了“audiobuffer”，则可以获取正在编辑的音频数据）
type：采集数据的类型
“pcm”= PCM采样数据（16位单声道）
“频谱”=每个频率的音量数据
“傅立叶”=通过语音的离散傅立叶变换获得的数据（不需要指定大小）
※从1/2048到原始频率的1/2变成1/2048步的1024个数据（可能...
size：要获取的数据数量（可能小于指定值）
返回值：采集数据的数量，采样率
示例：n = obj.getaudio（buf，“audiobuffer”，“spectrum”，32）
n，rate = obj.getaudio（buf，“c：\\ test.wav”，“pcm”，1000）
n，rate，buf = obj.getaudio（nil，“c：\\ test.wav”，“pcm”，1000）

○obj.filter（name [，param1，value1，param2，value2，...]）
在指定的屏幕上执行过滤器（过滤器对象）。
只能使用高级编辑插件添加的过滤器。
参数说明方法与obj.effect（）相同。
根据过滤器的不同，可能无法正确使用。
※可能会破坏对象的图像数据。
示例：obj.filter（“色调校正”，“亮度”，150，“色调”，180）

○obj.copybuffer（dst，src）
复制图像缓冲区
*复制目标图像缓冲区的大小更改为复制源的大小。
dst：复制目标缓冲区
“tmp”=虚拟缓冲区
“obj”=对象
“cache：xxxx”=缓存缓冲区（xxxx是任何名称）
src：复制源缓冲区
“frm”=帧缓冲区
“obj”=对象
“tmp”=虚拟缓冲区
“cache：xxxx”=缓存缓冲区（xxxx是任何名称）
“image：xxxx”=图像文件（xxxx是相对于脚本文件夹的图像文件名）
返回值：true =成功/错误=失败
※可以使用dst和src的组合。
“obj”<=“tmp”
“obj”<=“frm”
“obj”<=“cache：xxxx”
“obj”<=“image：xxxx”
“tmp”<=“obj”
“tmp”<=“frm”
“tmp”<=“cache：xxxx”
“tmp”<=“image：xxxx”
“cache：xxxx”<=“obj”
“cache：xxxx”<=“tmp”
缓存缓冲区名称对所有对象都是通用的。
因为缓存缓冲区和虚拟缓冲区是从图像数据缓存中保护的
如果从高速缓存号中读取其他图像等，则可以丢弃它们。
※在小图像等的情况下，区域的总和成为最大图像尺寸的一个缓存。
※如果使用缓存，则完成脚本的每次调用都会更安全。

○obj.getpixel（x，y [，type]）
获取当前对象的像素信息。
在不带参数的情况下调用时，可以获取对象的像素数。
※像素数可能与obj.w和obj.h不同。 （有很多事情很难理解......）
x，y：要获得的像素的坐标
type：像素信息的类型（“col”，“rgb”，“yc”）
*省略时，obj.pixeloption（“type”）指定的类型（通常为“col”）
返回值：如果类型为“col”
颜色信息（0x000000至0xffffff）和不透明度（0.0 =透明/ 1.0 =不透明）
col，a = obj.getpixel（0,0，“col”）
如果类型是“rgb”
每8位（0到255）的RGBA信息
r，g，b，a = obj.getpixel（0,0，“rgb”）
如果类型是“yc”
YCbCr内部格式
y，cb，cr，a = obj.getpixel（0,0，“yc”）
没有争论
水平和垂直像素数
w，h = obj.getpixel（）

○obj.putpixel（x，y，...）
重写当前对象的像素信息。
在不带参数的情况下调用时，可以获取对象的像素数。
要传递的像素信息的类型将是obj.pixeloption（“type”）指定的类型。
x，y：要重写的像素的坐标
颜色信息：当类型为“col”时
颜色信息（0x000000至0xffffff）和不透明度（0.0 =透明/ 1.0 =不透明）
obj.putpixel（0,0，col，a）
如果类型是“rgb”
每8位（0到255）的RGBA信息
obj.putpixel（0,0，r，g，b，a）
如果类型是“yc”
YCbCr内部格式
obj.putpixel（0,0，y，cb，cr，a）

○obj.copypixel（dst_x，dst_y，src_x，src_y）
复制当前对象的像素信息。
dst_x，dst_y：复制目标的坐标
src_x，src_y：复制源的坐标

○obj.pixeloption（名称，值）
设置obj.getpixel（），obj.putpixel（），obj.copypixel（）的处理选项。
※您需要指定脚本的每次调用。
name：选项名称
值：选项值

指定指定像素信息类型
obj.pixeloption（“type”，value）
值：“col”/“rgb”/“yc”

◇指定像素信息的读出目的地
obj.pixeloption（“get”，value）
值：“obj”= object /“frm”=帧缓冲区（无alpha值）

指定指定像素信息的目的地
obj.pixeloption（“put”，value）
值：“obj”= object /“frm”=帧缓冲区（无alpha值）

指定在写入时指定混合类型
obj.pixeloption（“blend”，value）
value：无参数= Replace / 0 = Normal / 1 = Add / 2 = Subtract / 3 = Multiplication / 4 = Screen
5 =叠加/ 6 =比较（亮）/ 7 =比较（暗）/ 8 =亮度/ 9 =色差

○obj.getpixeldata（[option，...]）
读出当前对象的图像数据。
此功能用于使用DLL进行图像处理。
图像数据以当前对象图像的分辨率以RGBA（32位）格式存储。
通过使用draw（）和effect（）等绘图处理函数可以获得图像数据的内容
它将被破坏，因此请将其复制到另一个区域并在必要时进行处理。
选项：可以列出各种选项。
“work”=获取指向与图像大小相同的工作缓冲区的指针。
“alloc”=分配内存（完整用户数据）并存储它
返回值：数据指针（用户数据），水平和垂直像素数
示例：data，w，h = obj.getpixeldata（）
work = obj.getpixeldata（“work”）

○obj.putpixeldata（数据）
将图像数据写入当前对象。
此功能用于使用DLL进行图像处理。
可以使用getpixeldata（）获取的相同图像数据格式
写入当前对象。图像数据的分辨率是
它必须与对象相同。
data：指向图像数据的指针（用户数据）
示例：obj.putpixeldata（data）

○obj.getpoint（target [，option]）
获取跟踪栏值。

target：integer =每个部分中的跟踪栏值
0 =起点/ 1 =第一中间点/ 2 = 2秒中间点/ ......
您可以使用选项指定要获取的相关轨道的相对位置。
“index”=获取当前部分的位置。
如果它在起始点和第一个中点之间，则由一个小数字表示，例如0.5。
“num”=获取起点和终点航点的总数。
“time”=获取当前时间。
您可以使用选项指定获取时间的间隔。
“acceleration”=获取是否设置了加速度。
返回值：true =有效/ false =无效
“减速”=获取是否设定减速度。
返回值：true =有效/ false =无效
“param”=获取跟踪栏设置。
“link”=获取索引和相关曲目的总数。
index，num = obj.getpoint（“link”）
相关轨迹用于通过坐标等获取另一轨道的值。
X坐标返回值：0,3 / Y坐标返回值：1,3 / Z坐标返回值：2,3

○obj.getinfo（name，...）
获取各种环境信息。
name：要获取的信息的名称

取获获取脚本文件夹路径
obj.getinfo（“script_path”）
返回值：脚本文件夹路径

调べる检查视频是否正在输出
obj.getinfo（“保存”）
返回值：true =输出/ false =不输出

取得获取最大图像尺寸
max_x，max_y = obj.getinfo（“image_max”）
返回值：最大图像尺寸（水平宽度，高度）

○obj。插值（时间，x0，y0，z0，x1，y1，z1，x2，y2，z2，x3，y3，z3）
从连续点p0（x0，y0，z0），p1（x1，y1，z1），p2（x2，y2，z2），p3（x3，y3，z3）
根据时间（0到1）计算p1和p2之间的坐标。
※y，z坐标可以省略。
示例：x，y，z = obj。插值（时间，x0，y0，z0，x1，x1，y1，x1，y2，x2，z2，x3，y3，z3）
x，y = obj。插值（时间，x0，y0，x1，y1，x2，y2，x3，y3）

○RGB（r，g，b）
颜色信息（0x000000至0xffffff）和红色（0至255），绿色（0至255）和蓝色（0至255）元素相互转换。
当指定两个r，g和b时，颜色根据物体的时间流逝而改变。
示例：col = RGB（r，g，b）
r，g，b = RGB（col）
col = RGB（r1，g1，b1，r2，g2，b2）

○HSV（h，s，v）
颜色信息（0x000000至0xffffff）和色调（0至360），饱和度（0至100）和亮度（0至100）相互转换。
当指定两个h，s和v时，颜色根据对象的时间流逝而变化。
示例：col = HSV（h，s，v）
h，s，v = HSV（col）
col = HSV（h1，s1，v1，h2，s2，v2）

○OR（a，b）/ AND（a，b）/ XOR（a，b）
执行OR，AND，XOR的位操作。
示例：c = OR（a，b）

○SHIFT（a，班次）
执行算术移位。如果shift是正数，则它是左移，如果是负，则是右移。
示例：b = SHIFT（a，1）

○debug_print（文本）
将指定的字符发送到OutputDebugString（）。用于调试。
※脚本执行错误消息自动设置为OutputDebugString（）
它应该被发送。
text：调试显示字符
示例：debug_print（“debug display”）


 - 使用示例 - 

○在文本中使用脚本的示例
以下文本显示对象时间计数器：

当前对象时间= <？Mes（string.format（“％02d：％02d。％02d”，obj.time / 60，obj.time％60，（obj.time * 100）％100））？>

○随时间改变对象的坐标和角度的示例
以下脚本随着时间的推移向右旋转。

obj.ox = obj.ox + obj.time * 10
obj.rz = obj.rz + obj.time * 360

○将滤镜效果应用于对象的示例
使用以下脚本随时间变暗和变暗。

i = math.cos（obj.time * math.pi * 2）* 50
obj.effect（“色调校正”，“亮度”，100 + i）

○绘制多个对象的示例
以下脚本在一个圆圈中绘制10个对象。

		n = 10
		l = obj.w*2
		for i=0,n do
		  r = 360*i/n
		  x = math.sin(r*math.pi/180)*l
		  y = -math.cos(r*math.pi/180)*l
		  obj.draw(x,y,0,1,1,0,0,r)
		end

○在脚本文件中使用跟踪栏和复选框值的示例
' -  Track0：脚本文件开头的名称，最小值，最大值，默认值，移动单位'（* .anm，*。Obj，*。Scn，* .Cam）
指定时，轨道栏将启用，如下所示。移动单元可以缩写为“1”，“0.1”或“0.01”。
最多可使用4个轨道条。 ※现场更换最多两个。
指定“--check0：Name，默认值（0或1）”将启用该复选框。

--track0：X速度，-10,10,0
--track1：Y速度，-10,10,0,1
--check0：gravity，0
obj.ox = obj.ox + obj.track0 * obj.time
obj.oy = obj.oy + obj.track1 * obj.time
if（obj.check0）然后
obj.oy = obj.oy + obj.time * obj.time
结束

○在脚本文件中使用参数设置的示例
如果在脚本文件的开头指定“--param：default setting”（* .anm，* .obj，* .scn，* .cam）
参数设置项生效。最多255个字节。
※您不能在--color， -  file或--dialog的同时指定此选项。

--param：dx = 10; dy = 20;
obj.ox = obj.ox + dx * obj.time
obj.oy = obj.oy + dy * obj.time

○在脚本文件中使用颜色选择对话框的示例
如果在脚本文件的开头指定' -  color：default setting'（* .anm，* .obj，* .scn，* .cam）
颜色选择对话框中的项目变为有效。
指定的颜色存储在变量（颜色）中
※您不能在--color， -  file或--dialog的同时指定此选项。

--color：0xffffff
obj.load（“图”，“矩形”，颜色，100）

○在脚本文件中使用文件选择对话框的示例
如果在脚本文件的开头指定'--file：'（* .anm，* .obj，* .scn，* .cam）
文件选择对话框中的项目有效。
指定的文件存储在变量（文件）中
※您不能在--color， -  file或--dialog的同时指定此选项。

--file：
obj.load（文件）

○在脚本文件中使用值输入对话框的示例
如果在脚本文件的开头指定'--dialog：display name，variable name = initial value;'（* .anm，* .obj，* .scn，* .cam）
值输入对话框中的项目有效。最多可指定16个项目。
如果显示名称以'/ chk'，'/ col'或'/ fig'结尾，则会添加一个复选框或颜色或形状选择按钮。
每个复选框和选择按钮最多可以指定4个项目。
※您不能在--color， -  file或--dialog的同时指定此选项。

--dialog：X offset，x = 100; Y offset，y = 100;
obj.ox = obj.ox + x
obj.oy = obj.oy + y

--dialog：size，size = 100; color / col，col = 0xffffff; shape / fig，fig =“square”
obj.load（“图”，图，col，大小）

○在一个文件中注册多个动画效果和自定义对象的示例
使用'@'启动脚本文件的文件名（* .anm，*。Obj，*。Scn，*。Cam）
如果在每个脚本的开头定义“@name”，如下所示
您可以一起定义多个脚本。
※exedit.anm，exedit.obj脚本也是这种格式。

ファイル注册多个文件时的文件内容[@multiple registration example.Anm]
@样本1
--track0：速度，-10,10,10
obj.ox = obj.ox + obj.track0 * obj.time
@样本2
--track0：速度，-10,10,10
obj.oy = obj.oy + obj.track0 * obj.time

内容单注册的文件内容[单注册示例.Anm]
--track0：速度，-10,10,10
obj.ox = obj.ox + obj.track0 * obj.time

○场景变更脚本的示例
随着时间的推移交叉淡入淡出以下脚本。
在场景更改脚本中将场景更改为帧缓冲区后的图像
对象包含场景更改前的图像以及显示的图像
使用obj.getvalue（“scenechange”）获取百分比并处理它。
* 0表示对象，1表示帧缓冲区。

a = 1-obj.getvalue（“scenechange”）
obj.draw（0,0,0,1，a）

○显示定位点和获取坐标的示例
使用以下脚本显示锚点并获取坐标。

场合使用对话框变量时
--dialog：coordinates，pos = {}
num = 3
obj.setanchor（“pos”，num，“loop”）;
对于i = 0，num-1做
x = pos [i * 2 + 1]
y = pos [i * 2 + 2]
结束
※在3D坐标的情况下，输入3个XYZ坐标的数组。
※您也可以输入pos = {}的初始值。

场合使用轨迹栏时
--track0：X，-1000,1000,0
--track1：Y，-1000,1000,0
--track2：Z，-1000,1000,0
num = obj.setanchor（“track”，0，“xyz”，“line”）;
对于i = 0，num-1做
x = obj.getvalue（0,0，i）
y = obj.getvalue（1,0，i）
z = obj.getvalue（2,0，i）
结束

场合多次使用obj.setanchor（）时
--dialog：坐标1，pos1 = {};坐标2，pos2 = {}
obj.setanchor（“pos1”，4，“loop”，“color”，RGB（0,255,255））;
obj.setanchor（“pos2”，2，“line”，“color”，RGB（0,255,0））;
※您不能使用同一对话框的多个变量。

○轨迹栏更改方法脚本示例
以下脚本以相同的速度将轨迹栏值从起点更改为终点。
您不能在轨迹栏更改方法脚本中使用与普通对象相关的变量或函数。
在脚本文件（* .tra）的开头指定'--twopoint'是一种忽略中间点的更改方法。
指定' -  param：Initial value（Integer）'可启用跟踪栏设置。
指定' -  speed：acceleration initial value（0/1），减速初始值（0/1）'可启用加速/减速设置。

index，ratio = math.modf（obj.getpoint（“index”））
st = obj.getpoint（index）;
ed = obj.getpoint（index + 1）;
return st +（ed-st）* ratio;


 - 历史 - 

[2011/2/28] ver 0.87 f
修复了在处理失去obj.effect（）中的图像时未正确反映的问题。
修复了obj.load（）无法读取文件名中包含全角字符的图像文件。
修复了无法使用obj.load（）加载影片文件时显示的警告对话框。
添加obj.load（）的文本加载不能在文本对象中使用的描述。
添加了在脚本之后执行过滤效果的函数到obj.effect（）。

[2011/3/29] ver 0.87 g
修复了当obj.effect（）中参数（如大小）发生变化时未反映的情况。
添加了obj.drawpoly（）和obj.setoption（）。
为obj.setfont（）添加了颜色参数。
添加了对话框选择功能（ -  color，-file）。

[2011/3/30] ver 0.87h
修复了obj.effect（）处理后某些参数恢复到原始值的问题。

[2011/4/10] ver 0.87i
修复了在颜色选择对话框中取消时未恢复颜色的问题。
添加了对话框选择功能（ - 对话框）。
添加了obj.getoption（）。

[2011/4/25] ver 0.88
修复了--dialog定义中使用的某些字符无法正常工作的问题。
修复了obj.setoption（）的混合未反映在obj.draw（）和obj.drawpoly（）中的问题。
轨迹栏和复选框以外的设置值也反映在obj.effect（）中。

[2011/5/8] ver 0.88a
修复了obj.effect（）中未正确反映设置值的问题。
当绘图对象的混合模式是标准时，会反映obj.setoption（）的混合。
可以在--dialog中输入的最大项目数已增加到12。

[2011/5/30] ver 0.88b
添加了可以使用obj.getoption（）获取的信息类型。
添加了obj.getvalue（）。

[2011/6/20] ver 0.89
即使通过obj.getvalue（）获取标准绘图对象的Z坐标，也会返回该值。
通过obj.getvalue（）可以获得另一个层的对象的值。

[2011/7/19] ver 0.89b
添加了obj.getaudio（）和obj.getpixel（）。

[2011/8/1] ver 0.89c
能够省略obj.getpixel（）的像素类型。
添加了obj.putpixel（），obj.copypixel（）和obj.pixeloption（）。
 - 修正了--dialog中没有正确反映对话框值的问题。

[2011/8/22] ver 0.89d
修复了某些脚本名称无法正常工作的问题。
修复了在obj.getaudio（）中使用“audiobuffer”时相机控制无效的问题。

[2011/8/29] ver 0.89e
使用--dialog的对话框的值

[2011/9/5] ver 0.89f
 - 修正了在--dialog中更改值时可能无法正确显示设置内容的问题。
修复了使用obj.getvalue（）无法获得正确值的问题。

[2011/10/2] ver 0.89 g
修复了根据obj.rand（）中的条件很容易获得类似值的问题。
能够在obj.drawpoly（）中省略uv坐标。
添加了带有alpha到obj.load（）的电影文件的参数。
添加了与obj.load（）和obj.setoption（）的虚拟缓冲区关联。
添加了obj.copybuffer（）。
添加了可以使用obj.getvalue（）获取的信息类型。
 - 可以通过轨道设置值的更改单位。
添加了场景更改脚本的说明。

[2011/10/16] ver 0.89h
参数被添加到obj.load（）的“framebuffer”和“tempbuffer”中。
在obj.setoption中添加了虚拟缓冲区专用混合模式以“混合”。
 - 通过对话框的定义，可以设置复选框的选择以及颜色和图形。

[2011/11/7] ver 0.89i
可以在场景更改脚本中使用的轨迹栏数已更改为最多两个。
添加了obj.filter（）。

[2011/11/19] ver 0.89j
package.path和package.cpath的初始值已更改为包含exedit.auf和脚本文件夹的文件夹。
在obj.setoption（）中更改与虚拟缓冲区相关的参数。 ※您可以像以前一样使用它。
添加了obj.setanchor（），RGB（），OR（），AND（），XOR（），SHIFT（）。
使用obj.setanchor（）添加了锚点控制的描述。

[2011/11/23] ver 0.89j2
添加了obj.getinfo（），obj.getpixeldata（）和obj.putpixeldata（）。
添加了obj.setanchor（）选项。

[2011/12/5] ver 0.89k
修复了虚拟缓冲区绘制时未反映obj.setoption（）的“antialias”设置。
修复了obj.getpixeldata（）和obj.putpixeldata（）无法正常工作的问题。
修复了obj.setanchor（）的返回值没有返回的问题。
将参考旋转角度添加到obj.rx，obj.ry和obj.rz的初始角度。
添加了obj.cx，obj.cy和obj.cz.

[2011/12/26] ver 0.89 l
修复了在时间轴上放置滤镜效果时未显示obj.setanchor（）的问题。
添加了一种设置方法，用于更改RGB（）中对象的颜色随时间的变化。
在obj.getoption（）中添加了“camera_param”，“camera_mode”和“gui”。
在obj.setoption（）中添加了“camera_param”和“draw_state”。
为obj.getinfo（）添加了“保存”。
添加了obj.copybuffer（）的参数类型。
添加了obj.interpolation（）和HSV（）。

[2011/12/29] ver 0.89 l3
添加了obj.getoption（）和obj.setoption（）的“camera_param”的设置。

[2012/1/9] ver 0.89 m
修复了在使用obj.getvalue（）获取音频对象时获取坐标等时被删除的问题。
为obj.getvalue（）的目标添加了“alpha”和“aspect”。
在obj.setanchor（）的选项中添加了“inout”和“color”。
已启用多次调用obj.setanchor（）。

[2012/1/22] ver 0.89m2
在obj.setoption（）中添加了一个选项“blend”。
添加了一个只显示obj.setanchor（）中的行的方法。
在obj.getpixeldata（）中添加了“type”选项。

[2012/1/29] ver 0.89n
修复了隐藏obj.getoption（）的“gui”中目标的设置对话框有时是真的。
--dialog的第一个颜色设置（/ col）按钮也显示在对象设置对话框中。
同时在对话框（--dialog等）中添加了--check0。

[2012/3/4] ver 0.89 o
修复了为1点对象执行obj.getpixeldata（）时被删除的问题。
修复了obj.getpixeldata（）中宽度为奇数时灰尘可能进入的问题。
在obj.setoption（）中添加了“focus_mode”。
脚本读取缓冲区已增加。
可以在--dialog中输入的最大项目数已增加到16。
执行时不将脚本文件转换为UTF-8。

[2012/3/13] ver 0.89p
脚本控制，它是在不将文本对象转换为UTF-8的情况下执行的。

[2012/3/24] ver 0.89 p2
能够显示带有mes（）和obj.load（）的“text”的Unicode标记（十进制数）。
脚本控制，将文本对象的Unicode字符转换为标记并处理它们。

[2012/4/8] ver 0.90
在obj.copybuffer（）的参数类型中添加了“cache”和“image”。

[2012/5/27] ver 0.90b
添加采样率以返回obj.getaudio（）的值。

[2012/6/17] ver 0.90c
将“fourier”添加到obj.getaudio（）的类型中

[2012/7/17] ver 0.90c4
为obj.getoption（）添加了“multi_object”选项。

[2012/9/3] ver 0.90d3
修复了使用相机控制+阴影时obj.setanchor（）无法正确移动的问题。

[2013/1/3] ver 0.90e
使用obj.putpixeldata（）添加了对用户数据格式的支持。

[2013/1/6] ver 0.90e2
为obj.getvalue（）的目标添加了“时间”。

[2013/2/11] ver 0.90e3
修复了在obj.copybuffer（）中处理大小为0的对象时发生的问题。

[2013/3/3] ver 0.90e4
添加了跳过obj.getoption（）的“script_name”的选项。
添加了obj.effect（）的描述。
在obj.load（）中添加了“layer”和“before”。
我们可以从脚本中只调用一次脚本。

[2013/3/18] ver 0.90e5
修复了在obj.load（）的“layer”中指定音频对象时的丢弃。
修复了obj.getoption（）中的“script_name”跳过中间点后无法正常工作的问题。

[2013/4/15] ver 0.91
在obj.getpixeldata（）中添加了“alloc”选项。
可以使用obj.getaudio（）通过返回值获取数据表。
添加了obj.getpoint（）。
添加了轨迹栏更改方法脚本的说明。

[2013/4/21] ver 0.91a
在轨迹栏更改方法脚本中添加了package.path和package.cpath。
添加了obj.rand（）来跟踪条形更改方法脚本。

[2013/6/2] ver 0.91b
修复了从脚本调用脚本并返回时更改虚拟缓冲区大小的问题。
选项“alpha_add2”已添加到obj.setoption（）中的“blend”中。

[2013/6/30] ver 0.91c
在obj.load（）中为“text”添加了“speed”和“time”选项。
在obj.getinfo（）中添加了“image_max”。


 - 关于Lua二元 - 

将lua51.dll附加到位于Lua主站点上的5.1.4版本
它是用5.14-2补丁构建的。

Lua的主页
http://www.lua.org/


	Lua License
	-----------

	Lua is licensed under the terms of the MIT license reproduced below.
	This means that Lua is free software and can be used for both academic
	and commercial purposes at absolutely no cost.

	For details and rationale, see http://www.lua.org/license.html .

	===============================================================================

	Copyright (C) 1994-2008 Lua.org, PUC-Rio.

	Permission is hereby granted, free of charge, to any person obtaining a copy
	of this software and associated documentation files (the "Software"), to deal
	in the Software without restriction, including without limitation the rights
	to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
	copies of the Software, and to permit persons to whom the Software is
	furnished to do so, subject to the following conditions:

	The above copyright notice and this permission notice shall be included in
	all copies or substantial portions of the Software.

	THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
	IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
	FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL THE
	AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
	LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
	OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
	THE SOFTWARE.

	===============================================================================

```
