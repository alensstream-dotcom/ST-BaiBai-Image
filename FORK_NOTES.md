# 非官方二次开发说明 / Unofficial fork

原项目：**柏宝绘 · ST-BaiBai-Image**
原作者：**柏柏**（GitHub: [baibai-git/ST-BaiBai-Image](https://github.com/baibai-git/ST-BaiBai-Image)）
本 Fork 维护者：**alensstream-dotcom**

本仓库从原项目 `1187528c5b796a686c57659556dfaecdd2ddfbf9` 开始修改；不是原作者的官方版本。本说明用于如实标记来源，不暗示原作者认可或参与后续修改。

## 本次修复范围

1. **目标正文识别**：优先选取 `<content>` 中的正文，移除 `<cot>`、`<options>`、`<tucao>` 等规划/选项/复盘标签。不改变插图锚点到**原始物理行号**的映射。
2. **JSON 解析**：候选 JSON 中优先选择确实包含 `images` 数组的对象，不再轻易误选先前的建档示例或规划对象。真正缺失 `images` 仍然会报错，而不是伪造图片。
3. **请求历史**：在 JSON 验收之前记录原始可见回复、usage、`finish_reason` 与可用的 `native_finish_reason`。解析失败的回复仍标记为失败，但允许在请求历史中查看与复制。仅保存在本次页面会话内，长文本仍按原插件的 20,000 字符上限截断。
4. **回归测试**：新增正文清洗、行号映射、JSON 候选识别、失败回复留存及流式终止原因的测试。

保留原插件的角色固定外貌库、服装时间线、自动插图、ComfyUI / NovelAI 后端、用户自定义提示词与多图选择机制。本次不修改其成人内容审查策略，也不保证特定 OpenRouter 提供商一定能够稳定生成 JSON。

## 构建和安装

插件由 `manifest.json` 引用已打包的 `dist/index.js`。仅修改 `src/` **不会改变实际安装运行的代码**。

修复分支包含自动测试/构建工作流（`.github/workflows/fork-build.yml`），运行 `pnpm typecheck`、`pnpm test`、`pnpm build`，成功后再将打包产物提交到同一分支。若 Fork 的 GitHub Actions 尚未启用，先到仓库 **Actions** 页面启用工作流；构建产物未生成前不要将该分支视为可安装的修复版。

## 许可与来源

Fork 时原仓库根目录未发现明确的 `LICENSE` 文件。因此本仓库不声称获得额外的复制、修改或公开再发布许可；署名不能替代授权。公开分发前请向原作者确认许可条件。