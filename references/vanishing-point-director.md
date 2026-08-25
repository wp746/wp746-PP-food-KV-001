# Vanishing Point Director

## Goal

建立一个主消失点，让 Food Hero、标题空间结构和环境属于同一摄影空间。

## Default

9:16 餐饮 KV 常用主消失点：画面中上部、中央或略偏一侧，具体依原照片决定。

## Align

尽量让以下元素服从同一纵深：

- 碗 / 盘的透视与椭圆关系
- 桌面纹理
- 门头 / 牌匾 / 标题建筑
- 走廊 / 梁柱 / 背景家具
- 菜单牌 / 辅助信息牌
- 蒸汽与空气透视
- 光源递减
- 前中后景尺度

## Hero Depth Stack

推荐：

```text
nearest foreground: food hero / vessel
near-mid: steam / utensil / subtle ingredients
mid: spatial headline structure
far: semantic restaurant environment
```

## Failure

- 食物一个视角，标题另一个透视。
- 背景水平线与桌面接触面冲突。
- 标题像后贴上去，没有环境阴影和尺度递减。
- 食物像漂浮在背景中。