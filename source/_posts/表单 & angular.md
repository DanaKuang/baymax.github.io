---
title: 表单 & angular1.3.2
date: 2018-03-20 10:06:22
tags: [form, angular]
---

趁着产品提新需求，调整之前saas活动这块的表单验证。新建/编辑活动总共要传40多个参数，想想就费劲…

思路是这样的：
表单的每一项都采用填写完毕即判断有效与否，最后提交时再做总的非空&有效性验证。满足以上两个才发请求，并控制按钮的勿重复操作。

技术栈:
bootstrap(3.0) + angular(1.3.2)

html结构:
form.form-horizontal
    .form-group.has-feedback ng-class="{'has-error': form.name.$dirty && (form.name.$error.required || form.name.$invalid), 'has-success': form.name.$valid}"
        .label-control.col-sm-2.col-md-4
        .col-sm-10.col-md-8
            .form-control.input-sm ng-pattern="/XXX/"
            .glyphicon.form-control-feedback ng-class="{'glyphicon-ok': XXX}"
            .glyphicon.form-control-feedback ng-class="{'glyphicon-remove': XXX}"
延伸一下:
<div class="form-group">
    <label class="sr-only">Email</label>
    <p class="form-control-static">email@example.com</p> //可以用来作为表单填写示范
</div>

label 的sr-only 类名可以隐藏label标签
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
        如果需要inline排列，可以在label上加上checkbox-inline,radio-inline让排列在一行
以上结合angular内置的表单校验功能 + boostrap，可以满足input[type=”text”]类型表单的基本校验

原生的表单相关功能：
reset()
checkValidity()，非空检验，不再于有没有被触发，只要是空就无法通过checkValidity的校验。
form.selectname.selectedOptions获得这个选择框的择项，它是一个数组，对于单选来说，就取第一个，即
[0]

form表单校验

格式化日期，为指定板式，暴露接口

html5 表单，搜索

angular 表单


