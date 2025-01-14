# gowatermark

使用 Go 语言开发图片水印工具，可以添加图片和文字水印。

## 安装

```
go get -u github.com/xing-zr/gowatermark
```

## 示例

- 添加图片水印
```golang
// 相关配置
config := gowatermark.ImageWatermarkConfig{
	OriginImagePath:    "./origin.jpg",        // 水印底图图片路径
	WatermarkImagePath: "./watermark.png",     // 水印图图片路径
	WatermarkPos:       gowatermark.LeftTop,   // 水印位置 有 左上、左下、右上、右下、平铺几个选项
	CompositeImagePath: "./composite.jpg",     // 合成后图片路径
    Opacity:   0.5,                            // 水印透明度 0-1 之间
    TiledRows: 3,                              // 水印平铺行数（水印类型为平铺有效）
    TiledCols: 4,                              // 水印平铺列数（水印类型为平铺有效）
}
// 生成图片水印图
err := gowatermark.CreateImageWatermark(config)
if err != nil {
	fmt.Println(err)
}
```
- 添加文字水印
1. 普通文字水印
```golang
// 相关配置
config := gowatermark.TextWatermarkConfig{
    OriginImagePath:    "./origin.jpg",      // 水印底图图片路径
    CompositeImagePath: "./composite.jpg",   // 合成后图片路径
    FontPath:           "./font.ttf",        // 字体文件路径
	TextInfos: []gowatermark.TextInfo{       // 文字内容位置信息
		{
			Text:  "hello world",
			Color: color.RGBA{R: 255, G: 255, B: 255, A: 255},
			Size:  20,
			X:     10,
			Y:     10,
		},
	},
}
// 生成文字水印图
err := gowatermark.CreateTextWatermark(config)
if err != nil {
	fmt.Println(err)
}
```
2. 文字水印平铺
```golang
// 相关配置
config := gowatermark.TextTiledWatermarkConfig{
	OriginImagePath:    "./origin.jpg",      // 水印底图图片路径
	CompositeImagePath: "./composite.jpg",   // 合成后图片路径
	FontPath:           "./font.ttf",        // 字体文件路径
	Text:               "hello world",       // 文字内容
	Color:              color.RGBA{R: 255, G: 255, B: 255, A: 255}, // 文字颜色
	TiledRows:          3,                   // 平铺行数
	TiledCols:          4,                   // 平铺列数
}
// 生成文字水印图
err := gowatermark.CreateTextTiledWatermark(config)
if err != nil {
	fmt.Println(err)
}
```