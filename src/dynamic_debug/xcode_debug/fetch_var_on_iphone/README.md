# Fetching Variables on iPhone

之前调试期间，遇到一个情况：

当：部分函数汇编代码非常长，时，触发了断点后，会出现：

卡死现象 == 等待期间，右上角状态会显示：

* Fetching Variables on iPhone
  * ![xcode_fetching_var_on_iphone](../../../assets/img/xcode_fetching_var_on_iphone.png)

此处等待一段时间后，获取完成后，正常显示触发断点处的代码：

![xcode_normal_trigger_breakpoint](../../../assets/img/xcode_normal_trigger_breakpoint.png)
