## 注释占比 15%左右

https://www.solidot.org/story?sid=65769

通过代码注释，可以看出代码作者的编码功底。新手写代码，要么不写注释，要么注释里尽写些废话，犹如画蛇添足；而优秀的程序猿写的注释言简意赅、恰到好处，有画龙点睛之妙。

## 标准制定

是否合理，还是制定者个人喜好，哪些地方需要制定规范

能否自动化/增加的工作量有多少？

主流项目是否制定了这个标准

## 代码检查

https://blog.csdn.net/qq_36631379/article/details/114533196

https://blog.csdn.net/qq_35333978/article/details/122347687

## google c++ 编程规范

https://zh-google-styleguide.readthedocs.io/en/latest/

https://google.github.io/styleguide/cppguide.html

## 更改 VS Code C++ 默认代码风格为 Google C++ Style

https://blog.csdn.net/sinat_34524528/article/details/85878592

## C++编程规范

https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#main

## 有的注释风格需要许多重复性劳动，应舍弃之，改用易于维护的注释风格。

## 直接把代码注释掉是讨厌的做法。别这么干！

《代码整洁之道》4.4.12

## c++在提交代码到git时，要保留注释掉的代码吗？

通常情况下，在提交代码到 Git 时，建议不要将注释掉的代码保留在提交中。Git 提交应该只包含当前正在使用的代码，而不是注释掉的或被废弃的代码。

如果注释掉的代码是针对特定情况的备份或调试目的，最好将其保存在本地，而不要将其提交到共享的代码库中。这可以通过本地的备份或分支来实现。Git 提交的目的是记录代码的改变历史，如果注释掉的代码不再需要，最好将其删除，保持提交的干净和可读性。

然而，有时注释掉的代码可能对于理解历史上的更改或者作为参考是有用的。在这种情况下，可以考虑使用版本控制系统的一些技巧，比如使用 git blame 或 git log 来查看代码历史，而不必保留注释掉的代码在提交中。

## 魔法字符串

https://www.cnblogs.com/perhaps/archive/2005/07/06/187464.html

## BS C++ style

https://www.stroustrup.com/bs_faq2.html

## 匈牙利记法

NL.5: Avoid encoding type information in names

https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rl-knr

## c++101编程规范

https://killwing.github.io/c++-coding-standards.md.html

## 函数默认传递指针用const修饰

 `[CG]Con.3`

## 魔数/魔法字符串

ES.45: Avoid “magic constants”; use symbolic constants
