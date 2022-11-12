### QML
#### [Fluid Elements动态元素](https://qmlbook.github.io/ch05-fluid/fluid.html#)
* `PropertyAnimation`属性动画 - Animates changes in property values
* `NumberAnimation`数字动画 - Animates changes in qreal-type values
* `ColorAnimation`颜色动画 - Animates changes in color values
* `RotationAnimation`旋转动画 - Animates changes in rotation values

* `PauseAnimation`停止动画 - Provides a pause for an animation
* `SequentialAnimation`顺序动画 - Allows animations to be run sequentially
* `ParallelAnimation`并行动画 - Allows animations to be run in parallel
* `AnchorAnimation`锚定动画 - Animates changes in anchor values
* `ParentAnimation`父元素动画 - Animates changes in parent values
* `SmoothedAnimation`平滑动画 - Allows a property to smoothly track a value
* `SpringAnimation`弹簧动画 - Allows a property to track a value in a spring-like motion
* `PathAnimation`路径动画 - Animates an item alongside a path
* `Vector3dAnimation`3D容器动画 - Animates changes in QVector3d values

* `PropertyAction`属性动作 - Specifies immediate property changes during animation
* `ScriptAction`脚本动作 - Defines scripts to be run during an animation
```
import QtQuick 2.12
import QtQuick.Window 2.12

Window {
    visible: true
    width: 960
    height: 600
    Item {
        id: root
        width: 960
        height: 600
        property int duration: 3000

        Rectangle {
            id: sky
            width: parent.width
            height: 400
            gradient: Gradient {
                GradientStop { position: 0.0;color: "#0080FF"}
                GradientStop { position: 1.0;color: "#66CCFF"}
            }
        }

        Rectangle {
            id: ground
            anchors.top: sky.bottom
            anchors.bottom: root.bottom
            width: parent.width
            gradient: Gradient {
                GradientStop { position: 0.0;color: "#00FF00"}
                GradientStop { position: 1.0;color: "#00803F"}
            }
        }


    }
    Image {
        id: ball
        x: 0;
        y: root.height-height
        source: "assets/soccer_ball.png"

        MouseArea {
            anchors.fill: parent
            onClicked: {
                ball.x = 0;
                ball.y = root.height-ball.height;
                ball.rotation = 0;
                anim.restart()
            }
        }
    }



    ParallelAnimation {
        id: anim
        SequentialAnimation {
            NumberAnimation {
                target: ball
                properties: "y"
                to: 20
                duration: root.duration * 0.4
                easing.type: Easing.OutCirc
            }
            NumberAnimation {
                target: ball
                properties: "y"
                to: 240
                duration: root.duration * 0.6
                easing.type: Easing.OutBounce
            }
        }
        NumberAnimation {
            target: ball
            properties: "x"
            to: 400
            duration: root.duration
        }
        RotationAnimation {
            target: ball
            properties: "rotation"
            to: 720
            duration: root.duration * 1.1
        }
    }

}
```
