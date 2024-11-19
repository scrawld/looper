# Looper

**Looper** 是一个轻量级、可靠的 Golang 定时任务库，用于管理和执行周期性任务。
它提供简单易用的接口，支持自定义任务间隔，并在任务执行时确保健壮的错误处理。

---

## 特性

- **简单易用**：只需几行代码即可添加周期性任务。
- **并发执行**：每个任务在独立的 Goroutine 中运行。
- **Panic 恢复**：自动捕获任务中的异常，确保服务稳定。
- **优雅停止**：支持任务的优雅退出，等待所有任务完成后停止。

---

## 安装

```bash
go get github.com/scrawld/looper
```

---

## 快速开始

以下是一个简单的使用示例：

```golang
package main

import (
	"context"
	"fmt"
	"time"

	"github.com/scrawld/looper"
)

func main() {
	// 创建一个新的 Looper 实例
	l := looper.New()

	// 添加周期性任务
	l.AddFunc(2*time.Second, func(ctx context.Context) {
		fmt.Println("任务 1 执行时间:", time.Now())
	})

	l.AddFunc(3*time.Second, func(ctx context.Context) {
		fmt.Println("任务 2 执行时间:", time.Now())
	})

	// 启动任务
	l.Start()

	// 运行 10 秒后停止
	time.Sleep(10 * time.Second)
	stopCtx := l.Stop()

	// 等待所有任务结束
	<-stopCtx.Done()
	fmt.Println("所有任务已优雅停止")
}
```

---

## 贡献

欢迎贡献代码！如果有任何问题或建议，请通过 [GitHub Issues](https://github.com/scrawld/looper/issues) 提交。

---

### 准备好简化你的定时任务了吗？
马上试试 **Looper** 吧！🚀
