# social-auto-upload（ZLZLGe fork）

本仓库 fork 自 [dreammis/social-auto-upload](https://github.com/dreammis/social-auto-upload)，遵循上游 MIT 协议，版权归原作者。

## 这个 fork 的改动

- 抖音视频上传上下文启用 `bypass_csp=True`。抖音上传页的 CSP 不允许 `blob:` Worker，而上传组件用 Worker 做分片，不开这个选项会一直「上传失败」。
- 记录 `create_v2` 发布接口的响应体，并在上传失败时保存进度区文字和截图，方便定位发布错误。
- 视频上传连续失败 2 次就放弃，不再无限重试。
- 发布成功后等待跳转的时间从 3 秒放宽到 15 秒，避免误判后重复点击发布。
- 标题输入兼容抖音的「填写作品标题 / 添加作品标题」两种 placeholder。
- 转载声明支持选择「取材站外」。
- 小红书只在显式提供来源时才勾选「来源转载」，避免空来源被默认打成转载。

## 注意

- `cookies/`、`conf.py`、`content/`、`qrcode.png`、`tools/` 属于本地账号、内容和调试产物，已在 `.gitignore` 中排除，不要提交。
- 如果用 `vstack` 等方式给视频补边，记得加 `setsar=1`。否则 SAR 可能被写成异常值，抖音发布接口会报 `532：请上传长宽比例不超过1:10的作品`。

## 使用

安装、CLI 和 Skill 用法见上游 README；`conf.example.py` 复制为 `conf.py` 后按需修改。