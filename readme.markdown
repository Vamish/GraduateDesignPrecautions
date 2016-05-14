# 信息分析与预测系统前端数据对接、框架与用户交互设计

## 引言
数据分析的目的是把隐没在一大批看来杂乱无章的数据中的信息集中、萃取和提炼出来，以找出所研究对象的内在规律。在实用中，数据分析可帮助人们作出判断，以便采取适当行动。数据分析是组织有目的地收集数据、分析数据，使之成为信息的过程。信息采集、浏览、查询、交换、分析与预测，是信息社会重要的特征。国内外已经有许多著名的统计分析软件，例如SPSS, Statistica，SAS等，但是这类桌面端的软件在安装时需要费较长的时间和经过一系列相对复杂的操作学习，大大提高了用户使用的门槛，减低了进行数据分析的效率。而运行在浏览器的网页版软件，可以通过网址直接进行访问、使用，省去用户安装的时间，可以把大部分的精力都放在需要注意的事情上。而且相对于桌面端对于系统硬件的要求，网页端的计算全部在云端服务器上进行，用户只需关心数据的内容，而非是数据之外的麻烦。

前端框架的发展，已经允许我们在浏览器上实现相对复杂的软件操作，而且网页端的图表更新迭代的速度远大于桌面端的传统软件，这允许我们在本设计中运用交互性、便捷性、可读性更好的图表展示。这可使用户可以更清楚的了解，更透彻的分析，更直观的发现数据的关联、趋势等之前在传统桌面软件中不曾或难以发现的内容。

## 一、相关技术综述
### 1.1 Bootstrap 前端框架介绍
2011年8月，Twitter Bootstrap 诞生。到如今Bootstrap 已成为前端设计领域最受欢迎的辅助技术。Bootstrap是一组用于网站和网络应用程序开发的开源前端（所谓“前端”，指的是展现给最终用户的界面。与之对应的“后端”是在服务器上面运行的代码）框架，包括HTML、CSS及JavaScript的框架，提供字体排印、窗体、按钮、导航及其他各种组件及Javascript扩展，旨在使动态网页和Web应用的开发更加容易。Bootstrap 提供了大量可重用的组件，可以让开发者快速搭建优秀的、易于维护的网站。
### 1.2 HTML5 存储特性介绍
HTML5 是HTML 最新的修订版本，2014年10月由万维网联盟（W3C）完成标准制定。目标是替换1999年所制定的HTML 4.01和XHTML 1.0标准。HTML5 并不只是一个单独的技术。他是一个概括性的术语，包含了新的以及增强的HTML 元素、CSS样式、Javascript API 和事件。[参考文献](《HTML5 开发手册》 Chuck Hudson,Tom Leadbetter)

HTML5 在原先DOM 接口的基础上，增加了更多样化的API与提供了自定义数据属性。
    【TODO】图书馆

#### 1.2.1 本地存储API
本地存储API 是HTML5 API 中的一个新增项。传统网站在页面端的数据存储需求一般靠Cookie 操作，但Cookie 的存储大小十分有限，仅为4KB，常见的用途是在网站“记住密码”、存储用户身份判断数据等。并不适用于存储数据量复杂的情况。

HTML5 提供的本地存储API 中包括了：localStorage 和  sessionStorage 两种存储对象。两者都受到IE8以后版本及所有现代浏览器的广泛支持，包括移动设备。两个存储对象使用完全相同的API，这意味着任何用localStorage 完成的工作，用sessionStorage 也能做到，反之亦然[参考文献](《HTML5和 Javascript Web 应用开发》 - [美]Wesley Hale著 姚军译)。但是两者的使用范围与生命周期各有不同。localStorage 与sessionStorage 的存储大小一般为5MB，仅在客户端保存，并不参与和服务器的通信。其中localStorage 除非用户清楚，否则将会永久保存，而sessionStorage 仅在当前会话下有效，用户关闭页面或浏览器后都将被清除。
    
