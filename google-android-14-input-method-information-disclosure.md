# 漏洞描述

google Android 14（智能手机操作系统）中发现了一个漏洞(CVE-2023-21336)，在输入法中，由于侧通道信息泄露，有一种可能无需查询权限即可确定应用程序是否安装的方法。这可能会导致本地信息泄露，而无需额外的执行权限。利用该漏洞不需要用户交互。

# 漏洞影响：
受影响软件

#          类型                 厂商               产品                 版本                       影响面

1          系统             google             android                *                     Up to(excluding)14.0

对应用开发者影响评估：
谷歌在安卓14发布了一些系统安全漏洞的补丁，基于[系统安全](https://cncso.com)考虑，华为侧评估这些漏洞补丁需要合入现有和后续的系统版本中。Google的补丁号是[CVE-2023-21336](https://cncso.com)，合入后Google接口InputMethodManager类中getEnabledInputMethodList 和getInputMethodList接口的返回值将会产生变化，可能会对业务造成影响。如果应用涉及这两个接口的调用，建议在AndroidManifest.xml中增加queries权限避免造成影响。针对开发者会造成一定影响面。

# 开发者修复：

一、权限添加示例：

<!– To query enabled input methods. –>
<queries>

<intent>

<action android:name=”android.view.InputMethod” />

</intent>

</queries>

# 二、返回示例：
1．合入补丁后具体接口的返回示例如下：

比如有5个输入法，手机上 （搜狗(默认输入法)、QQ拼音（用户勾选）、微信键盘(用户勾选)、讯飞、Goard）

添加queries权限：

getEnabledInputMethodList获取的内容：搜狗、QQ拼音、微信键盘

getInputMethodList获取的内容：搜狗(默认输入法)、QQ拼音（用户勾选）、微信键盘(用户勾选)、讯飞、Goard

2、未添加queries权限的返回示例如下：

getEnabledInputMethodList获取的内容：搜狗

getInputMethodList获取的内容:搜狗

备注：因为搜狗输入法是手机默认输入法，所以是否添加queries权限都能有返回值。其他输入法获取返回值会受影响。

# 三、建议排查：

1、是否涉及接口调用；

2、如涉及接口调用，该谷歌补丁是否会对应用造成影响；

# 参考链接：
https://source.android.com/docs/security/bulletin/android-14
[首席安全官](https://cncso.com/google-android-14-input-method-information-disclosure.html)



