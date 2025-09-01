# ⚠️ Windows 未签名版本使用说明

## 为什么会出现"文件在使用中"错误？

这个构建版本是自编译的，没有购买代码签名证书（年费约 $300-500），因此 Windows 会将其视为潜在风险文件。

## 🔧 解决方法

### 快速解决（推荐）

1. **下载文件后，先不要双击运行**
2. **右键点击** exe 文件
3. 选择 **"属性"**
4. 在底部找到 **"此文件来自其他计算机，可能被阻止"**
5. 勾选 **"解除锁定"**
6. 点击 **"确定"**
7. 现在可以正常运行了

### 如果还是不行

**方法 A：使用 PowerShell**
```powershell
# 右键开始菜单，选择 PowerShell（管理员）
# 导航到下载目录
cd $env:USERPROFILE\Downloads

# 解除文件锁定
Unblock-File -Path ".\Bitwarden-Portable-*.exe"

# 运行程序
.\Bitwarden-Portable-*.exe
```

**方法 B：临时禁用 Windows Defender**
1. Windows 设置 → 更新和安全 → Windows 安全中心
2. 病毒和威胁防护 → 管理设置
3. 关闭"实时保护"（会在重启后自动开启）
4. 运行程序
5. 程序启动后，重新开启实时保护

**方法 C：添加排除**
1. Windows 安全中心 → 病毒和威胁防护
2. 管理设置 → 排除项 → 添加排除项
3. 选择"文件夹"
4. 选择你存放 Bitwarden 的文件夹

## 🔒 安全说明

- ✅ 此版本是从开源代码编译的，完全透明
- ✅ 没有添加任何恶意代码或后门
- ✅ 源代码：[dbds-team/my_bitwarden_client](https://github.com/dbds-team/my_bitwarden_client)
- ❌ 缺少数字签名（需要付费证书）

## 📝 验证文件完整性

下载后可以验证 SHA256 哈希值：
```powershell
# PowerShell 中运行
Get-FileHash ".\Bitwarden-Portable-*.exe" -Algorithm SHA256
```

对比 Release 页面提供的 `checksums-*.txt` 文件中的值。

## 💡 替代方案

如果实在无法运行 Windows 版本，可以考虑：

1. **使用 Web 版本**
   - 下载 `bitwarden-web-*.tar.gz`
   - 解压后用浏览器打开 index.html

2. **使用浏览器扩展**
   - Chrome/Edge: `bitwarden-browser-chrome-*.zip`
   - Firefox: `bitwarden-browser-firefox-*.zip`

3. **使用 CLI 版本**
   - `bitwarden-cli-windows-*.zip`
   - 命令行工具，无需 GUI

## ❓ 常见问题

**Q: 为什么官方版本没有这个问题？**
A: 官方版本购买了 EV 代码签名证书，Windows 会信任。

**Q: 这个版本安全吗？**
A: 是的，代码完全开源，构建过程透明，你可以查看所有源代码和构建日志。

**Q: 能否添加数字签名？**
A: 可以，但需要：
- 购买代码签名证书（$300-500/年）
- 或使用自签名证书（仍会有警告，但比没有好）

**Q: 为什么要用这个版本而不是官方版本？**
A: 如果你信任官方版本，建议使用官方版本。这个版本适合：
- 想要完全控制代码的用户
- 需要自定义功能的用户
- 学习和研究目的