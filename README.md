1、本地部署好graphrag之后，在graphrag-local-ollama目录下
    利用该指令提出问题：python-m graphrag.query--root./ragtest --method global "问题"
    利用该指令创造api接口：uvicorn api_v2:app --reload
2、在部署好浏览器插件brainy-ai-kimi之后，在该目录下
    执行：pnpm dev即可
