# gooxml-test
###  安装gooxml
	```
	go get baliance.com/gooxml/
	go build -i baliance.com/gooxml/...
	```
## 打开文件

	``` 
	f, err := os.Open("your file path")
	    if err != nil {
		logger.Error(err)
	    }
	defer f.Close()
	doc, err := document.Read(f, filesize)
	```


## 解析纯文本
			
	``` 
	for _, par := range doc.Paragraphs() {  //读取文档类所有段落
		for _, run := range par.Runs() {
		    txt := run.Text()
		    fmt.Println("Paragraphs", txt)
		}
	}
	```

## 解析表格

	``` 
	for tabId, tbl := range doc.Tables() {  //返回文档类所有表格
		for rowId, row := range tbl.Rows() {
		    for cellId, cell := range row.Cells() {
			tex := ""

			for _, par := range cell.Paragraphs() {
			    for _, run := range par.Runs() {
				if run.Text() == "" {
				    continue
				}
				tex += run.Text()
				// fmt.Println("粗体", run.Properties().IsBold(), run.Text())   //判断是否是粗体
				//fmt.Println("粗体准确属性", run.Properties().BoldValue(), run.Text())
				// fmt.Println("斜体", run.Properties().IsItalic(), run.Text()) //判断是否是斜体
				// fmt.Println("斜体准确属性", run.Properties().ItalicValue(), run.Text())

			    }
			}
			fmt.Println("table"+gconv.String(tabId), "行"+gconv.String(rowId), "列"+gconv.String(cellId), tex)
		    }
		}
	    }
	```

## 解析图片

	``` 
	    //var fileBytes []byte
	    for k, img := range doc.Images {  //返回文档内所有图片 
		logger.Print("image:", k, img.Format(), img.Path(), img.Size())
		// imagName := gconv.String(time.Now().Unix()) + "_" + gconv.String(k) + "." + img.Format()
		// f, err := os.OpenFile(img.Path(), os.O_RDONLY, 0600)
		// if err != nil {
		//  fmt.Println(err.Error())
		// }
		// fileBytes, _ = ioutil.ReadAll(f)
		// // 上传到cos服务
		// fileUrl, cosKey, _ := gcos.CosStorageUpLoad(fileBytes, "img", imagName)
		// logger.Print(fileUrl, cosKey)
		f.Close()

	    }
	```

## 更多word文档操作

	``` 
	 https://github.com/carmel/gooxml
	```
