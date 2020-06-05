# UIControl

## 控制事件 UIControl.Event

    touchDown: 按下?
    touchDownRepeat: 连续按下?
    touchDragInside:
    touchDragOutside:
    touchDragEnter:
    touchDragExit:
    touchUpInside:
    touchUpOutside:
    touchCancel:
    valueChanged:
    primaryActionTriggered:
    editingDidBegin:
    editingChanged:
    editingDidEnd:
    editingDidEndOnExit:
    allTouchEvents:
    allEditingEvents:
    applicationReserved:
    systemReserved:
    allEvents:
- 启用 isEnabled
- 选中 isSelected 
- 高亮 isHighlighted
- 添加监听控制事件的对象和方法 addTarget(target:action:for controlEvents) 
- 监听控制事件的对象和方法removeTarget(target:action:for controlEvents)
- 移除 allTargets
- 发送某个控制事件的行为? sendAction(action: to target: for event)
- 发送控制事件的行为? sendActions(for controlEvents: )

