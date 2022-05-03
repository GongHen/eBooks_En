#### [C++ GUI Qt编程](http://www.qtcn.org/gpq4/)
----
* 1.1 Hello Qt!
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
* 1.2 响应动作
```
#include <QApplication>
#include <QPushButton>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    QPushButton *button=new QPushButton("Quit");
    QObject::connect(button,SIGNAL(clicked()),&a,SLOT(quit()));
    button->show();
    return a.exec();
}
```
* 1.3窗口控件布局
```
#include <QApplication>
#include <QHBoxLayout>
#include <QSlider>
#include <QSpinBox>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);

    QWidget *window=new QWidget;
    window->setWindowTitle("Enter Your Age");

    QSpinBox *spinBox=new QSpinBox;
    QSlider *slider=new QSlider(Qt::Horizontal);
    spinBox->setRange(0,130);
    slider->setRange(0,130);

    QObject::connect(spinBox,SIGNAL(valueChanged(int)),slider,SLOT(setValue(int)));
    QObject::connect(slider,SIGNAL(valueChanged(int)),spinBox,SLOT(setValue(int)));
    spinBox->setValue(35);

    QHBoxLayout *layout=new QHBoxLayout;
    layout->addWidget(spinBox);
    layout->addWidget(slider);
    window->setLayout(layout);

    window->show();

    return a.exec();
}
```
* 2.1 子类化QDialog
```
```
