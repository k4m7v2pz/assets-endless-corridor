# 音频格式转换指南

本文档说明如何将 MP3 格式的音频文件转换为 OGG 格式，以便在游戏中使用。

## 为什么使用 OGG 格式

- **文件更小**：OGG Vorbis 格式通常比 MP3 节省 30-50% 的空间
- **开源友好**：OGG 是完全开源的音频格式，没有专利限制
- **游戏兼容**：Arcade/Pyglet 对 OGG 格式的支持更好

## 转换命令

使用 FFmpeg 将 MP3 转换为 OGG 格式：

```bash
ffmpeg -i "input.mp3" -vn -c:a libvorbis -q:a 4 "output.ogg"
```

### 参数说明

| 参数 | 说明 |
|------|------|
| `-i "input.mp3"` | 输入文件路径 |
| `-vn` | 禁用视频流（移除封面图片等） |
| `-c:a libvorbis` | 使用 Vorbis 音频编码器 |
| `-q:a 4` | 音频质量（0-10，4 为高质量，约 128-160kbps） |
| `"output.ogg"` | 输出文件路径 |

## 命名规范

转换后的文件应使用小写 SHA256 哈希值命名：

```bash
# 计算文件的 SHA256 哈希值
sha256sum "output.ogg"

# 重命名为哈希值.扩展名
mv "output.ogg" "<hash>.ogg"
```

## 完整示例

```bash
# 1. 转换 MP3 为 OGG
ffmpeg -i "Main Menu.mp3" -vn -c:a libvorbis -q:a 4 "Main Menu.ogg"

# 2. 计算 SHA256 哈希值
sha256sum "Main Menu.ogg"
# 输出示例：9cb7a52c59405723c58f47e80ca579baa22f44acf0ea1169eed88b2e29f92161  Main Menu.ogg

# 3. 重命名为哈希值
mv "Main Menu.ogg" "9cb7a52c59405723c58f47e80ca579baa22f44acf0ea1169eed88b2e29f92161.ogg"
```

## 当前目录中的文件

| 文件名 | 说明 |
|--------|------|
| `53ff7a8878fa8b380d6250628f19044053dcb6ac956dd0cad56c801a21574131.ogg` | 游戏背景音乐 (Cracked Nursery Key) |
| `LICENSE` | 音频文件许可证 |
| `CONVERSION.md` | 本文档 |

## 注意事项

1. **保留源文件**：建议在转换前保留原始 MP3 文件，直到确认 OGG 文件正常工作
2. **质量选择**：`-q:a 4` 提供良好的音质和文件大小平衡，如需更高质量可增加到 6-8
3. **批量转换**：如需批量转换多个文件，可以使用 shell 循环脚本
