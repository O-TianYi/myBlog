#### 对返回内容进行转义

##### 出现问题原因：

显示的内容带html标签，原因后台请求返回的数据为进过转义的数据，例如“<”被转义为了&lt。

##### 解决：

把返回的字符串进行转义处理：

```
project_content: "蔬菜生产管护是需要非常有耐心的，合适的请报名。&lt;img src=&quot;https://ynrbhupload.yl1001.com/2020-11-16/5fb2507c54020.jpg&quot; alt=&quot;&quot; /&gt;&lt;img src=&quot;https://ynrbhupload.yl1001.com/2020-11-16/5fb2507c6b800.png&quot; alt=&quot;&quot; /&gt;"
```



```
htmlDecodeByRegExp(str) {
var temp = "";
    if (str.length == 0) return "";
    temp = str.replace(/&amp;/g, "&");
    temp = temp.replace(/&lt;/g, "<");
    temp = temp.replace(/&gt;/g, ">");
    temp = temp.replace(/&nbsp;/g, " ");
    temp = temp.replace(/&#39;/g, "'");
    temp = temp.replace(/&quot;/g, '"');
    temp = temp.replace(/↵/g, "");
    return temp;
},

this.htmlDecodeByRegExp(data.data.project_content);
```







##### 富文本框的引入

##### 使用：

```
import tinymceEditor from "@/components/tinymce-editor";

components: {
	tinymceEditor,
},

<tinymce-editor :disabled="true" :key="tinymceFlag" v-model="dataForm.project_content" ref="editor"></tinymce-editor>
```



#####  富文本框组件：

