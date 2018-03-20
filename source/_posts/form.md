---
title: form
date: 2018-03-20 10:06:22
tags: [form, angular]
---

bootstrap 样式，交互

form表单校验
    form.checkValidity()
    空校验，最后；填写正确与否，当下

    一般结构：
    form.form-horizontal|.form-inline|''
        div.form-group.col-md-5.form-group-lg|.form-group-sm.has-feedback ng-class="{'has-error': XXX, 'has-success': XXX, 'has-warning': XXX}"
            label.control-label.col-sm-2 for="XX"
            div.col-sm-10
                input.form-control.input-lg|.input-sm#XX type="text"
                span.glyphicon.form-control-feedback ng-class="{'glyphicon-ok': XXX}"
                span.glyphicon.form-control-feedback ng-class="{'glyphicon-remove': XXX}"
    <div class="form-group">
        <label class="sr-only">Email</label>
        <p class="form-control-static">email@example.com</p> //例子
    </div>
    *label 的sr-only 类名可以隐藏label标签
    如果输入框前后有说明，结构建议如下：
        div.form-group
            label.sr-only
            div.input-group
                div.input-group-addon
                input.form-control type="text"
                div.input-group-addon
    如果是勾选框，建议结构如下：
        div.radio.disabled
            <label for="">
                <input type="radio" name="optionsRadios" id="optionsRadios3" value="option3" disabled>Option three is disabled
            </label>
        如果需要inline排列，可以在label上加上checkboxl-inline,radio-inline让排列在一行
    * 不要将表单组和输入框组混合使用，建议将输入框组嵌套到表单组中使用



格式化日期，为指定板式，暴露接口

html5 表单，搜索

angular 表单


