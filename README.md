# agent_peivite · 可追溯知识 Agent 作品集

基于 AnythingLLM 的知识问答、Mem0 记忆工作台，以及 Agent 评测回放面板。个人贡献聚焦回答依据快照、结构审计、失败反馈及可回放运行记录。

## 三个项目

| 项目 | 功能 | 本地页面 |
|---|---|---|
| 知识 Agent | 文档问答、查看候选依据和压缩后消息、引用结构检查、JSONL 导出 | http://localhost:3100 |
| Mem0 工作台 | 确认写入、新会话召回、用户隔离、更新删除、修改记录 | http://localhost:8501 |
| 评测与回放 | 固定案例、JSONL 导入、回答/依据对照、人工标签、失败筛选、指标导出 | http://localhost:8502 |

## 本地安装和启动

已验证环境：macOS Apple Silicon、Node 20.19.5、Yarn 1.22.22、Python 3.12。其他平台尚未完成完整验收。

```bash
git clone https://github.com/zhenglianglala-wq/agent_peivite.git
cd agent_peivite
python3.12 portfolio/scripts/bootstrap.py
cp portfolio/local-config.example.json portfolio/local-config.json
chmod 600 portfolio/local-config.json
```

在本地编辑配置，填写聊天/embedding 的兼容 `/v1` 端点、模型名及各自 API Key。本次已验证阿里云北京端点、qwen-plus、text-embedding-v4。**仓库不包含 Key，配置不能提交。** 模型调用使用提供方额度；安装脚本不下载模型权重，也不安装 Puppeteer 浏览器。

```bash
python3 portfolio/scripts/start_all.py
```

第一次进入知识页面，创建工作区并上传 `portfolio/materials/项目说明.txt`，等待处理并加入工作区，随后提问。服务端更新后需重启。详细说明见 [项目运行说明](portfolio/README.md)。

## 学习和演示

- [项目学习手册](portfolio/项目学习手册.md)：10次实操、源码阅读、RAG/Agent/记忆/评测及代码练习。
- [学习路线与操作记录](portfolio/学习路线与操作记录.md)
- [完成度与验收报告](portfolio/完成度与验收报告.md)
- [演示脚本](portfolio/演示脚本.md)

## 验证结果与边界

20条实际问答运行完成，8类真实Mem0/embedding行为和3类来源专项通过；有独立回归及浏览器检查。测试资料为合成演示数据。**运行完成不代表回答内容正确**：QA-18出现了资料外表结构补充，已保留为待评审案例，人工内容评分仍pending。

快照首版覆盖本地 Web 文本 RAG 路径，保留压缩前候选来源与压缩后生成层消息。它们不能证明模型实际依赖了某个片段。结构检查与人工内容支持判断分开。MCP深度联动、Langfuse和自动语义judge未计入首版；连续演示录屏尚未制作。

## 上游与许可证

基于 [AnythingLLM](https://github.com/Mintplex-Labs/anything-llm)，固定上游 commit `2a10d052a1812d7be12c43f9024072cf26a27a8b`。保留上游 MIT [LICENSE](LICENSE)、[原始介绍](UPSTREAM_README.md)及[归属说明](NOTICE.md)。上游已有文档聊天、引用、记忆、工具与MCP，不包装为个人新增能力。

仓库仅发布源码、文档和合成测试证据，排除本地凭据、数据库、依赖、缓存及上游GitHub自动工作流。