```
<template>
    <div class="tinymce-editor">
        <editor v-model="myValue" :init="init" :disabled="disabled" @onClick="onClick"></editor>
    </div>
</template>
<script>
import tinymce from "tinymce/tinymce";
import Editor from "@tinymce/tinymce-vue";
import "tinymce/themes/silver";
// 编辑器插件plugins
// 更多插件参考：https://www.tiny.cloud/docs/plugins/
import "tinymce/plugins/image"; // 插入上传图片插件
import "tinymce/plugins/media"; // 插入视频插件
import "tinymce/plugins/table"; // 插入表格插件
import "tinymce/plugins/lists"; // 列表插件
import "tinymce/plugins/wordcount"; // 字数统计插件
import "tinymce/plugins/colorpicker"; //
import "tinymce/plugins/contextmenu";
import "tinymce/plugins/textcolor";
import "tinymce/plugins/code";
import "tinymce/plugins/link";
import "tinymce/plugins/advlist";
import "tinymce/plugins/autolink";
import "tinymce/icons/default/icons.min.js";
export default {
    components: {
        Editor,
    },
    props: {
        value: {
            type: String,
            default: "",
        },
        disabled: {
            type: Boolean,
            default: false,
        },
        plugins: {
            type: [String, Array],
            default:
                "lists advlist link  image media table wordcount contextmenu textcolor code",
        },
        toolbar: {
            type: [String, Array],
            default: `code | undo redo | styleselect | fontselect | formatselect | fontsizeselect | link | forecolor backcolor | 
                bold italic underline strikethrough | image  media wordcount | table | contextmenu textcolor | alignleft aligncenter alignright alignjustify | 
                outdent indent | numlist bullist | preview removeformat  hr | paste | fullscreen `,
        },
    },
    data() {
        return {
            init: {
                language_url:
                    window.SITE_CONFIG.cdnUrl +
                    "/static/tinymce/langs/zh_CN.js",
                language: "zh_CN",
                skin_url:
                    window.SITE_CONFIG.cdnUrl +
                    "/static/tinymce/skins/ui/oxide",
                // skin_url: '/tinymce/skins/ui/oxide',//暗色系
                height: 400,
                plugins: this.plugins,
                toolbar: this.toolbar,
                // branding: true,
                menubar: true,
                // 此处为图片上传处理函数，这个直接用了base64的图片形式上传图片，
                // 如需ajax上传可参考https://www.tiny.cloud/docs/configure/file-image-upload/#images_upload_handler
                images_upload_handler: (blobInfo, success, failure) => {
                    this.uploadform(blobInfo.blob()).then((res) => {
                        // success(window.SITE_CONFIG.rbhUrl + res.url)
                        success(res.url);
                    });
                },
                content_style: `
                        *                         { padding:0; margin:0; }
                        html, body                { height:100%; }
                        img                       { max-width:100%; display:block;height:auto; }
                        a                         { text-decoration: none; }
                        iframe                    { width: 100%; }
                        p                         { line-height:1.6; margin: 0px; }
                        table                     { word-wrap:break-word; word-break:break-all; max-width:100%; border:none; border-color:#999; }
                        .mce-object-iframe        { width:100%; box-sizing:border-box; margin:0; padding:0; }
                        ul,ol                     { list-style-position:inside; }
                    `,
                // CONFIG: Paste
                paste_retain_style_properties: "all",
                paste_word_valid_elements: "*[*]", // word需要它
                paste_data_images: true, // 粘贴的同时能把内容里的图片自动上传，非常强力的功能
                paste_convert_word_fake_lists: false, // 插入word文档需要该属性
                paste_webkit_styles: "all",
                paste_merge_formats: true,
                nonbreaking_force_tab: false,
                paste_auto_cleanup_on_paste: false,
                style_formats: [
                    {
                        title: "首行缩进",
                        block: "p",
                        styles: {
                            "text-indent": "2em",
                        },
                    },
                    {
                        title: "行高",
                        items: [
                            {
                                title: "1",
                                styles: {
                                    "line-height": "1",
                                },
                                inline: "span",
                            },
                            {
                                title: "1.5",
                                styles: {
                                    "line-height": "1.5",
                                },
                                inline: "span",
                            },
                            {
                                title: "2",
                                styles: {
                                    "line-height": "2",
                                },
                                inline: "span",
                            },
                            {
                                title: "2.5",
                                styles: {
                                    "line-height": "2.5",
                                },
                                inline: "span",
                            },
                            {
                                title: "3",
                                styles: {
                                    "line-height": "3",
                                },
                                inline: "span",
                            },
                            {
                                title: "4",
                                styles: {
                                    "line-height": "4",
                                },
                                inline: "span",
                            },
                            {
                                title: "5",
                                styles: {
                                    "line-height": "5",
                                },
                                inline: "span",
                            },
                        ],
                    },
                ],
                font_formats: `
                    微软雅黑=微软雅黑;
                    宋体=宋体;
                    黑体=黑体;
                    仿宋=仿宋;
                    楷体=楷体;
                    隶书=隶书;
                    幼圆=幼圆;
                    Andale Mono=andale mono,times;
                    Arial=arial, helvetica,
                    sans-serif;
                    Arial Black=arial black, avant garde;
                    Book Antiqua=book antiqua,palatino;
                    Comic Sans MS=comic sans ms,sans-serif;
                    Courier New=courier new,courier;
                    Georgia=georgia,palatino;
                    Helvetica=helvetica;
                    Impact=impact,chicago;
                    Symbol=symbol;
                    Tahoma=tahoma,arial,helvetica,sans-serif;
                    Terminal=terminal,monaco;
                    Times New Roman=times new roman,times;
                    Trebuchet MS=trebuchet ms,geneva;
                    Verdana=verdana,geneva;
                    Webdings=webdings;
                    Wingdings=wingdings,zapf dingbats`,
                // Image
                imagetools_toolbar:
                    "rotateleft rotateright | flipv fliph | editimage imageoptions",
            },
            myValue: this.value,
        };
    },
    mounted() {},
    methods: {
        uploadform(file) {
            return new Promise((res, rej) => {
                var a = new FormData(); // formdata 请求是没有跨域限制的
                //使用append方法向空的FormData对象添加字段
                a.append("file", file); //上传文件
                var oReq = new XMLHttpRequest();
                oReq.onload = function (info) {
                    if (info.target.status === 200) {
                        res(JSON.parse(info.target.response));
                    }
                    console.log("info", info);
                };
                let url =
                    window.SITE_CONFIG.rbhUrl +
                    "/person.php/info_index/Jsapi/uploadImg.html";
                oReq.open("POST", url);
                oReq.send(a);
            });
        },
        // 添加相关的事件，可用的事件参照文档=> https://github.com/tinymce/tinymce-vue => All available events
        // 需要什么事件可以自己增加
        onClick(e) {
            console.log("e", e);
            this.$emit("onClick", e, tinymce);
        },
        // 可以添加一些自己的自定义事件，如清空内容
        clear() {
            this.myValue = "";
        },
    },
    watch: {
        value(newValue) {
            this.myValue = newValue;
        },
        myValue(newValue) {
            this.$emit("input", newValue);
        },
    },
};
</script>
```





#### el-upload在action的时候传递参数

##### 场景：

post请求videoAction地址，访问该地址需要传递两个参数，file和appName，file为选中的文件内容，默认会携带，不需要写；所以需要携带的就只有appName这个参数，这个参数携带只需要添加

`:data="{appName: 'yunnan-guojiaohui'}"`即可传递

```
<el-upload  :action="videoAction" :show-file-list="false" :on-success="handleVideoSuccess" :data="{appName: 'yunnan-guojiaohui'}">
        <video v-if="dataForm.videoUrl !='' && videoFlag == false" :src="dataForm.videoUrl" id="videoPlayer" class="avatar2" controls="controls">您的浏览器不支持视频播放</video>
        <i v-else-if="dataForm.videoUrl =='' && videoFlag == false" class="el-icon-plus avatar-uploader-icon2"></i>
        <el-progress v-if="videoFlag == true" type="circle" :percentage="videoUploadPercent" style="margin-top:30px;"></el-progress>
</el-upload>
```



##### el-upload上传限制上传文件的格式和大小：

utils/index.js:

```
export function pictureLimit(file, vm) {
  const pictureEnable = file.size / 1024 / 1024 < 1;
  const imageTypes = ['image/jpeg', 'image/png','image/gif']
  const isJPG = imageTypes.indexOf(file.type) > -1;
  if (!isJPG) {
    vm.$message.error("仅支持 JPG/png/jpeg/gif 格式的图片!");
  }
  if (!pictureEnable) {
    vm.$message.error("上传图片大小不能超过 1MB!");
  }
  return isJPG && pictureEnable;
}
const pictureUpTypetips = '支持(jpg/png/jpeg/gif格式)，图片小于1M';
```





#### jquery实现滚动的时候触发动画：

##### 获取滚动的位置：

```
$(window).on('scroll',throttle(animate1,500))
//节流操作
function throttle(after, wait) {
    var timer;
    var isScroll; //是否正在执行回调
    return function() {
    if (isScroll) return; //在回调函数未执行完以前
        isScroll = true;
        timer && clearTimeout(timer);
        timer = setTimeout(function() {
            after && after();
            isScroll = false;
            timer = null;
        }, wait);
    }
}
```

```
//动画方法
//先设置透明，滚动到指定位置的时候有种从无到有的感觉
$('.newsImgList .swiperImg img').css({opacity: 0})

function animate1(){
    if ( $(window).scrollTop() >= 200){
    	$('.newsImgList .swiperImg img').addClass('fadeInLeft').css({opacity: 1})
    }
    if ( $(window).scrollTop() >= 1200){
        $('.zc-content .zc-box').first().fadeIn('fast',function testShow(){
        	$(this).next().fadeIn('fast',testShow);
        })
    }
}

/*从左到右*/
.fadeInLeft{
  animation: fadeInLeft 1.5s ease-in;
  -webkit-animation: fadeInLeft 1.5s ease-in;
}

/*从左到右进入*/
@keyframes fadeInLeft
{
    from {
      transform: translate(-300px,0);
      -webkit-transform: translate(-300px,0);
      -moz-transform: translate(-300px,0);
      -ms-transform: translate(-300px,0);
      -o-transform: translate(-300px,0);
    }
    to {
        -webkit-transform: translate(0,0); 
        transform: translate(0,0); 
        -moz-transform: translate(0,0);
        -ms-transform: translate(0,0);
        -o-transform: translate(0,0);
    }
}

@-webkit-keyframes fadeInLeft {
  from {
    transform: translate(-300px,0);
    -webkit-transform: translate(-300px,0);
    -moz-transform: translate(-300px,0);
    -ms-transform: translate(-300px,0);
    -o-transform: translate(-300px,0);
  }
  to {
      -webkit-transform: translate(0,0); 
      transform: translate(0,0); 
      -moz-transform: translate(0,0);
      -ms-transform: translate(0,0);
      -o-transform: translate(0,0);
  }
}
```









