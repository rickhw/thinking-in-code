

# 題目

任務分配控制器

## 前提

有五十台機器，有五種規格，每種規格有十台，規格如下：

* CPU core 2, RAM 8G
* CPU core 4, RAM 16G
* CPU core 8, RAM 32G
* CPU core 16, RAM 64G
* CPU core 32, RAM 128G

五種程式 (Task) 要跑，每種程式所需要的資源如下：

* Task A: 2 core, 8G
* Task B: 4 core, 10G
* Task C: 8 core, 16G
* Task D: 32 core, 24G
* Task E: 1 core, 64G

每個 Task 執行的時候，必須有時間限制，如果執行時間超過必須被中斷，然後主動重跑，或者重跑幾次。


## 題目

設計一個資源分配器 (Distributor)，分配這五種程式到機器上執行，但必須在最短時間完成所有指定的工作。例如指定工作 Mission A 如下：

* Task A 跑 5 次
* Task B 跑 2 次
* Task C 跑 3 次
* Task D 跑 1 次
* Task E 跑 2 次

Mission B：

* Task A 跑 1 次
* Task B 跑 2 次
* Task C 跑 3 次
* Task D 跑 5 次
* Task E 跑 4 次

## psudeo code

```java
TaskDefines = {
    A = [2, 8],
    B = [4, 10],
    C = [8, 16],
    D = [32, 24],
    E = [1, 64]
}

Mission_A = { A: 5, B: 2, C: 3, D: 1, E: 2 }
Mission_A = { A: 1, B: 2, C: 3, D: 5, E: 4 }

// 分配器
Distributor(TaskDefines, Mission_A)
Distributor(TaskDefines, Mission_B)
```
