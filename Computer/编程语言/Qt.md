#### [C++ GUI Qt编程](http://www.qtcn.org/gpq4/) 
----
* [网站](https://www.informit.com/store/c-plus-plus-gui-programming-with-qt4-9780132354165)
> Qt 框架允许开发与多种平台(如 Windows、Linux、MacOS、QNX(最初称为Quick Unix[Qunix])、iOS 和 Android)兼容的应用。 凭借其一次编码的能力和随时随地部署的理念，它以更好的代码质量促进了更快的应用开发。 Qt 在内部处理特定于平台的实现，还使您能够在微控制器驱动的设备上使用令人印象深刻的 GUI 构建令人惊叹的超轻量级应用。响应动作,子类化QDialog
* Hello Qt!
```
#include <QApplication>
#include <QLabel>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    QLabel *label=new QLabel("Hello Qt!");
    label->show();
    return a.exec();
}
```


