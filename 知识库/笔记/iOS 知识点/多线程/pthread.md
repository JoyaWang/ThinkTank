# pthread

- ### 简介

  > C语言
  >
  > 一套通用的多线程API
  >
  > 适用于Unix\Linux\Windows等系统
  >
  > 跨平台\可移植
  >
  > 线程生命周期程序员管理
  >
  > 使用难度大

- ### 创建线程的函数

  ```
  pthread_create(&pthread, NULL, runATask, (__bridge void *)(name));
  ```

  > - 参数1：线程编号变量的地址
  >
  > - 参数2：线程的属性变量的地址
  >
  > - 参数3：要创建的线程中要执行的函数(我们要做的任务就在这里)。这是个函数signature: void* (*) (void*)
  >
  >   > 这个函数signature分解: 返回值类型void*，函数名(* _Nonnull) 和参数类型(void* _Nullable)
  >   >
  >   > int *是指向int类型变量的指针，void *是指向任何类型变量的指针，有点类似OC中的id
  >   >
  >   > 参数4: 要执行的函数的参数
  >
  > - 返回值 int 0是成功， 非0是失败(可以是其他任何数，用来表示失败的原因)

