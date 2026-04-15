## 项目介绍
本项目基于 **GraphRAG Local Ollama** 实现本地大模型知识图谱检索，并通过 **BrainyAI 浏览器插件**提供可视化交互界面，实现本地私有化 AI 查询服务。

## 环境依赖
- Python 3.10
- Node.js
- pnpm
- Ollama

---

# 一、GraphRAG Local Ollama 部署步骤

## 1. 创建并激活虚拟环境
```bash
conda create -n graphrag-ollama-local python=3.10
conda activate graphrag-ollama-local
```

## 2. 安装 Ollama
```bash
curl -fsSL https://ollama.com/install.sh | sh
pip install ollama
```

## 3. 下载模型
```bash
ollama pull mistral
ollama pull nomic-embed-text
```

## 4. 克隆项目
```bash
git clone https://github.com/TheAiSingularity/graphrag-local-ollama.git
cd graphrag-local-ollama/
```

## 5. 安装依赖
```bash
pip install -e .
```

## 6. 创建输入目录并放入数据
```bash
mkdir -p ./ragtest/input
cp input/* ./ragtest/input
```

## 7. 初始化项目
```bash
python -m graphrag.index --init --root ./ragtest
cp settings.yaml ./ragtest
```

## 8. 构建索引（生成知识图谱）
```bash
python -m graphrag.index --root ./ragtest
```

---

# 二、启动服务

## 1. 命令行提问（测试用）
```bash
python -m graphrag.query --root ./ragtest --method global "你的问题"
```

## 2. 启动 API 接口（供插件调用）
```bash
uvicorn api_v2:app --reload
```

---

# 三、浏览器插件 BrainyAI 部署

进入浏览器插件项目目录 `brainy-ai-kimi`，执行：

## 1. 安装 pnpm
```bash
npm install pnpm -g
```

## 2. 安装依赖
```bash
pnpm install
```

## 3. 启动插件开发服务
```bash
pnpm dev
```

启动成功后，在浏览器中加载已解压的扩展程序，选择插件目录即可使用。

---

## 四、使用流程（最简总结）
1. 启动 GraphRAG API：
```bash
uvicorn api_v2:app --reload
```
2. 启动浏览器插件：
```bash
pnpm dev
```
3. 在浏览器插件中发送查询，即可调用本地 GraphRAG 服务。

---

## 五、项目说明
- 所有模型与数据均在本地运行，无需联网 API
- 支持本地知识图谱构建与全局查询
- 浏览器插件提供轻量化交互界面
- 完全开源、免费、可二次开发

---
