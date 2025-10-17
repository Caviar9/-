## 摸鱼浏览器（MiniBrowser）

一个基于 PyQt5 + QtWebEngine 的轻量浏览器，内置纯黑主题、置顶、小窗透明度调节、老板键与简单导航栏。默认打开抖音，可自定义访问任意网址。

### 功能特性
- 纯黑深色主题（可在设置中切换浅色/深色/跟随系统）
- 窗口置顶与透明度滑条
- 老板键（快捷最小化），可在设置里自定义
- 简易导航栏：返回/前进/地址栏/前往
- 一键打开抖音移动版
- 自定义 User-Agent（当前为桌面 Chrome UA）

### 环境要求
- Windows 10/11
- Python 3.8+（建议 3.10）
- 依赖：PyQt5、PyQtWebEngine

安装依赖：
```bash
pip install PyQt5 PyQtWebEngine
```

### 运行
```bash
python webmini.py
```

首次运行会打开抖音主页；也可在地址栏输入任意网址，回车或点击“前往”。

### 界面与操作
- 顶部：
  - 置顶按钮：在“📌置顶/📍置顶”之间切换
  - 返回/前进：页面历史导航
  - 地址栏：输入网址，支持自动补全 `https://`
  - 前往：加载地址栏中的链接
  - 📱移动版：一键打开 `https://m.douyin.com`

- 底部：
  - 透明度滑条：5% ~ 100%
  - ⚙ 设置：打开设置窗口

- 设置窗口：
  - 老板键：输入如 `F1` 或 `Ctrl+Q`，点击“保存”即可更新
  - 主题模式：浅色 / 深色 / 跟随系统

### 快捷键（默认）
- 老板键：F1（在设置中可改）

### 常见问题（FAQ）
1) 抖音提示“不支持的音频/视频格式”
- 这通常与系统缺少解码器有关。建议在微软商店安装：
  - HEVC Video Extensions（HEVC/H.265）
  - AV1 Video Extension（AV1）
- 某些内容需要 H.264/AAC，一般系统自带；若为精简系统可能缺失对应解码组件，请补全后重试。
- 若仍有问题，可点击“📱移动版”使用移动站点，它通常优先使用 H.264/AAC。

2) 显示“设备无网络”或页面报网络相关错误
- 请先在地址栏访问 `https://www.baidu.com` 确认是否能正常打开。
- 检查公司/校园网络是否对 `douyin.com` 做了域名或 SNI 层面的拦截；必要时切换网络环境。
- 检查代理/安全软件是否拦截了 QtWebEngine 流量。

3) 自动播放/有声音但卡顿
- 已在程序内关闭“需要用户手势才播放”的限制，但具体站点策略可能不同。
- 若视频卡顿，建议改用移动站点或降低分辨率；也可检查系统硬件解码支持与显卡驱动。

4) 深色样式没有生效
- 主题为应用层样式；部分站点自身样式可能覆盖。已注入基础黑色背景与前景色，但不是完整全网“深色化”方案。

5) 修改图标
- 将 `1.ico` 放在与 `webmini.py` 同目录下即可。

### 目录结构（示例）
```
Downloads/
├─ webmini.py
├─ README.md
└─ 1.ico            # 可选，窗口图标
```

### 开发说明（针对当前源码）
- 入口：`webmini.py` 最下方 `if __name__ == '__main__':`
- 主窗口类：`MiniBrowser`
- 自定义页面类：`CustomWebPage`（处理 UA 与新窗口）
- 设置窗口类：`SettingsWindow`
- 主题切换：`MiniBrowser.apply_theme`
- 页面加载后注入：`MiniBrowser.apply_page_dark_css`（用于基础黑色样式和 UA 伪装）

如需改为移动端 UA，可在 `MiniBrowser.__init__` 中调整：
```python
profile.setHttpUserAgent(
    "Mozilla/5.0 (iPhone; CPU iPhone OS 17_0 like Mac OS X) "
    "AppleWebKit/605.1.15 (KHTML, like Gecko) "
    "Version/17.0 Mobile/15E148 Safari/604.1"
)
```

### 许可证
本项目示例性质，未附带许可证，按“现状”提供；在使用站点内容时请遵守其相关条款与法律法规。


