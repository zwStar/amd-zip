
#### 说明  
修改 adm-zip支持GBK编码 解决中文内容和文件名乱码问题

修改内部内容读取部分代码 - 利用 jschardet 判断文件和文件名编码，利用 iconv-lite 解决中文编码问题


#### 源仓库地址： https://github.com/cthackers/adm-zip

#### 使用

```
$ npm install @zwg/adm-zip
```

```
var AdmZip = require('@zwg/adm-zip');

	// reading archives
	var zip = new AdmZip("./my_file.zip");
	var zipEntries = zip.getEntries(); // an array of ZipEntry records

	zipEntries.forEach(function(zipEntry) {
	    console.log(zipEntry.toString()); // outputs zip entries information
		if (zipEntry.entryName == "my_file.txt") {
		     console.log(zipEntry.getData().toString('utf8')); 
		}
	});
	// outputs the content of some_folder/my_file.txt
	console.log(zip.readAsText("some_folder/my_file.txt")); 
	// extracts the specified file to the specified location
	zip.extractEntryTo(/*entry name*/"some_folder/my_file.txt", /*target path*/"/home/me/tempfolder", /*maintainEntryPath*/false, /*overwrite*/true);
	// extracts everything
	zip.extractAllTo(/*target path*/"/home/me/zipcontent/", /*overwrite*/true);


	// creating archives
	var zip = new AdmZip();

	// add file directly
	var content = "inner content of the file";
	zip.addFile("test.txt", Buffer.alloc(content.length, content), "entry comment goes here");
	// add local file
	zip.addLocalFile("/home/me/some_picture.png");
	// get everything as a buffer
	var willSendthis = zip.toBuffer();
	// or write everything to disk
	zip.writeZip(/*target file name*/"/home/me/files.zip");
	
	
	// ... more examples in the wiki
	
	
```

#### 具体使用参考原库使用，无任何差别