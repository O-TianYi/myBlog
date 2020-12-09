tool.js:

```js
/**
 * 网页方法 
 */


//获取url中的参数params
function getUrlParam(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)"); //构造一个含有目标参数的正则表达式对象
    var r = window.location.search.substr(1).match(reg); //匹配目标参数
    if (r != null) return decodeURI(r[2]); return null; //返回参数值
};

// 下载文件
function downLoadFile(url, fileName, callback) {
    let oA = document.createElement('a');
    oA.setAttribute('href', url);
    if(fileName) {
        oA.setAttribute('download', fileName);
    }
    oA.setAttribute('target', '__blank');
    oA.onclick = () => {
        // console.log('下载附件')
        callback instanceof Function && callback();
    }
    oA.click();
}

// 复制文本
function copyText(text, success) {
    let input = document.createElement('input');
    input.setAttribute('readonly', 'readonly'); //兼容ios弹起闪烁
    input.setAttribute('value', text);
    document.body.appendChild(input);
    // setSelectionRange 兼容ios
    input.select();
    input.setSelectionRange(0, text.length);

    try {
        var successful = document.execCommand('copy'); // 执行 copy 操作 (只能copy选中的内容且在页面上)
        var msg = successful ? 'successful' : 'unsuccessful';
        console.log('Copy was ' + msg);
        success instanceof Function && success(text);
    } catch (err) {
        console.log(err);
    }
    document.body.removeChild(input)
    window.getSelection().removeAllRanges(); // 移除选中的元素
}


// pc端细节自适应
var adaption = {
    _w: document.documentElement.clientWidth,
    changeWidth: function() {
        this._w = document.documentElement.clientWidth;
    },
    _p: function (width) {
        return ((this._w * width) / 1920);
    }
}



// 判断浏览器函数
function isMobile(){
    if(window.navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i)) {
        return true; // 移动端
    }else{
        return false; // PC端
    }
}

function checkPhoneValid(number) {

    // 兼容国内/国际手机号
    // 参见 https://cloud.tencent.com/developer/article/1140913
  
    const phones = {
      'ar-DZ': /^(\+?213|0)(5|6|7)\d{8}$/,
      'ar-SY': /^(!?(\+?963)|0)?9\d{8}$/,
      'ar-SA': /^(!?(\+?966)|0)?5\d{8}$/,
      'en-US': /^(\+?1)?[2-9]\d{2}[2-9](?!11)\d{6}$/,
      'cs-CZ': /^(\+?420)? ?[1-9][0-9]{2} ?[0-9]{3} ?[0-9]{3}$/,
      'de-DE': /^(\+?49[ \.\-])?([\(]{1}[0-9]{1,6}[\)])?([0-9 \.\-\/]{3,20})((x|ext|extension)[ ]?[0-9]{1,4})?$/,
      'da-DK': /^(\+?45)?(\d{8})$/,
      'el-GR': /^(\+?30)?(69\d{8})$/,
      'en-AU': /^(\+?61|0)4\d{8}$/,
      'en-GB': /^(\+?44|0)7\d{9}$/,
      'en-HK': /^(\+?852\-?)?[569]\d{3}\-?\d{4}$/,
      'en-IN': /^(\+?91|0)?[789]\d{9}$/,
      'en-NZ': /^(\+?64|0)2\d{7,9}$/,
      'en-ZA': /^(\+?27|0)\d{9}$/,
      'en-ZM': /^(\+?26)?09[567]\d{7}$/,
      'es-ES': /^(\+?34)?(6\d{1}|7[1234])\d{7}$/,
      'fi-FI': /^(\+?358|0)\s?(4(0|1|2|4|5)?|50)\s?(\d\s?){4,8}\d$/,
      'fr-FR': /^(\+?33|0)[67]\d{8}$/,
      'he-IL': /^(\+972|0)([23489]|5[0248]|77)[1-9]\d{6}/,
      'hu-HU': /^(\+?36)(20|30|70)\d{7}$/,
      'it-IT': /^(\+?39)?\s?3\d{2} ?\d{6,7}$/,
      'ja-JP': /^(\+?81|0)\d{1,4}[ \-]?\d{1,4}[ \-]?\d{4}$/,
      'ms-MY': /^(\+?6?01){1}(([145]{1}(\-|\s)?\d{7,8})|([236789]{1}(\s|\-)?\d{7}))$/,
      'nb-NO': /^(\+?47)?[49]\d{7}$/,
      'nl-BE': /^(\+?32|0)4?\d{8}$/,
      'nn-NO': /^(\+?47)?[49]\d{7}$/,
      'pl-PL': /^(\+?48)? ?[5-8]\d ?\d{3} ?\d{2} ?\d{2}$/,
      'pt-BR': /^(\+?55|0)\-?[1-9]{2}\-?[2-9]{1}\d{3,4}\-?\d{4}$/,
      'pt-PT': /^(\+?351)?9[1236]\d{7}$/,
      'ru-RU': /^(\+?7|8)?9\d{9}$/,
      'sr-RS': /^(\+3816|06)[- \d]{5,9}$/,
      'tr-TR': /^(\+?90|0)?5\d{9}$/,
      'vi-VN': /^(\+?84|0)?((1(2([0-9])|6([2-9])|88|99))|(9((?!5)[0-9])))([0-9]{7})$/,
      'zh-CN': /^(\+?0?86\-?)?1[3456789]\d{9}$/,
      'zh-TW': /^(\+?886\-?|0)?9\d{8}$/
    };
  
    const regArr = Object.values(phones);
  
    return regArr.some(reg => reg.test(number));
}

// 校验邮箱格式是否正确
export const checkEmailValid = (email) => {
    const reg = /^([a-zA-Z]|[0-9])(\w|\-)+@([a-zA-Z0-9]|\-)+\.([a-zA-Z]{2,4})$/;
    return reg.test(email);
}




/**
 * 小程序方法
 */
// 通用跳转
export function navigateTo({
	url,
	event = {}
}) {
	let _len = getCurrentPages().length;
	return new Promise((res, rej) => {
		if (_len > 8) {
			wx.redirectTo({
				url,
				success() {
					res();
				},
				fail() {
					wx.switchTab({
						url,
						success() {
							res();
						},
						fail() {
							rej();
						}
					})
				}
			})
		} else {
			wx.navigateTo({
				url,
				event,
				success() {
					res();
				},
				fail() {
					wx.switchTab({
						url,
						success() {
							res();
						},
						fail() {
							rej();
						}
					})
				}
			})
		}

	})
}




/**
 * 跨平台方法
 */

// 参数转化
function objToQuery(obj) {
	var _i = 0,
		result = "";
	for (var prop in obj) {
		if (_i == 0) {
			result += `?${prop}=${obj[prop]}`;
		} else {
			result += `&${prop}=${obj[prop]}`;
		}
		_i++;
	}
	return result;
}

function StringUtil(str) {
    // 存储字符串
    this.str = str || '';

    /**
     * 把字符串中的特殊字符串，转成特定的html
     * @param {String} str
     * @param {String} element
     */
    StringUtil.prototype.toElement = function(str = '\n', element = 'br') {
        let reg = new RegExp(str, 'g');
        return this.str.replace(reg, `<${element}><${element}/>`)
    }


    return this instanceof StringUtil ? this : new StringUtil(str);
}


function Moment(date) {
    // 存储时间
    this.date = date ? new Date(date) : new Date();


    /**
     * 转化成不同类型的字符串
     * @param {String} pattern 时间展示形式 和elementui一致
     * @return {String}  
     */
    Moment.prototype.format = function (pattern = 'yyyy-MM-dd hh:mm:ss') {
        let _this = this;
        // pattern
        let reg = /(\w)+/g;
        return pattern.replace(reg, function(match) {
            return _this.query(match);
        })
       
    }; 

    /**
     * @param {String} type 类型
     */
    Moment.prototype.query = function (type) {
        switch (type) {
            case 'yyyy':
                return this.date.getFullYear();
            case 'MM':
                let MM = this.date.getUTCMonth() + 1 + '';
                return MM.length == 2 ? MM : '0' + MM;
            case 'dd':
                let dd = this.date.getUTCDate() + '';
                return dd.length == 2 ? dd : '0' + dd;
            case 'hh':
                let hh = this.date.getHours() + '';
                return hh.length == 2 ? hh : '0' + hh;
            case 'mm':
                let mm = this.date.getMinutes() + '';
                return mm.length == 2 ? mm : '0' + mm;

            case 'ss':
                let ss = this.date.getSeconds() + '';
                return ss.length == 2 ? ss : '0' + ss;
        }

    }

    return this instanceof Moment ? this : new Moment(date);
}

```

