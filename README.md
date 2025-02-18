# 本地版服务器性能测试工具(基于宝塔跑分)

## 项目简介

本项目基于宝塔 Linux 面板官方的服务器性能测试工具，移除了身份验证、评分上传和数据加密/解密功能，仅保留本地性能测试模块。  
用户可以独立运行本工具，在本地评估服务器的 CPU、内存和磁盘性能等，而无需联网提交数据。

## 主要修改点

- **移除联网功能**：删除了所有与 `bt.cn` 服务器的通信接口，包括身份验证 (`CheckToken`)、评分提交 (`SubmitScore`) 和配置上传 (`SubmitSetScore`)。
- **保留完整的本地测试功能**：
  - **CPU 测试**：支持整数运算、浮点运算、多线程计算、排序等基准测试。
  - **内存测试**：评估系统内存大小。
  - **磁盘测试**：测试磁盘的读写速度。
- **代码精简**：移除了 `En_Code` 和 `De_Code` 数据加密/解密功能，直接使用 JSON 进行数据存储和处理。

## 使用方法

### 1. 运行测试

本工具无需安装额外依赖，仅需 Python3 运行环境和相关第三方库如`psutil`

```bash
python3 btScore_local.py
```

### 2. 运行单项测试

#### CPU 性能测试
```python
from btScore_local import score_main
benchmark = score_main()
cpu_result = benchmark.testCpu(None)
print(cpu_result)
```

#### 内存性能测试
```python
mem_result = benchmark.testMem(None)
print(mem_result)
```

#### 磁盘性能测试
```python
disk_result = benchmark.testDisk(None)
print(disk_result)
```

### 3. 查看测试结果

测试结果将以 JSON 格式存储在 `plugin/score/score.json`，可以手动读取该文件，或使用 `readScore()` 方法：
```python
scores = benchmark.readScore()
print(scores)
```

## 适用场景

- **离线测试**：本工具无需网络连接，可在本地环境下独立运行。
- **私有服务器评估**：适用于云服务器、物理机、自建服务器等性能测试。
- **定期监测服务器性能**：可配合 `cron` 定时任务，定期运行测试并记录结果。

## 贡献

欢迎提交 Issue 和 Pull Request，改进本地版的服务器性能测试工具！