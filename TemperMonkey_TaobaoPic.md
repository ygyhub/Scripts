// ==UserScript==
// @name			淘宝 获取主图
// @namespace		https://item.taobao.com/
// @license         MIT
// @version			1
// @description		下载淘宝宝贝原图
// @author			YY
// @homepage		http://www.greasyfork.org/
// @match           https://item.taobao.com/*
// @iconURL         https://img.alicdn.com/favicon.ico
// @grant           GM_addStyle
// @grant           GM_download
// ==/UserScript==

	//Document Css Style
	GM_addStyle('\
	#download{\
	color: #E5511D;\
    border-color: #F0CAB6;\
    background: #FFE4D0;\
    list-style: none;\
    word-break: break-all;\
    text-align: center;\
    border: 0;\
    vertical-align: middle;\
    max-width: 50px;\
    max-height: 50px;\
    margin:0 auto;\
	}\
	');

   //下载主图
	document.onreadystatechange = function()
	{
		var DIV = document.createElement('button')
		DIV.id = 'download'
		DIV.innerHTML = '下载原图'
		document.getElementById('J_UlThumb').appendChild(DIV);
		DIV.onclick = function()
		{
			for(var i = 1;i <= 5; i++)
			{
			var url = "https:"+document.querySelector("#J_UlThumb > li:nth-child(" + i + ") > div > a > img").getAttribute("src")
			var patt = /https.*(?:jpg|png)(?=.*(?:jpg|png))/
			var orgurl = patt.exec(url)[0]
			var name = document.querySelector("#J_Title > h3").getAttribute('data-title')
			GM_download(orgurl,name + i + 'pic.jpg');
			}
		}

	};
