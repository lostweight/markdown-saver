# Linux 系统遇到的问题以及解决办法

## 充电的时候电池显示未充电：

原因：UPower 服务出错，卡在了 `pending-charge` 状态，因此一直显示未充电

解决办法：

```
sudo systemctl restart upower
```



### upower 是什么东西？

UPower 是 Linux 桌面上负责 电源信息 的后台服务

它干的事情非常简单：

* 读取内和里面的电池/适配器状态（是否插电、电量多少、是否在充电）

* 将这些信息提供给 GNOME (GNOME 在右上角显示图表，休眠策略等)

所以在不在充电是由硬件和内和决定的

而显示错误是由 upower 决定的