[参考文献](http://jerryzou.com/posts/cookie-and-web-storage/)

#### 1.2.2 自定义data-* 属性
自定义data-* 属性是以"data-*"开头的属性，其没有独立的命名空间。该属性与XML 兼容。
自定义data-* 属性用于当没有合适的属性或元素时存储页面中或者应用程序的定义数据。
    【TODO】图书馆
[参考文献](https://www.w3.org/TR/2011/WD-html5-20110525/elements.html#embedding-custom-non-visible-data-with-the-data-attributes)
### 1.3 Ajax 介绍
AJAX即“Asynchronous JavaScript and XML”（异步的JavaScript与XML技术），指的是一套综合了多项技术的浏览器端网页开发技术。Ajax的概念由杰西·詹姆士·贾瑞特所提出。

传统的Web应用允许用户端填写表单（form），当提交表单时就向Web服务器发送一个请求。服务器接收并处理传来的表单，然后送回一个新的网页，但这个做法浪费了许多带宽，因为在前后两个页面中的大部分HTML码往往是相同的。由于每次应用的沟通都需要向服务器发送请求，应用的回应时间依赖于服务器的回应时间。这导致了用户界面的回应比本机应用慢得多。

与此不同，AJAX应用可以仅向服务器发送并取回必须的数据，并在客户端采用JavaScript处理来自服务器的回应。因为在服务器和浏览器之间交换的数据大量减少,服务器回应更快了。同时，很多的处理工作可以在发出请求的客户端机器上完成，因此Web服务器的负荷也减少了。

## 二、系统设计
### 2.1 系统托管与版本控制
本系统由项目小组成员在不同地点协同完成，各有分工，所以设计系统之前最先考虑的是项目的托管与版本控制问题。

在比较目前流行的VCS（版本控制系统）后发现，开源社区Github 不仅能提供稳定的托管服务还解决了版本控制的问题，而且自带的issue 功能还能起到分配任务与bug 反馈的功能。这大大降低了项目维护的成本并提高了项目的稳定性。

### 2.2 程序流程与用户交互设计
本系统的主要流程如下：

用户访问 -> 数据上传 -> 数据表格展示 -> 用户选择相对应的数据分析功能 -> 参数与配置选择并提交 -> 展示相对应的数据表格与图表 -> 流程结束

【TODO】这里应该有个图

通过设计使用户在使用这个系统的时候觉得便捷是这个系统在设计之初的一个想法，『设计这项工作从石器时代起就是人们生活中必不可少的重要因素』[参考文献](田中一光《设计的觉醒》)。但是功能多了之后不一定让用户体验更简单，反而经常会导致用户更多的迷惑。[参考文献](《简约至上交互式设计四策略》)所以在设计流程的时候，我们在功能上采取了“删除”、“组织”、“隐藏”和“转移”四个交互设计策略。[参考文献，同上]“删除”在系统流程中不必要的、干扰用户选择的界面元素，“组织”相同属性的功能，“隐藏”次级功能的入口，避免分散用户的注意力，“转移”不同功能页面中的内容，使用户更清晰地了解数据与结果。

#### 2.2.1 数据上传
在用户使用本系统的过程中我们发现，绝大部分用户上传的数据文件为xls/xlsx 格式。在上传文件只有单一sheet或者非xls/xlsx格式的情况下，系统会直接跳转到该数据的数据展示页面并展示该数据。但由于Microsoft Office 套件在新建Excel 文档时默认会有sheet1 - sheet3 三个表单，而用户在本系统中分析的数据一般只有一个表单，所以我们在用户上传文件的时候会优先让用户选择要分析的表单，再对这个表单进行操作。这样一来，不仅用户不会因为操作到无关的表单而产生无效、干扰的数据结果，系统在处理相对应的表单的时候也能能快速高效的获取用户所选择、输入的值。

并且在优化用户交互体验方面，为了防止用户在选择表单的时候由于失误选错了表单，本系统会提供了在数据展示页面动态切换表单的功能。

#### 2.2.2 变量与配置选择
在实践中我们注意到，用户选择的数据配置并不会影响到后端功能的计算。于是，本系统采用的方式是在前端部分保存用户选择的参数信息，后台返回所有关于该功能计算后的值，再由前端部分根据用户选择的参数信息将制定的参数打印、显示。这样可以减少了后端的判断量，使系统能加轻便。

### 2.3 前端框架设计与数据对接模块设计
本系统功能繁多，而且各个功能之间的相关参数并没有复用的必要性。每个功能的传参都有独立的控件分别控制。因为每个功能间的参数、配置选择都是相互独立的。在本系统内应用的框架模式是在原有Bootstrap 样式框架的基础上，分功能设定出每个功能的弹框页面，并在该HTML 页面内应该有该功能逻辑的相关控制方法。并且由于功能点与可允许用户操作的菜单是一一对应的关系，通过这些功能所在的路径，定义好菜单的JSON 格式的配置文件，用户访问数据展示页面的页面上打印出可以让用户操作的菜单栏。

由于前后端的完全分离，在本系统中项目组决定使用JSON 作为数据传输的数据包。这是因为考虑到JSON 类型的通用性：无论是在前端Javascript 环境下或者是后端Java 环境下都有良好的支持。前端在数据对接模块采用了MVC 架构模式进行管理控制。在用户点击提交时，系统会设置一个该功能的标志位，每个功能控件中的参数封装成JSON 格式的数据包（Model 层）后封装好的方法VariableSubmit.js（Controller 层）通过Ajax 发送到指定标志位的后端进行处理，再后端处理后返回相对应的结果时，先判断返回数据的状态是否是正常可用的，若结果可用则把数据保存并跳转数据展示页面并且打印相对应的数据表格、数据图（View 层）等后续操作。

【TODO】这里能有一张图

### 2.4 多语言配置设计
多语言是本系统中一个可以独立的功能，它不参与具体的参数传输，只负责在页面内切换不同的语种时显示相对应的语种标签。于是这个功能应该完全由前端来负责实现。在设计时采用了MVC 架构模式来实现多语言配置模块。即通过定义一个JSON 格式的文件来存储所有有可切换语言的标签内的显示内容（Model 层），通过一个独立的控制类i18n.js 来负责页面间的具体的语种显示（Controller 层），通过定义可切换的标签中"data-i18n-type"与"data-i18n-tag"自定义属性来决定该标签显示的多语言类型与具体内容（View 层）。

【TODO】这边应该有个图

### 2.5 参数处理流程设计
与其他数据操作系统不同，本系统中的参数根据每次用户使用的功能不同而有不同的参数项目。所以本系统的对于参数的处理流程为：用户选择需要使用的功能，选择完相关的变量、配置后点击"下一步"，这时候在页面向后台提交数据之前会先读取用户选择的配置部分，并将这部分的值保存在一个有关这个功能的数组内，再将该数组保存在本地的sessionStorage 中。一般情况下，配置的值不作为参数传入后台，而仅仅是保存在前端页面中。等待后台返回相对应的结果后，再读取出该数组，并通过该配置数组控制显示相关的变量值等内容。

### 2.6 数据展示模块设计
在数据展示模块同样使用了MVC 架构模式。通过用户在提交时设置的标志位，在控制器resultTableGenerator.js（Controller 层）中判断采取哪种变量表格生成的方法。并在方法中取出之前返回成功结果的JSON 数据（Model 层），并对此数据在数据展示页（View 层）进行打印。

【TODO】这边应该有个图

## 三、系统主要功能实现
在系统设计时决定的前后台分离使系统的逻辑框架更为清晰。笔者在项目中主要负责前端部分，下面将主要讲解前端部分的功能实现。

### 3.1 数据文档上传
本系统现在支持四种数据文档格式的文件，分别是.xls，.xlsx，.dat，.txt。前端的主要职责是在用户选择文件后，并在上传之前判断该文件格式符不符合前文提到的四种文件格式，若不符合规范，应该在用户上传之前有相应的警告，并且提示用户上传正确格式的文件。

【TODO】一张用户上传文件失败的运行截图

若文件上传成功，后台会返回相应的JSON数据格式，返回结果有两种。
若所传文件的返回结果只有单张表单，则返回JSON 如下所示：
```javascript
{
  "ret_code": "0",
  "ret_msg": "",
  "ret_err": "",
  "token": "40E3884605BDC6EBBECBFCD144EA5C2E",
  "createTime": 57271883002276,
  "isMultiSheet": false,
  "fileName": null,
  "sheetNum": 0,
  "version": null,
  "sheetNameList": null
}
```
其中```isMultiSheet``` 为```false```，系统会直接跳转到数据展示页面。

若所传文件含有多张表单则返回JSON 如下所示：
```javascript
{
  "ret_code": "0",
  "ret_msg": "",
  "ret_err": "",
  "token": "C321A1DA295CBDDF4B8ED482BE09ACF4",
  "createTime": 56980719414133,
  "isMultiSheet": true,
  "fileName": "Sample_data.xls",
  "sheetNum": 5,
  "version": "2003",
  "sheetNameList": [
    "NingXia 10 Indicators in 85-08",
    "Hunan 12 Indecators in 88-06",
    "2004 CN consume composing",
    "2004 CN Town Family Situation",
    "West CN GDP 85-04 Per Captia "
  ]
}
```
其中```isMultiSheet```为```true```，此时系统会将返回的```sheetNameList```填充到下拉框中让用户选择。系统运行截图如下：
![multiinfo-isMultiSheet](img/multiinfo-isMultiSheet.jpg)
在用户选择待分析的表单后，页面跳转到数据展示页面。

### 3.2 变量选择规则设计与变量值存储
#### 3.2.1 变量选择规则设计
变量选择是本系统中的一个重点。在实践中我们发现，不同的功能对于变量选择的要求各不相同，过程中我们总结了变量选择的几种规则，分别是普通型（对于选择的变量无特殊要求）、连续选择性（所选的变量必须是连续不能有间断）、单选型（该组变量中有且只能选择一个变量）还有组合型（两组变量为组，不能重复选择相同的变量）。前端部分把这几种选择规则统一成一个独立的规则控制文件variableRule.js，由这个文件来控制变量选择区域所应用的变量规则具体类型。
variableRule.js 的具体实现逻辑如下：
```javascript
var variableRule = function () {
    //变量选择规则 - 普通型
    $('[data-variable-select-rule="normal"]').each(function () {
        $(this).find('.variable-wrapper').on('click', function (e) {
            if (!$(this).attr('disabled')) {
                $(this).toggleClass('active');
            }
        });
    });

    //变量选择规则 - 连续选择型
    $('[data-variable-select-rule="consequent"]').each(function () {

        var variableList = {};
        $(this).find('.variable-wrapper').map(function (i, elem) {
            variableList[$(elem).index()] = $(elem);
        });
        var variablesIndex = Object.keys(variableList);
        var _variablesIndex = Object.keys(variableList).reverse();

        $(this).find('.variable-wrapper').on('click', function () {
            //选择该变量之前的所有变量
            for (var i = variablesIndex[0]; i < $(this).index(); i++) {
                $(variableList[i]).addClass('active');
            }
            //取消该变量之后的所有变量
            for (var j = _variablesIndex[0]; j > $(this).index(); j--) {
                $(variableList[j]).removeClass('active');
            }

        });
    });

    //变量选择规则 - 单选变量型
    $('[data-variable-select-rule="single"]').each(function () {

        var that = this;
        $(this).find('.variable-wrapper').on('click', function () {
            //取消之前选择的
            if (!$(this).attr('disabled')) {
                $(that).find('.variable-wrapper').removeClass('active');
                $(this).addClass('active');
            }
        });
    });

    //变量选择规则 - 组合型
    if ($('[data-variable-select-group]')) {
        var groupList = $('[data-variable-select-group]').attr('data-variable-select-group').split(',');

        $('[data-group-name=' + groupList[0] + ']').on('click', '.variable-wrapper', function (e) {
            e.stopPropagation();
            $('[data-group-name=' + groupList[0] + ']').find('.variable-wrapper').map(function (index, variable) {
                $('[data-group-name=' + groupList[1] + ']').find('[data-toggle-select=' + $(variable).attr('data-toggle-select') + ']')
                    .attr('disabled', ($(this).hasClass('active')) ? true : false);
            });
        });

        $('[data-group-name=' + groupList[1] + ']').on('click', '.variable-wrapper', function (e) {
            e.stopPropagation();
            $('[data-group-name=' + groupList[1] + ']').find('.variable-wrapper').map(function (index, variable) {
                $('[data-group-name=' + groupList[0] + ']').find('[data-toggle-select=' + $(variable).attr('data-toggle-select') + ']')
                    .attr('disabled', ($(this).hasClass('active')) ? true : false);
            });
        });
    }
};
```
得益于HTML5 中的自定义data-* 属性，我们可以通过定义变量选择区域的data-variable-select-rule 属性，来使系统在指定区域加载指定选择规则。
以规则中单选为例，使用jQuery中的.each 方法可以操作所有的单选区域，并且在该区域下的".variable-wrapper"设置点击的监听事件。若判断当前点击的对象可选（没有"disabled"属性），那么给这个对象添加上"active"的标志类，表示以选中。

#### 3.2.2 变量值的获取与存储
根据统一的接口，前端部分会根据接口中入参设计的字段数、字段名确定页面中需要的变量组的个数和变量组的临时名称。通过自定义字段"data-config-group"来表示当前的结构内的变量为一组，通过自定义字段"data-group-name"来表示当前变量组的名称。因为判断组内的变量选中的情况不同，所以通过自定义字段"data-config-val-flag"来规范自定义字段的选中情况。
页面的结构如下：
```html
<div data-config-group
     data-group-name="dependentVariable"
     data-config-val-flag=".active"
     data-variable-select-rule="single"
     data-variable-group="dependentVariable,independentVariable">
     ...
</div>
```
获取与存储的脚本script.js 逻辑如下：
```javascript
$(function () {
    var CONFIG = {};
    $('[data-config-group]').each(function () {
        var groupName = $(this).attr('data-group-name');
        var checkedFlag = $(this).attr('data-config-val-flag');

        var selector = '[name=' + groupName + ']';
        if (checkedFlag) {
            selector += checkedFlag;
        }

        var configsList = [];
        $(selector).each(function () {
            configsList.push($(this).val());
        });
        CONFIG[groupName] = configsList;
    });
    sessionStorage.setItem('PRIVATE_CONFIG_FUNCTION_NAME', JSON.stringify(CONFIG));
});
```
这个脚本会在用户点击相对应的功能的时候随弹出框一起加载，并且每个脚本内的sessionStorage 存储的PRIVATE_CONFIG_FUNCTION_NAME 会因为功能名称的不同而各不相同。

### 3.3 本地配置存储
以『描述统计』功能中的『描述性』功能为例。在用户点击菜单中的相应菜单项是，系统会弹出如下框体：
![multiinfo-modal](img/multiinfo-modal.jpg)
系统将框体分为两部分，上半部分为用户选择的参数列表，下半部分的『选项』为待本地存储的配置参数项。


### 3.2 多语言切换
设计中提到的多语言配置的控制器i18n.js，其名称来源于internationalization（国际化），因首字母i与末字母n中间隔了18个字母，故缩写为i18n。

其逻辑如下：
```javascript
var i18n = function () {
    //多语言配置
    var lang = (localStorage.getItem("MULTIINFO_CONFIG_LANGUAGE")) ?
        localStorage.getItem("MULTIINFO_CONFIG_LANGUAGE") :
        "zh-cn";

    var CONFIG_LANG_STRING = sessionStorage.getItem('PRIVATE_CONFIG_LANGUAGE_STRINGS');

    if (CONFIG_LANG_STRING) {
        $('[data-i18n-tag]').each(function () {
            var String = JSON.parse(CONFIG_LANG_STRING);

            var that = this;
            $(that).html(String[$(that).attr('data-i18n-type')][lang][$(that).attr('data-i18n-tag')]);
        });
    } else {
        $.getJSON('js/config/String.json', function (String) {
            sessionStorage.setItem('PRIVATE_CONFIG_LANGUAGE_STRINGS', JSON.stringify(String));
            $('[data-i18n-tag]').each(function () {
                var that = this;
                $(that).html(String[$(that).attr('data-i18n-type')][lang][$(that).attr('data-i18n-tag')]);
            });
        });
    }
};
```

在用户第一次使用本系统的时候，因为没有相关的语言选项，默认为中文。用户可以在上传数据的页面右上角的『设置』中找到切换语言的菜单项。点击相对应的语言即可进行切换。
中遇到的需要切换多语言的情况
![multiinfo-language](img/multiinfo-language.jpg)

### 3.4 数据展示
数据展示是整个流程中的最后一个步骤。用户通过上一步选择的功能和配置信息，会在这一部分得出所需的结果。以功能“描述统计”中的“描述”为例，其结果截图如下：
![multiinfo-result](img/multiinfo-result.jpg)

结果的相关表格、图形展示，是通过相关的

## 四、系统难点的解决与创新
### 4.1 本系统的创新点
#### 4.1.1 多语言配置模块
    【TODO】多语言是这个系统中一个。。。
#### 4.1.2 功能模块化
#### 4.1.3 变量选择规则模块
#### 4.1.4 HTML5 数据存储
##### 4.1.4.1 本地存储API
    【TODO】根据localStorage 与sessionStorage 的特性不同，我们可以知道，localStorage 使用与存储常用的、不会经常改变配置，如用户语种选择、结果小数保留位数。而考虑到用户可能多次使用本系统，所以sessionStorage 更适合存储一些不用长时间存储的值，比如文件的sheet编号、相应功能的配置信息等。
##### 4.1.3.2 自定义data-* 数据存储
### 4.2 本系统的特色
### 4.3 本系统的难点
    【TODO】本系统的难点在与功能多、数据量复杂，配置、数据处理的情况各不相同。

## 总结

## 致谢
    本文在选题、撰写过程和系统的设计上得到了丁跃潮教授的细心帮助与指导，特此感谢。

## 参考文献
