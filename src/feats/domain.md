---
title: 自动秘境
order: 10
---
::: warning 注意

自动战斗、自动秘境功能目前只支持 1920x1080 分辨率

:::

自动秘境中自带有自动战斗的功能，两者配置共用，自动战斗任务可以在秘境外被启用。

## 自动战斗

在使用自动秘境功能前，请先正确配置自动战斗功能。

启动后，BetterGI 会通过 OCR 识别出当前右侧角色配队阵容，只支持4人队，支持流浪者识别，不支持主角识别。然后执行选择的战斗策略。

配队识别和战斗策略执行是完全独立的，也就是说队伍角色不来源于战斗策略，战斗策略中也无队伍中角色在几号位置的信息。

### 配队识别失败？

可以直接在“独立任务”页设置“强制指定配队”，用逗号分割（中英文都可以），**注意必须使用角色的官方中文名！必须是4人队伍！**

比如：`钟离，雷电将军，纳西妲，芙宁娜`

### 战斗策略脚本编写

和“七圣召唤”一样，战斗策略也提供了对应的自定义脚本配置，编写一个UTF-8格式的文本文件放入 `\User\AutoFight\` ，就能在 BetterGI 界面上看到并选择对应的战斗策略。

**和配队配置一样，角色名称必须使用官方中文名称！**

脚本语法如下：

| 名称 | 方法 | 别名 | 参数 | 说明 | 示例 |
| ---- | ---- | ---- | ---- | ---- | ---- |
| 元素战技 | skill | e | hold 代表长按，选填 | 触发键盘按下e键，并等待200ms。夜兰按两次e才能中断元素战技的释放。其中纳西妲长e会自动旋转。 | `skill`,`e`,`e(hold)` |
| 元素爆发 | burst | q |  | 触发键盘按下q键，至少会等待1.7秒，建议下一步动作为切换角色，保证元素爆发释放完成。 | `burst`,`q` |
| 普通攻击 | attack |  | 普攻持续时间(s)，选填 | 触发左键连击，每200ms触发一次左键单击 | `attack`,`attack(5.5)` |
| 重击 | charge |  | 长按的持续时间(s)，选填 | 长按左键。其中那维莱特重击会自动旋转。 | `charge`,`charge(6)` |
| 等待 | wait |  | 等待时间(s)，必填 | 程序等待 | `wait(0.5)` |
| 冲刺 | dash |  | 冲刺时间(s)，选填 | 朝当前方向冲刺 | `dash`,`dash(2)` |
| 跳跃 | jump | j |  | 跳跃一下 | `jump` |
| 行走 | walk |  | 行走的方向，必填、行走的时间(s)，必填 | 按下w/a/s/d行走 | `walk(w,0.2)` |
| 向前行走 | w |  | 行走的时间(s)，必填 | 按下w行走，等效于`walk(w,?)` | `w(0.2)` |
| 向左行走 | a |  | 行走的时间(s)，必填 | 按下a行走，等效于`walk(a,?)` | `a(0.2)` |
| 向后行走 | s |  | 行走的时间(s)，必填 | 按下s行走，等效于`walk(s,?)` | `s(0.2)` |
| 向右行走 | d |  | 行走的时间(s)，必填 | 按下d行走，等效于`walk(d,?)` | `d(0.2)` |

切换角色的时候会保证切换成功，但是元素战技/元素爆发的释放判断是没有的，所以请灵活使用wait保证技能释放成功

示例:

::: tabs

@tab 四神队.txt
```js
钟离 s(0.2),e(hold),wait(0.3),w(0.2),q
雷电将军 e
纳西妲 e(hold),wait(0.3),q
芙宁娜 e,wait(0.3),q
```
@tab 双水宵宫.txt
```js
钟离 s(0.2),e(hold),wait(0.3),w(0.2),q
夜兰 e,e,wait(0.8),e,e,wait(1.5),q
行秋 e,e,q
宵宫 e,attack(5)
```
:::


## 自动秘境

请站在秘境门口启动”自动秘境“功能，启动后自动刷本直到用光体力结束。当然也可以在设置中配置刷取次数。

![请站在秘境门口启动”自动秘境“功能](https://img.alicdn.com/imgextra/i2/2042484851/O1CN016CLDxN1lhoELu85HD_!!2042484851.jpg  =400x)

请保证进入前有背包有空间领取奖励，不然会卡死在领取奖励的过程中。

使用此功能前请确保自动战斗功能能够正常运行。

### 石化古树无法识别？

当前训练集有限，只是训练一些高频刷取的本的石化古树（枫丹新本、绝缘、每个地区具有代表性的圣遗物本）。

如果出现无法识别到石化古树的现象，请联系作者补充训练集。