# Spatial Typography Engine

主标题是 KV 的空间构件，不是简单叠加在图片上的文字。

## Modes

### TITLE_AS_SIGNAGE
标题成为餐厅门头 / 牌匾 / 招牌。

### TITLE_AS_ARCHITECTURE
标题成为墙体、门廊、梁柱、入口框架或空间建筑。

### TITLE_AS_STAGE
标题形成食物背后的巨大舞台。

### TITLE_AS_DEPTH_FIELD
标题沿纵深组织，形成视觉通道或深度场。

### TITLE_AS_FOREGROUND_GRAPHIC
少量字形进入近景，与主体边缘交错，但不得抢过 Food Hero。

## Food Translation Rule

可以借鉴巨字透视 Campaign 的空间语法，但必须翻译成餐饮空间语言：木构、门头、屏风、石材、餐桌、店堂、灯笼、菜单牌、地方器物等。

禁止默认生成科技墙、赛博走廊、HUD、参数屏。

## Material & Light

标题必须与环境共享：

- 光源方向
- 色温
- 接触阴影
- 空气透视
- 材质反射

金色毛笔字如果被设为门头结构，应有实体边缘、受光面和阴影，而不是平面贴图。

## Readability

中文准确率优先于造型。

任何空间扭曲不得导致：错字、粘连、缺笔画、难识别。